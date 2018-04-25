---
title: Configurazione degli scenari per il servizio di registrazione centralizzato
TOCTitle: Configurazione degli scenari per il servizio di registrazione centralizzato
ms:assetid: 6c3bf826-e7fd-4002-95dc-01020641ef01
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688085(v=OCS.15)
ms:contentKeyID: 49887599
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione degli scenari per il servizio di registrazione centralizzato

 

_**Ultima modifica dell'argomento:** 2014-02-05_

Gli scenari definiscono l'ambito (globale, sito, pool o computer) e i provider da utilizzare nel servizio di servizio di registrazione centralizzato. Attraverso gli scenari si attivano o disattivano le tracce per i provider (ad esempio, S4, SIPStack, messaggistica immediata e presenza). Attraverso la configurazione di uno scenario, è possibile raggruppare tutti i provider per una data raccolta logica relativa a un problema specifico. Se si ha bisogno di modificare uno scenario per adattarlo alle proprie esigenze di risoluzione dei problemi e registrazione, gli strumenti di debug di Lync Server 2013 forniscono un modulo di Windows PowerShell chiamato *ClsController.psm1*, che contiene una funzione chiamata *Edit-CsClsScenario*. Il modulo consente di modificare le proprietà dello scenario. In questo argomento sono forniti esempi di funzionamento del modulo. È possibile scaricare gli strumenti di debug di Lync Server 2013 al seguente indirizzo: [http://go.microsoft.com/fwlink/?LinkId=285257](http://go.microsoft.com/fwlink/?linkid=285257).

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Per un determinato ambito (sito, globale, pool o computer), è possibile eseguire un massimo di due scenari alla volta. Per determinare quali scenari sono in esecuzione, utilizzare Windows PowerShell e <a href="get-csclsscenario.md">Get-CsClsScenario</a>. Con Windows PowerShell e <a href="set-csclsscenario.md">Set-CsClsScenario</a> è possibile modificare dinamicamente gli scenari in esecuzione. È possibile modificare gli scenari durante una sessione di registrazione, al fine di regolare o rifinire i dati che vengono raccolti, nonché i provider.</td>
</tr>
</tbody>
</table>


Per eseguire le funzioni di servizio di registrazione centralizzato utilizzando Lync Server Management Shell, è necessario essere membri dei gruppi di sicurezza RBAC CsAdministrator o CsServerAdministrator, o avere un ruolo RBAC personalizzato, contenente uno dei due gruppi. Per restituire un elenco di tutti i ruoli RBAC ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Lync Server Management Shell o Windows PowerShell:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Lync Server 2013 cmdlet"}

Ad esempio:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Set-CsClsConfiguration"}

Questo argomento si concentra sulle modalità di definizione di uno scenario, modifica di uno scenario, recupero degli scenari in esecuzione, rimozione di uno scenario e specificazione del contenuto di uno scenario, per l'ottimizzazione della risoluzione dei problemi. Esistono due modalità di emissione dei comandi di servizio di registrazione centralizzato. È possibile utilizzare CLSController.exe che si trova, per impostazione predefinita, nella cartella C:\\Program Files\\Common Files\\Microsoft Lync Server 2013\\CLSAgent. Alternativamente, è possibile utilizzare Lync Server Management Shell per l'emissione dei comandi di Windows PowerShell. Quando si utilizza CLSController.exe, nella riga di comando esiste una selezione di scenari disponibili finita. Quando si utilizza Windows PowerShell, è possibile definire nuovi scenari da utilizzare nelle sessioni di registrazione.

Come anticipato in [Panoramica del servizio di registrazione centralizzato](lync-server-2013-overview-of-the-centralized-logging-service.md), gli elementi di uno scenario sono:

  - **Provider**   Se si ha famigliarità con OCSLogger, i provider sono i componenti che si sceglie per informare OCSLogger in relazione al modulo di traccia dal quale raccogliere i registri. I provider sono gli stessi componenti, e in molti casi ne condividono anche il nome, dei componenti in OCSLogger. Se non si ha famigliarità con OCSLogger, i provider sono componenti specifici del ruolo del server dal quale servizio di registrazione centralizzato può raccogliere registri. Per dettagli sulla configurazione dei provider, vedere [Configurazione dei provider per il servizio di registrazione centralizzato](lync-server-2013-configuring-providers-for-centralized-logging-service.md).

  - **Identity**   Il parametro –Identity imposta l'ambito e il nome dello scenario. Ad esempio, è possibile impostare un ambito “globale” e identificare lo scenario con “LyssServiceScenario”. Quando si combinano le due cose, si definisce il parametro Identity (ad esempio, “global/LyssServiceScenario”).
    
    Facoltativamente è possibile utilizzare i parametri –Name and –Parent. Il parametro Name identifica lo scenario in maniera univoca. Se si utilizza il parametro Name, è necessario utilizzare anche il parametro Parent per aggiungere lo scenario all'ambito globale o sito.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Se si utilizzano i parametri Name e Parent, non è possibile utilizzare il parametro <strong>–Identity</strong>.</td>
    </tr>
    </tbody>
    </table>


## Per creare un nuovo scenario con il cmdlet New-CsClsScenario

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Per creare un nuovo scenario per una sessione di registrazione, utilizzare [New-CsClsProvider](new-csclsprovider.md) e definire il nome dello scenario (ovvero, un'identificazione univoca). Scegliere un tipo di formato di registrazione da WPP (ovvero, Windows software trace preprocessor e predefinito), EventLog (ovvero, il formato del registro eventi di Windows) o IISLog (ovvero, il file formato ASCII basato sul formato dei file di registro IIS). Definire quindi il livello (Secondo la definizione dei livelli di registrazione in questo argomento) e i contrassergni (secondo la definizione dei contrassegni in questo argomento).
    
    In questo scenario di esempio, utilizzeremo LyssProvider come provider variabile di esempio.
    
    Per creare uno scenario utilizzando le opzioni definite, digitare:
    
        New-CsClsScenario -Identity <scope>/<unique scenario name> -Provider <provider variable>
    
    Ad esempio:
    
        New-CsClsScenario -Identity "site:Redmond/LyssServiceScenario" -Provider $LyssProvider
    
    Il formato alternativo, –Name e –Parent:
    
        New-CsClsScenario -Name "LyssServiceScenario" -Parent "site:Redmond" -Provider $LyssProvider

## Per creare un nuovo scenario con provider multipli con il cmdlet New-CsClsScenario

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Esiste un limite di due scenari per ambito. Non esiste, tuttavia, un limite fisso di provider. In questo esempio, si supponga di aver creato tre provider, e di volerli assegnare tutti a uno scenario che si sta definendo. I nomi variabili dei provider sono LyssProvider, ABServerProvider e SIPStackProvider. Per definire e assegnare provider multipli a uno scenario, digitare quanto segue nel prompt dei comandi di Lync Server Management Shell o Windows PowerShell:
    
        New-CsClsScenario -Identity "site:Redmond/CollectDataScenario" -Provider @{Add=$LyssProvider, $ABServerProvider,  $SIPStackProvider}
    

    > [!NOTE]
    > Come è noto in Windows PowerShell, la convenzione per la creazione di una tabella di hash di valori utilizzando <CODE>@{&lt;variable&gt;=&lt;value1&gt;, &lt;value2&gt;, &lt;value&gt;...}</CODE> è nota come <EM>splatting</EM>. Per informazioni dettagliate sullo splatting in Windows PowerShell, vedere <A class=uri href="http://go.microsoft.com/fwlink/?linkid=267760%26clcid=0x410">http://go.microsoft.com/fwlink/?linkid=267760&amp;clcid=0x410</A>.



## Per modificare uno scenario esistente tramite il cmdlet Set-CsClsScenario

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Esiste un limite di due scenari per ambito. È possibile cambiare in qualunque momento lo scenario eseguito, anche quando è in esecuzione una sessione di raccolta di registri. Se si definisce nuovamente lo scenario in esecuzione, la sessione di raccolta smetterà di utilizzare lo scenario rimosso, e inizierà ad utilizzare il nuovo scenario. Tuttavia, le informazioni raccolte con lo scenario rimosso rimarranno nei registri. Per definire un nuovo scenario, eseguire le operazioni seguenti (supponiamo che è stato aggiunto un nome di provider già definito, chiamato “S4Provider”):
    
        Set-CsClsScenario -Identity <name of scope and scenario defined by New-CsClsScenario> -Provider @{Add=<new provider to add>}
    
    Ad esempio:
    
        Set-CsClsScenario -Identity "site:Redmond/LyssServiceScenario" -Provider @{Add=$S4Provider}
    
    Per sostituire un provider, definire un provider singolo o un elenco di provider separati da virgola a sostituzione dell'insieme esistente. Se si desidera sostituire uno dei molti provider, aggiungere i nuovi provider a quelli esistenti, per creare un insieme di provider contenente sia i provider esistenti che quelli nuovi. Per sostituire tutti i provider con un nuovo insieme, digitare:
    
        Set-CsClsScenario -Identity <name of scope and scenario defined by New-CsClsScenario> -Provider @{Replace=<providers to replace existing provider set>}
    
    Ad esempio, per sostituire l'insieme esistente di $LyssProvider, $ABServerProvider e $SIPStackProvider con $LyssServiceProvider:
    
        Set-CsClsScenario -Identity "site:Redmond/LyssServiceScenario" -Provider @{Replace=$LyssServiceProvider}
    
    Per sostituire soltanto il provider $LyssProvider dall'insieme corrente di $LyssProvider, $ABServerProvider e $SIPStackProvider con $LyssServiceProvider, digitare:
    
        Set-CsClsScenario -Identity "site:Redmond/LyssServiceScenario" -Provider @{Replace=$LyssServiceProvider, $ABServerProvider, $SIPStackProvider}

## Per rimuovere uno scenario esistente tramite il cmdlet Remove-CsClsScenario

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Per rimuovere uno scenario precedentemente definito, digitare:
    
        Remove-CsClsScenario -Identity <name of scope and scenario>
    
    Ad esempio, per rimuovere lo scenario definito:Redmond/LyssServiceScenario:
    
        Remove-CsClsScenario -Identity "site:Redmond/LyssServiceScenario"

Il cmdlet **Remove-CsClsScenario** rimuove lo scenario specificato, ma le tracce acquisite restano disponibili nei registri per la ricerca.

## Per caricare e scaricare il cmdlet Edit-CsClsScenario attraverso il modulo ClsController.psm1

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Il modulo ClsController.psm1 è fornito come download Web separato. Il modulo fa parte degli strumenti di debug di Lync Server 2013. Per impostazione predefinita, gli strumenti di debug sono installati nella cartella C:\Program Files\Lync Server 2013\Debugging Tools.</td>
    </tr>
    </tbody>
    </table>


2.  In Windows PowerShell digitare:
    
        Import-Module "C:\Program Files\Lync Server 2013\Debugging Tools\ClsController.psm1"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Se il modulo è caricato correttamente, si tornerà al prompt dei comandi di Windows PowerShell. Per confermare che il modulo è caricato e che Edit-CsClsScenario è disponibile, digitare <code>Get-Help Edit-CsClsScenario</code>. Dovrebbe essere visualizzato un riepilogo di base della sintassi per EditCsClsScenario.</td>
    </tr>
    </tbody>
    </table>


3.  Per scaricare i moduli, digitare:
    
        Remove-Module ClsController
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Se il modulo viene scaricato con successo, si torna al prompt dei comandi di Windows PowerShell. Per confermare che il modulo è stato scaricato, digitare <code>Get-Help Edit-CsClsScenario</code>. Windows PowerShell tenterà di localizzare la guida del cmdlet.</td>
    </tr>
    </tbody>
    </table>


## Per rimuovere un provider esistente da uno scenario attraverso il modulo Edit-ClsController

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Per rimuovere un provider dallo scenario AlwaysOn, digitare:
    
        Edit-CsClsScenario -ScenarioName <string of the scenario to edit> -ProviderName <string of the provider to remove> -Remove
    
    Ad esempio:
    
        Edit-CsClsScenario -ScenarioName AlwaysOn -ProviderName ChatServer -Remove
    
    I parametri ScenarioName e ProviderName sono parametri relativi alla posizione, ovvero devono essere definiti nella posizione della riga di comando attesa. Il nome del parametro non deve essere definito esplicitamente se il nome dello scenario si trova in posizione due e il provider in posizione tre, in relazione al nome del cmdlet in posizione uno. Attraverso queste informazioni, il comando precedente verrebbe digitato come:
    
        Edit-CsClsScenario AlwaysOn ChatServer -Remove
    
    Questo tipo di posizionamento del valore del parametro si applica soltanto ai parametri –Scenario e –Provider. Tutti gli altri parametri devono essere definiti esplicitamente.

## Per aggiungere un provider esistente a uno scenario attraverso il modulo Edit-ClsController

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Per aggiungere un provider allo scenario AlwaysOn, digitare:
    
        Edit-CsClsScenario -ScenarioName <string of the scenario to edit> -ProviderName <string of the provider to add> -Level <string of type level> -Flags <string of type flags>
    
    Ad esempio:
    
        Edit-CsClsScenario -ScenarioName AlwaysOn -ProviderName ChatServer -Level Info -Flags TF_COMPONENT
    
    \-Loglevel può essere di tipo Fatal, Error, Warning, Info, Verbose, Debug o All. –I contrassegni possono essere tutti quelli supportati dal provider, come TF\_COMPONENT, TF\_DIAG. –Il valore dei contrassegni, inoltre, può essere ALL
    
    L'esempio precedente può essere digitato anche attraverso la caratteristiche di posizione del cmdlet. Ad esempio, per aggiungere il provider ChatServer allo scenario AlwaysOn, digitare:
    
        Edit-CsClsScenario AlwaysOn ChatServer -Level Info -Flags ALL

