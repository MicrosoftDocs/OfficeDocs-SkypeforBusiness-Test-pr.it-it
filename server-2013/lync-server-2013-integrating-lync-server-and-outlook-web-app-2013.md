---
title: Integrazione di Microsoft Lync Server 2013 e Microsoft Outlook Web App 2013
TOCTitle: Integrazione di Microsoft Lync Server 2013 e Microsoft Outlook Web App 2013
ms:assetid: 513d4cc7-aa87-4f68-b99d-d58b63bdf242
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688055(v=OCS.15)
ms:contentKeyID: 49887561
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Integrazione di Microsoft Lync Server 2013 e Microsoft Outlook Web App 2013

 

_**Ultima modifica dell'argomento:** 2013-02-03_

Oltre a integrarsi totalmente con Microsoft Outlook 2013, Microsoft Lync Server 2013 può integrarsi in modo completo con Microsoft Outlook Web App 2013. Tra gli altri vantaggi, questa integrazione aggiunge a Outlook Web App le funzionalità di messaggistica istantanea e presenza e consente la condivisione dell'elenco contatti unificato tra Outlook Web App e Microsoft Lync 2013. Per integrare Lync Server 2013 e Outlook Web App, è necessario prima di tutto verificare che Unified Communications Managed API 4.0 Runtime sia installato nel server back-end Microsoft Exchange Server 2013, controllando se nel Registro di sistema è presente il valore seguente:

HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\MSExchange OWA\\InstantMessaging\\ImplementationDLLPath

ImplementationDLLPath deve puntare alla cartella del file Microsoft.Rtc.Internal.Ucweb.dll. In caso contrario, o se il valore non esiste nel Registro di sistema, è necessario scaricare ed eseguire il programma di installazione di UCMA Runtime dall'Area download Microsoft all'indirizzo <http://www.microsoft.com/it-it/download/details.aspx?id=34992>. Nella stessa pagina Web sono disponibili anche informazioni su come installare UCMA Runtime.

**Compatibilità con le versioni precedenti**

È possibile integrare Lync Server 2013 con le versioni per Microsoft Exchange Server 2010 sia della messaggistica unificata che di Outlook Web App. Per ulteriori informazioni, vedere l'articolo "Distribuzione della messaggistica unificata di Exchange in locale per fornire la funzionalità di segreteria telefonica di Lync Server 2010" all'indirizzo [http://technet.microsoft.com/it-it/library/gg398768.aspx](lync-server-2013-deploying-on-premises-exchange-um-to-provide-lync-server-2013-voice-mail.md). In caso di integrazione con Exchange 2010 non saranno disponibili funzionalità specifiche di Lync Server, come l'archivio contatti unificato e l'archiviazione da Lync a Exchange.

È inoltre possibile utilizzare Microsoft Lync 2013 insieme a Exchange 2010 e Outlook 2010. Anche in questo caso, tuttavia, le nuove funzionalità come l'archivio contatti unificato e le foto ad alta risoluzione non saranno disponibili per gli utenti di Lync 2013. Per queste nuove funzionalità sono necessari sia Lync Server 2013 che Exchange 2013.

**Creazione di un pool di applicazioni attendibili per Outlook Web App**

Se si installano il servizio di routing delle chiamate di messaggistica unificata di Microsoft Exchange e il servizio Messaggistica unificata di Microsoft Exchange nello stesso computer non è necessario creare un pool di applicazioni attendibili per Outlook Web App (ciò presuppone che il server in questione ospiti un dial plan di messaggistica unificata SipName). Se si utilizza un singolo computer per ospitare entrambi questi servizi, è possibile passare alla sezione del documento intitolata **Abilitazione della messaggistica istantanea in Outlook Web App**.

Lync Server 2013 supporta l'individuazione automatica di qualsiasi server Exchange che ospiti un dial plan di messaggistica unificata SipName. Questi server vengono aggiunti automaticamente all'elenco dei server noti di Lync Server. Non è necessario creare un pool di applicazioni attendibili e aggiungere questi server all'elenco dei server noti. Ciò impedirebbe in effetti il funzionamento dell'integrazione di Outlook Web App.


> [!NOTE]
> La causa è il fatto che la topologia di Lync Server includerebbe due voci per lo stesso computer, ovvero la voce individuata automaticamente e quella aggiunta manualmente. Per risolvere il problema e ripristinare il funzionamento di Outlook Web App, utilizzare Windows PowerShell per rimuovere le voci del pool attendibile e dell'applicazione attendibile per il server. Per ulteriori informazioni, vedere gli argomenti della Guida per i cmdlet <A href="remove-cstrustedapplicationpool.md">Remove-CsTrustedApplicationPool</A> e <A href="remove-cstrustedapplication.md">Remove-CsTrustedApplication</A>.



Se i due servizi sono eseguiti in computer separati, dopo aver verificato che Unified Communications Managed API 4.0 Runtime sia installato, è necessario creare un pool di applicazioni attendibili Lync Server e un'applicazione attendibile associati a Outlook Web App. In questo modo il server verrà aggiunto all'elenco dei server noti. A tale scopo, da Lync Server Management Shell eseguire prima di tutto un comando simile a questo:

    New-CsTrustedApplicationPool -Identity atl-owa-001.litwareinc.com -Registrar atl-cs-001.litwareinc.com -Site Redmond -RequiresReplication $False

Nel comando precedente, atl-owa-001.litwareinc.com è il nome di dominio completo del pool Outlook Web App e deve corrispondere al nome che compare nei campi Nome soggetto e Nome alternativo del certificato che consente l'accesso ad Outlook Web App. Analogamente, atl-cs-001.litwareinc.com è il nome di dominio completo del pool Lync Server 2013 che ospiterà il nuovo pool di applicazioni attendibili. Si noti inoltre che il sito specificato, Redmond, rappresenta il SiteID del sito Lync Server. Il SiteID non è necessariamente uguale al DisplayName del sito. È possibile recuperare i SiteID dei siti Lync Server eseguendo il comando seguente da Lync Server Management Shell:

    Get-CsSite | Select-Object DisplayName, SiteID

Dopo aver creato il pool di applicazioni attendibili, utilizzare un comando simile al seguente per configurare l'identità di un'applicazione e la porta per Outlook Web App:

    New-CsTrustedApplication -ApplicationId OutlookWebApp -TrustedApplicationPoolFqdn atl-owa-001.litwareinc.com  -Port 5199

Nel comando precedente, ApplicationID è un identificatore descrittivo usato per distinguere le applicazioni attendibili. Come ApplicationID si può usare qualsiasi stringa di testo che non comprenda spazi o altri caratteri non consentiti. Per creare un identificatore valido, assicurarsi di usare solo lettere e numeri. Anche il valore assegnato al parametro Port è a discrezione dell'amministratore e può corrispondere a qualsiasi porta di rete disponibile.

Dopo aver creato l'applicazione attendibile, per abilitare le modifiche alla topologia Lync Server è necessario eseguire il comando seguente:

    Enable-CsTopology

Si noti che è inoltre necessario aggiungere il server di accesso client e delle cassette postali di Exchange a tutti i dial plan URI SIP. Ciò consentirà a sua volta di configurare i server come peer SIP attendibili con la topologia ExUmRouting per Lync Server.

**Abilitazione della messaggistica istantanea in Outlook Web App**

Ora che Lync Server è stato configurato correttamente è possibile passare alla configurazione di Outlook Web App. Il primo passaggio di questo processo è l'abilitazione della messaggistica istantanea in tutte le directory virtuali di Outlook Web App nei server front-end. Non è necessario abilitare la messaggistica istantanea per le directory virtuali nei server back-end ed in effetti è consigliabile non abilitarla. La messaggistica istantanea può essere abilitata nei server di accesso client eseguendo il comando seguente da Exchange Management Shell:

    Get-OwaVirtualDirectory | Set-OwaVirtualDirectory -InstantMessagingEnabled $True -InstantMessagingType OCS


> [!NOTE]
> Per impostazione predefinita, la messaggistica istantanea è abilitata quando si installa Outlook Web App, ovvero la proprietà InstantMessagingEnabled è impostata su True. È comunque necessario eseguire il comando precedente per impostare il tipo di messaggistica istantanea su OCS. Per impostazione predefinita, InstantMessagingType è impostato su None.



Subito dopo è necessario aggiungere le due righe seguenti al file Web.config di Outlook Web App, che in genere si trova nella cartella C:\\Programmi\\Microsoft\\Exchange Server\\V15\\ClientAccess\\Owa. Queste due righe devono essere aggiunte nel nodo \<AppSettings\> nel file Web.config e la procedura deve essere eseguita solo nei server back-end in cui si installa Outlook Web App:

    <add key="IMCertificateThumbprint" value="EA5A332496CC05DA69B75B66111C0F78A110D22d"/>
    <add key="IMServerName" value="atl-cs-001.litwareinc.com"/>

Nell'esempio precedente, il valore di IMCertificateThumbprint deve essere l'identificazione digitale del certificato di Exchange 2013 installato nei server back-end. Per recuperare questa informazione, eseguire il comando seguente da Exchange Management Shell:

    Get-ExchangeCertificate

Si noti inoltre che il valore assegnato a IMServerName è il nome di dominio completo del pool Lync Server in cui è stato creato il pool di applicazioni attendibili per Outlook Web App.

Il certificato utilizzato per Outlook Web App deve essere considerato attendibile da Lync Server. Un modo per assicurarsi che il certificato venga considerato attendibile sia da Lync Server che da Exchange consiste nell'utilizzare l'Autorità di certificazione interna per creare un certificato nel server delle cassette postali, assicurandosi che il nome di dominio completo del server venga utilizzato per il nome soggetto e che questo FQDN compaia nel campo nel nome alternativo del certificato. Dopo aver creato il certificato sarà possibile importarlo nei server back-end. Il risultato finale è che lo stesso certificato viene utilizzato per due scopi: 1) le comunicazioni tra la messaggistica unificata di Exchange e Lync Server e 2) l'integrazione tra Outlook Web App e Lync Server.

Dopo aver aggiornato il file Web.config, è necessario eseguire il comando seguente nel server back-end di Exchange per riciclare il pool Outlook Web App:

    C:\Windows\System32\Inetsrv\Appcmd.exe recycle apppool /apppool.name:"MSExchangeOWAAppPool"

Se l'operazione di riciclo riesce, in Exchange Management Shell sarà visibile il messaggio seguente:

    "MSExchangeOWAAppPool" successfully recycled

**Configurazione dei criteri delle cassette postali di Outlook Web App**

A questo punto è possibile utilizzar il comando seguente per configurare la messaggistica istantanea nei criteri delle cassette postali di Outlook Web App appropriati. Ad esempio, questo comando, eseguito in uno dei server delle cassette postali, consente di abilitare la messaggistica istantanea per i criteri Default:

    Set-OwaMailboxPolicy -Identity "Default" -InstantMessagingEnabled $True -InstantMessagingType "OCS"

E questo comando abilita la messaggistica istantanea per tutti i criteri delle cassette postali di Outlook Web App:

    Get-OwaMailboxPolicy | Set-OwaMailboxPolicy -InstantMessagingEnabled $True -InstantMessagingType "OCS"

Dopo l'abilitazione dei criteri delle cassette postali, tutti gli utenti gestiti da questi criteri possono usufruire dell'integrazione completa tra Lync Server e Outlook Web App, a condizione che:

  - Abbiano una cassetta postale in Exchange 2013.

  - Siano stati abilitati per Lync Server 2013.

  - Dispongano di un indirizzo proxy SIP.

**Disabilitazione della messaggistica istantanea in Outlook Web App**

Come indicato in precedenza, la messaggistica istantanea è abilitata per impostazione predefinita in Outlook Web App. Ciò significa che se non si integra Outlook Web App con Lync Server, gli utenti vedranno icone presenza vuote e un messaggio di errore a ogni accesso a Outlook Web App. Per evitare questo problema, utilizzare il comando seguente di Exchange Management Shell per disabilitare la messaggistica istantanea in Outlook web App:

    Get-OwaVirtualDirectory | Set-OwaVirtualDirectory -InstantMessagingEnabled $False

**Verifica dell'integrazione con Outlook Web App**

Per verificare che la messaggistica istantanea e la presenza siano integrate con Outlook Web App, accedere a Outlook Web App 2013. Nell'angolo in alto a destra dello schermo è visibile il proprio nome visualizzato Exchange. Se accanto al proprio nome compare un'icona presenza, ad esempio un'icona verde che indica che lo stato corrente è Disponibile, ciò significa che l'integrazione di Lync Server e Outlook Web App è stata eseguita correttamente.

Dopo l'accesso iniziale a Outlook Web App, controllare se è stato scritto un evento con ID 112 (e origine MSExchange OWA) nel registro eventi nel server delle cassette postali. Questo evento indica la corretta inizializzazione di Gestione endpoint di Messaggistica istantanea. Se la messaggistica istantanea risulta non funzionante, nel server delle cassette postali cercare i file di log nella cartella C:\\Programmi\\Microsoft\\Exchange server\\V15\\Logging\\OWA\\InstantMessaging. Se le cartelle Logging o InstantMessaging non esistono, ciò indica che l'integrazione non è riuscita. In questo caso, è possibile utilizzare la traccia SIPStack in Lync Server (tutti i livelli e tutti i flag) per provare a scoprire i motivi.

