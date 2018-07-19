---
title: Configurazione dei provider per il servizio di registrazione centralizzato
TOCTitle: Configurazione dei provider per il servizio di registrazione centralizzato
ms:assetid: 6a197ecf-b56b-45e0-8e7c-f532ec5164ff
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688082(v=OCS.15)
ms:contentKeyID: 49887594
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione dei provider per il servizio di registrazione centralizzato

 

_**Ultima modifica dell'argomento:** 2014-03-19_

I concetti e la configurazione dei *provider* in servizio di registrazione centralizzato sono uno degli argomenti più importanti da comprendere appieno. Tra i *provider* e i componenti del ruolo server Lync Server esistono corrispondenze dirette nel modello di traccia di Lync Server. Il provider definisce i componenti di Lync Server 2013 che verranno inclusi nella traccia, il tipo di messaggi da raccogliere (ad esempio, errori irreversibili, errori o avvisi) e i flag (ad esempio, TF\_Connection o TF\_Diag). I provider sono i componenti tracciabili in ogni ruolo server di Lync Server. Tramite i provider vengono definiti il livello e il tipo di traccia per i componenti (ad esempio, S4, SIPStack, messaggistica istantanea e presenza). Il provider definito viene utilizzato in uno scenario per raggruppare tutti i provider per una determinata raccolta logica riferita a una condizione problematica specifica.

Per eseguire le funzioni del servizio di registrazione centralizzato tramite Lync Server Management Shell, è necessario essere membri dei gruppi di sicurezza per il controllo di accesso basato sui ruoli (RBAC) CsAdministrator o CsServerAdministrator oppure di un ruolo RBAC personalizzato che contenga uno di questi due gruppi. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli a cui è stato assegnato il cmdlet, inclusi eventuali ruoli RBAC personalizzati, eseguire il comando seguente da Lync Server Management Shell o dal prompt Windows PowerShell:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Lync Server 2013 cmdlet"}

Ad esempio:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Set-CsClsConfiguration"}

Le informazioni nel resto dell'argomento sono incentrate su come definire i provider, modificare un provider e il contenuto della definizione di un provider per ottimizzare la risoluzione dei problemi. Esistono due modi per eseguire i comandi del servizio di registrazione centralizzato. È possibile utilizzare CLSController.exe, disponibile per impostazione predefinita nella directory C:\\Programmi\\Common Files\\Microsoft Lync Server 2013\\CLSAgent oppure utilizzare Lync Server Management Shell per eseguire comandi Windows PowerShell. È importante tenere presente che quando si utilizza CLSController.exe al prompt dei comandi esiste una scelta limitata di scenari disponibili, nei quali i provider sono già definiti e non sono modificabili, ma è possibile definire il livello di registrazione. Quando si utilizza Windows PowerShell, invece, è possibile definire nuovi provider per l'utilizzo nelle sessioni di registrazione e disporre del controllo completo sulla loro creazione, sui dati raccolti e sul livello di raccolta dei dati.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Come già accennato, i provider sono uno strumento dalle grandi potenzialità. Gli scenari, tuttavia, sono ancora più efficaci perché incorporano tutte le informazioni necessarie per impostare ed eseguire la traccia sui componenti rappresentati dai provider. Dato che gli scenari sono in effetti una raccolta di provider, possono essere paragonati all'esecuzione di un file batch contenente centinaia di comandi per raccogliere grandi quantità di informazioni anziché eseguire centinaia di comandi, uno alla volta, dalla riga di comando.<br />
Per evitare di dover approfondire nei dettagli il funzionamento dei provider, il servizio di registrazione centralizzato include numerosi scenari già definiti, appropriati per la stragrande maggioranza dei possibili problemi che possono verificarsi. In rari casi potrebbe risultare necessario creare e definire provider e assegnarli a scenari. È consigliabile imparare a conoscere nei dettagli ogni scenario disponibile, prima di affrontare la creazione di nuovi provider e scenari. Sebbene in questo argomento siano disponibili informazioni sulla creazione dei provider per capire come gli scenari utilizzino gli elementi dei provider per raccogliere informazioni di traccia, non sono fornite informazioni dettagliate sui provider stessi.</td>
</tr>
</tbody>
</table>


Come indicato nelle informazioni introduttive in [Panoramica del servizio di registrazione centralizzato](lync-server-2013-overview-of-the-centralized-logging-service.md), gli elementi principali per la definizione di un provider per l'utilizzo in uno scenario sono:

  - **Provider**   Per gli utenti che hanno familiarità con OCSLogger, i provider sono i componenti che vengono scelti per indicare a OCSLogger l'origine da cui il motore di traccia deve raccogliere i log. I provider sono gli stessi componenti e in molti casi hanno lo stesso nome dei componenti in OCSLogger. Se non si conosce OCSLogger, i provider sono componenti specifici del ruolo del server da cui il servizio di registrazione centralizzato può raccogliere i log. Nel caso del servizio di registrazione centralizzato, CLSAgent è la parte architetturale del servizio di registrazione centralizzato che esegue la traccia dei componenti definiti nella configurazione dei provider.

  - **Livelli di registrazione**   In OCSLogger è possibile scegliere il numero di livelli di dettaglio per i dati raccolti. Questa funzionalità è un elemento cruciale del servizio di registrazione centralizzato e degli scenari e viene definita dal parametro **Type**. È possibile scegliere tra i valori seguenti:
    
      - **All**   Raccoglie i messaggi di traccia di tipo errore irreversibile, errore, avviso e informazioni nel log per il provider definito.
    
      - **Fatal**   Raccoglie solo i messaggi di traccia che indicano un errore irreversibile per il provider definito.
    
      - **Error**   Raccoglie solo i messaggi di traccia che indicano un errore per il provider definito, oltre ai messaggi per errori irreversibili.
    
      - **Warning**   Raccoglie solo i messaggi di traccia che indicano un avviso per il provider definito, oltre ai messaggi per errori irreversibili ed errori.
    
      - **Info**   Raccoglie solo i messaggi di traccia che indicano un messaggio informativo per il provider definito, oltre ai messaggi per errori irreversibili, errori e avvisi.
    
      - **Verbose**   Raccoglie tutti i messaggi di traccia per errori irreversibili, errori, avvisi e informazioni per il provider definito.

  - **Flags**   OCSLogger consente di scegliere i flag per ogni provider che definiscono il tipo di informazioni recuperabili dai file di traccia. È possibile scegliere tra i flag seguenti, in base al provider:
    
      - **TF\_Connection**   Voci di log correlate alla connessione. Questi log includono informazioni sulle connessioni stabilite con e da un particolare componente. Potrebbero essere anche incluse informazioni significative a livello di rete, ovvero per componenti non correlati al concetto di connessione.
    
      - **TF\_Security**   Tutti gli eventi e le voci di log correlati alla sicurezza. Per SipStack, ad esempio, si tratta degli eventi di sicurezza come errori di convalida del dominio ed errori di autenticazione/autorizzazione dei client.
    
      - **TF\_Diag**   Eventi diagnostici utilizzabili per la diagnosi o la risoluzione dei problemi relativi al componente. Per SipStack, ad esempio, si tratta di errori dei certificati oppure di avvisi/errori DNS.
    
      - **TF\_Protocol**   Messaggi di protocollo, come i messaggi SIP e CCCP.
    
      - **TF\_Component**   Abilita la registrazione per i componenti specificati nell'ambito del provider.
    
      - **All**   Imposta tutti i flag disponibili per il provider.

## Per visualizzare le informazioni sui provider di scenari del servizio di registrazione centralizzato esistenti

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Per esaminare la configurazione dei provider esistenti, digitare il comando seguente:
    
        Get-CsClsScenario -Identity <scope and scenario name>
    
    Per visualizzare informazioni sull'operatore conferenza globale, ad esempio, digitare:
    
        Get-CsClsScenario -Identity "global/CAA"
    
    Il comando visualizza un elenco dei provider con i flag, le impostazioni e i componenti associati. Se le informazioni visualizzate non sono sufficienti o l'elenco è troppo lungo per il formato di elenco predefinito di Windows PowerShell, è possibile visualizzare informazioni aggiuntive definendo un metodo di output diverso. A tale scopo, digitare:
    
        Get-CsClsScenario -Identity "global/CAA" | Select-Object -ExpandProperty Provider
    
    Nell'output di questo comando, le informazioni su ogni provider sono visualizzate su cinque righe separate che includono nome del provider, tipo di registrazione, livello di registrazione, flag, GUID e ruolo.

## Per definire un nuovo provider di scenari del servizio di registrazione centralizzato

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Un provider di scenari è costituito dal componente da tracciare, i flag da utilizzare e il livello di dettaglio per la raccolta dei dati. Per definire questi elementi, digitare:
    
        $<variableName> = New-CsClsProvider -Name <provider component> -Type <log type> -Level <log level detail type> -Flags <provider trace log flags>
    
    La definizione di un provider di traccia per specificare quali dati raccogliere e con quale livello di dettaglio dal provider Lyss, ad esempio, è simile alla seguente:
    
        $LyssProvider = New-CsClsProvider -Name "Lyss" -Type "WPP" -Level "Info" -Flags "All"

Il parametro -Level consente di specificare se raccogliere i messaggi relativi a errori irreversibili, errori, avvisi e informazioni. I flag utilizzati sono tutti quelli definiti per il provider Lyss e includono TF\_Connection, TF\_Diag e TF\_Protocol.

Dopo aver definito la variabile $LyssProvider è possibile utilizzarla con il cmdlet **New-CsClsScenario** per raccogliere le tracce dal provider Lyss. Per completare la creazione e l'assegnazione del provider a un nuovo scenario, digitare:

    New-CsClsScenario -Identity "site:Redmond/RedmondLyssInfo" -Provider $LyssProvider

Dove $LyssProvider è la variabile che contiene lo scenario definito creato con **New-CsClsProvider**.

## Per modificare un provider di scenari del servizio di registrazione centralizzato esistente

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Per aggiornare o modificare la configurazione di un provider esistente, digitare:
    
        $LyssProvider = New-CsClsProvider -Name "Lyss" -Type "WPP" -Level "Debug" -Flags "TF_Connection, TF_Diag"
    
    Aggiornare quindi lo scenario per assegnare il provider digitando il comando seguente:
    
        Set-CsClsScenario -Identity "site:Redmond/RedmondLyssInfo" -Provider $LyssProvider

Il risultato finale del comando è l'aggiornamento dei flag per lo scenario site:Redmond/RedmondLyssInfo e l'assegnazione del livello per il provider. Per visualizzare il nuovo scenario, utilizzare Get-CsClsScenario. Per informazioni dettagliate, vedere [Get-CsClsScenario](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsClsScenario).


> [!WARNING]
> <STRONG>New-ClsCsProvider</STRONG> non esegue un controllo per stabilire se i flag sono validi. Assicurarsi di digitare correttamente i flag, ad esempio TF_DIAG o TF_CONNECTION. Se il nome dei flag non è corretto, il provider non potrà restituire le informazioni di log previste.



Se si desidera aggiungere ulteriori provider a questo scenario, digitare il comando seguente:

    Set-CsClsScenario -Identity "site:Redmond/RedmondLyssInfo" -Provider @{Add=$ABSProvider, $CASProvider, S4Provider}

In cui ogni provider definito con la direttiva Add è già stato definito tramite il processo **New-CsClsProvider**.

## Per rimuovere un provider di scenari

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  I cmdlet indicati consentono di aggiornare i provider esistenti e di crearne di nuovi. Per rimuovere un provider, è necessario utilizzare la direttiva Replace per il parametro Provider in **Set-CsClsScenario**. L'unico modo per rimuovere completamente un provider consiste nel sostituirlo con un provider ridefinito con lo stesso nome e poi utilizzare la direttiva Update. Il provider LyssProvider utilizzato negli esempi precedenti, ad esempio, è definito con il tipo di log WPP, il livello di registrazione Debug e i flag TF\_CONNECTION e TF\_DIAG. Supponendo di dover modificare i flag e impostare "All". per modificare il provider digitare il comando seguente:
    
        $LyssProvider = New-CsClsProvider -Name "Lyss" -Type "WPP" -Level "Debug" -Flags "All"
    
        Set-CsClsScenario -Identity "site:Redmond/RedmondLyssInfo" -Provider @{Replace=$LyssProvider}

3.  Se si desidera rimuovere completamente uno scenario e i provider associati, digitare il comando seguente:
    
        Remove-CsClsScenario -Identity <scope and name of scenario>
    
    Ad esempio:
    
        Remove-CsClsScenario -Identity "site:Redmond/RedmondLyssInfo"
    

    > [!WARNING]
    > Il cmdlet <STRONG>Remove-CsClsScenario</STRONG> non richiede alcuna conferma. Lo scenario viene eliminato insieme ai provider assegnati. È possibile ricreare lo scenario rieseguendo i comandi utilizzati inizialmente per crearlo. Non esiste una procedura per il ripristino di scenari o provider rimossi.



Quando si rimuove uno scenario tramite il cmdlet **Remove-CsClsScenario**, si rimuove completamente lo scenario dall'ambito. Per utilizzare gli scenari creati e i provider che facevano parte dello scenario, creare nuovi provider e assegnarli a un nuovo scenario.

## Vedere anche

#### Ulteriori risorse

[Get-CsClsScenario](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsClsScenario)  
[New-CsClsScenario](new-csclsscenario.md)  
[Remove-CsClsScenario](remove-csclsscenario.md)  
[Set-CsClsScenario](set-csclsscenario.md)  
[New-CsClsProvider](new-csclsprovider.md)

