---
title: "Lync Server 2013: Ricerca con MS SharePoint Server 2013 dati archiv. di MS LS 2013"
TOCTitle: "Lync Server 2013: Ricerca con MS SharePoint Server 2013 dati archiv. di MS LS 2013"
ms:assetid: 17f49365-8778-4962-a41b-f96faf6902f1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ687978(v=OCS.15)
ms:contentKeyID: 49887458
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione di Microsoft SharePoint Server 2013 per la ricerca di dati archiviati di Microsoft Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-02-04_

Uno dei principali vantaggi derivanti dall'archiviare le trascrizioni delle sessioni di messaggistica istantanea e Web Conferencing in Microsoft Exchange Server 2013 anziché Microsoft Lync Server 2013 risiede nel fatto che l'archiviazione dei dati nella stessa posizione consente agli amministratori di utilizzare un unico strumento per cercare dati archiviati in Exchange e/o Lync Server. Poiché tutti i dati sono archiviati nello stesso luogo (Exchange), qualsiasi strumento in grado di cercare i dati Exchange archiviati può cercare anche i dati archiviati di Lync Server.

Microsoft SharePoint Server 2013 semplifica la ricerca dei dati archiviati. Per cercare i dati di Lync Server tramite SharePoint, è necessario prima completare la procedura di configurazione dell'archiviazione Exchange in Lync Server. Dopo aver integrato correttamente Exchange 2013 e Lync Server 2013, è necessario installare Exchange Web Services Managed API versione 2.0 in SharePoint Server. Il programma di installazione dell'API può essere scaricato da Microsoft Download Center all'indirizzo [http://go.microsoft.com/fwlink/?linkid=258305\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=258305%26clcid=0x410). Il file scaricato, EWSManagedAPI.msi, può essere salvato in qualsiasi cartella di SharePoint Server.

Al termine del download del file, eseguire la procedura seguente in SharePoint Server:

1.  Aprire una finestra dei comandi facendo clic su **Start**, scegliere **Tutti i programmi**, **Accessori**, fare clic con il pulsante destro del mouse su **Prompt dei comandi** e quindi fare clic su **Esegui come amministratore**.

2.  Nella finestra dei comandi passare dalla directory corrente alla cartella in cui è stato salvato il file EWSManagedAPI.msi utilizzando il comando **cd**. Se, ad esempio, il file è stato salvato in C:\\Downloads, digitare il comando seguente nella finestra dei comandi, quindi premere INVIO:
    
        cd C:\Downloads

3.  Per installare l'API, digitare il comando seguente e premere INVIO:
    
        msiexec /I EwsManagedApi.msi addlocal="ExchangeWebServicesApi_Feature,ExchangeWebServicesApi_Gac"

4.  Al termine dell'installazione dell'API, riavviare IIS digitando questo comando seguito da INVIO:
    
        iisreset

Al termine dell'installazione di Servizi Web Exchange, è necessario configurare l'autenticazione server-server tra SharePoint Server 2013 ed Exchange 2013. Per eseguire l'operazione, aprire prima la shell di gestione SharePoint 2013 ed eseguire il set di comandi seguente:

    New-SPTrustedSecurityTokenIssuer -Name "Exchange" -MetadataEndPoint "https://autodiscover.litwareinc.com/autodiscover/metadata/json/1"
    $service = Get-SPSecurityTokenServiceConfig
    $service.HybridStsSelectionEnabled = $True
    $service.AllowMetadataOverHttp = $False
    $service.AllowOAuthOverHttp = $False
    $service.Update()


> [!NOTE]
> Verificare e utilizzare l'URI del servizio di individuazione automatica. Non utilizzare l'URI di esempio, https://autodiscover.litwareinc.com/autodiscover/metadata/json/1.



Dopo avere creato l'emittente di token e configurato il servizio token, eseguire questi comandi avendo cura di sostituire l'URL di esempio http://atl-sharepoint-001 con l'URL del sito SharePoint:

    $exchange = Get-SPTrustedSecurityTokenIssuer "Exchange"
    $app = Get-SPAppPrincipal -Site "https://atl-sharepoint-001" -NameIdentifier $exchange.NameID
    $site = Get-SPSite  "https://atl-sharepoint-001"
    Set-SPAppPrincipalPermission -AppPrincipal $app -Site $site.RootWeb -Scope "SiteSubscription" -Right "FullControl" -EnableAppOnlyPolicy

Per configurare l'autenticazione server-server per Exchange 2013, aprire Exchange Management Shell ed eseguire un comando simile a quello riportato di seguito, in cui si presume che Exchange sia stato installato nell'unità C: nel percorso della cartella predefinita:

    "C:\Program Files\Microsoft\Exchange Server\V15\Scripts\Configure-EnterprisePartnerApplication.ps1 -AuthMetaDataUrl 'https://atl-sharepoint-001/_layouts/15/metadata/json/1' -ApplicationType SharePoint"

Dopo aver configurato l'applicazione partner, si consiglia di arrestare e riavviare Internet Information Services (IIS) su tutti i server di cassette postali e accesso client di Exchange. Per riavviare IIS è possibile utilizzare un comando simile al seguente, che riavvia il servizio sul computer atl-exchange-001:

    iisreset atl-exchange-001

Questo comando può essere eseguito dall'interno di Exchange Management Shell oppure da una finestra dei comandi.

Eseguire quindi un comando simile al seguente per autorizzare l'utente specificato, nell'esempio kenmyer, a eseguire ricerche in Exchange:

    Add-RoleGroupMember "Discovery Management" -Member "kenmyer"

Dopo aver stabilito l'autenticazione server-server tra Exchange e SharePoint, è necessario creare un sito eDiscovery in SharePoint. Per farlo, eseguire comandi simili ai seguenti dalla shell di gestione SharePoint:

    $template = Get-SPWebTemplate | Where-Object {$_.Title -eq "eDiscovery Center"}
    New-SPSite -Url "https://atl-sharepoint-001/sites/discovery" -OwnerAlias "kenmyer" -Template $Template -Name "Discovery Center"


> [!NOTE]
> "eDiscovery" è l'abbreviazione di "individuazione elettronica" e in genere si riferisce al processo di ricerca in archivi elettronici di elementi che possano essere "considerati ragionevolmente ammissibili come prova" in un tribunale.



Quando il nuovo sito è pronto, è necessario configurare Exchange 2013 affinché funga da origine dei risultati per SharePoint. Eseguire l'operazione completando la procedura seguente nella pagina Amministrazione centrale SharePoint 2013:

1.  Nella pagina Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**, quindi su **Applicazione servizio di ricerca**.

2.  In Applicazione servizio di ricerca: nella pagina Amministrazione ricerca fare clic su **Origini di risultati** e quindi su **Nuova origine dei risultati**.

3.  Nel riquadro **Nuova origine dei risultati** specificare un nome per la nuova origine dei risultati, ad esempio **Microsoft Exchange**, nella casella **Nome**. Selezionare **Exchange** come **Protocollo** di origine dei risultati, quindi inserire l'URL di origine dei servizi Web per il server di Exchange nella casella **URL di origine di Exchange**. L'URL di origine avrà un aspetto simile al seguente:
    
    https://atl-exchange-001.litwareinc.com/ews/exchange.asmx

4.  Verificare che l'opzione **Usa individuazione automatica** non sia selezionata, quindi fare clic su **OK**.

Creare infine un nuovo caso e un nuovo set eDiscovery eseguendo questa procedura nel sito di individuazione SharePoint, ad esempio https://atl-sharepoint-001/sites/discovery:

1.  Nella pagina Contenuto del sito fare clic su **Crea un nuovo caso**.

2.  In Contenuto del sito: nella pagina Nuovo sito di SharePoint inserire l'alias di posta elettronica dell'utente, ad esempio **kenmyer**, nella casella **Titolo**, quindi aggiungere lo stesso URL nella casella **Indirizzo sito Web**. Verrà creato un URL simile a questo:
    
    https://atl-sharepoint-001/sites/eDiscovery/kenmyer

3.  Fare clic su **Crea**.

4.  Quando viene visualizzata la pagina Set eDiscovery, fare clic su **nuovo elemento** in **Identity and Preserve: Discovery Sets**.

5.  Nella pagina New: Discovery Set inserire l'alias di posta elettronica dell'utente nella casella **Discovery Set Name**. Immettere **eDiscovery Lync\*** nella casella **Filtro** e fare clic su **Aggiungi e gestisci origini**.

6.  Nella pagina Aggiungi e gestisci origini inserire l'alias di posta elettronica dell'utente nella prima casella di testo sotto **Cassette postali**. Fare clic sull'icona Controlla cassetta postale accanto alla casella di testo per verificare che SharePoint sia in grado di connettersi alla cassetta postale specificata.

7.  Fare clic su **OK**.

8.  Nella pagina Set eDiscovery fare clic su **Salva** per salvare il nuovo set eDiscovery.

È ora possibile cercare la cassetta postale specificata, kenmyer, e/o abilitare l'archiviazione sul posto analogamente a qualsiasi altra origine dei risultati o contenuto di SharePoint.

