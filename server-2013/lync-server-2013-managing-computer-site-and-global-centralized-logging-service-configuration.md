---
title: Gestione della configurazione di computer, siti e servizio di registrazione centralizzato globale
TOCTitle: Gestione della configurazione di computer, siti e servizio di registrazione centralizzato globale
ms:assetid: 93b9a354-9aea-4b3a-a4fe-68a89f436196
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688138(v=OCS.15)
ms:contentKeyID: 49887662
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestione della configurazione di computer, siti e servizio di registrazione centralizzato globale

 

_**Ultima modifica dell'argomento:** 2014-02-04_

Il servizio di registrazione centralizzato può essere eseguito in un ambito che include un singolo computer, un pool di computer, nell'ambito di un sito (ovvero un sito definito, ad esempio il sito Redmond contenente una raccolta di computer e pool della distribuzione) o in un ambito globale (ovvero tutti i computer e i pool della distribuzione).

Per configurare l'ambito del servizio servizio di registrazione centralizzato mediante la Lync Server Management Shell, è necessario essere membri dei gruppi di sicurezza del controllo di accesso basato sul ruolo (RBAC) CsAdministrator o CsServerAdministrator oppure di un ruolo personalizzato contenente l'uno o l'altro di questi due gruppi. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente) eseguire il comando seguente dalla Lync Server Management Shell o dal prompt di Windows PowerShell:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "<Lync Server 2013 cmdlet>"}

Esempio:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Set-CsClsConfiguration"}


> [!NOTE]
> Windows PowerShell offre un maggior numero di scelte e opzioni di configurazione aggiuntive non disponibili mediante CLSController.exe. CLSController offre un metodo rapido e sintetico per eseguire i comandi, tuttavia è limitato al set di comandi disponibili per CLSController. Windows PowerShell non è limitato ai soli comandi disponibili per il processore dei comandi di CLSController e offre un più ampio set di comandi e un set di opzioni più avanzate. Ad esempio, CLSController.exe offre opzioni sull'ambito, ovvero computer e pool. Con Windows PowerShell, è possibile indicare computer e pool nella maggior parte dei comandi e quando si definiscono nuovi scenari (CLSController ha un numero finito di scenari non modificabili dall'utente) è possibile definire un sito o un ambito globale. Questa potente funzionalità di Windows PowerShell consente di definire uno scenario con un ambito globale o a livello di sito, tuttavia limita la registrazione effettiva a un computer o un pool.<BR>Esistono alcune differenze fondamentali tra i comandi della riga di comando che è possibile eseguire in Windows PowerShell o in CLSController. Windows PowerShell offre un metodo avanzato per configurare e definire gli scenari e riutilizzare tali scenari in modo significativo per la risoluzione dei problemi. Mentre CLSController non offre un modo rapido ed efficiente per eseguire comandi e ottenere risultati, il set di comandi di CLSController è limitato dal numero finito di comandi disponibili dalla riga di comando. A differenza dei cmdlet di Windows PowerShell, con CLSController non è possibile definire nuovi scenari, gestire un ambito a livello globale o di sito e si applicano molte altre limitazioni derivanti dal numero finito del set di comandi non configurabile dinamicamente. Sebbene CLSController rappresenti un mezzo per l'esecuzione veloce, Windows PowerShell offre metodi per estendere le funzionalità del servizio di registrazione centralizzato al di là delle possibilità di CLSController.



Gli ambiti a livello di singolo computer possono essere definiti durante l'esecuzione di un comando [Search-CsClsLogging](https://docs.microsoft.com/en-us/powershell/module/skype/Search-CsClsLogging), [Show-CsClsLogging](https://docs.microsoft.com/en-us/powershell/module/skype/Show-CsClsLogging), [Start-CsClsLogging](https://docs.microsoft.com/en-us/powershell/module/skype/Start-CsClsLogging), [Stop-CsClsLogging](https://docs.microsoft.com/en-us/powershell/module/skype/Stop-CsClsLogging), [Sync-CsClsLogging](https://docs.microsoft.com/en-us/powershell/module/skype/Sync-CsClsLogging) e [Update-CsClsLogging](https://docs.microsoft.com/en-us/powershell/module/skype/Update-CsClsLogging) mediante il parametro –Computers. Il parametro –Computers accetta un elenco con valori separati da virgole di nomi di dominio completi dei computer di destinazione.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>È inoltre possibile definire –Pools e un elenco di valori separati da virgole di pool in cui si desidera eseguire i comandi di registrazione.</td>
</tr>
</tbody>
</table>


Gli ambiti a livello di sito e globali sono definiti nei cmdlet **New-**, **Set-** e **Remove-** per il servizio di registrazione centralizzato. Negli esempi seguenti viene illustrato come impostare un ambito a livello di sito o globale.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>I comandi illustrati possono contenere i parametri e concetti trattati in altre sezioni. I comandi di esempio servono a illustrare l'uso del parametro <strong>–Identity</strong> per definire l'ambito e gli altri parametri sono inclusi per completezza e per specificare l'ambito. Per dettagli sui cmdlet <strong>Set-CsClsConfiguration</strong>, vedere <a href="https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClsConfiguration">Set-CsClsConfiguration</a> nella documentazione sulle operazioni.</td>
</tr>
</tbody>
</table>


## Per recuperare la configurazione del servizio di registrazione centralizzato

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Digitare quanto segue al prompt dei comandi:
    
        Get-CsClsConfiguration

Usare i cmdlet **New-CsClsConfiguration** e **Set-CsClsConfiguration** per creare una nuova configurazione o aggiornarne una esistente.

Quando si esegue **Get-CsClsConfiguration**, vengono visualizzate informazioni analoghe a quelle nella cattura di schermata seguente, in cui la distribuzione presenta attualmente la configurazione globale predefinita ma nessuna configurazione a livello di sito:

![Output di esempio di Get-CsClsConfiguration.](images/JJ688029.23f98ddc-fc48-499a-b6c5-752611f2a0b0(OCS.15).jpg "Output di esempio di Get-CsClsConfiguration.")

## Per recuperare la configurazione corrente del servizio di registrazione centralizzato dall'archivio locale del computer

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Digitare quanto segue al prompt dei comandi:
    
        Get-CsClsConfiguration -LocalStore

Quando si usa il primo esempio in cui **Get-CsClsConfiguration** non specifica alcun parametro, il comando fa riferimento a archivio di gestione centrale per i dati. Se si specifica il parametro –LocalStore, il comando fa invece riferimento al computer LocalStore di archivio di gestione centrale.

## Per recuperare un elenco di scenari attualmente definiti

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Digitare quanto segue al prompt dei comandi:
    
        Get-CsClsConfiguration -Identity <scope and name> | Select-Object -ExpandProperty Scenarios
    
    Ad esempio, per recuperare gli scenari definiti nell'ambito globale:
    
        Get-CsClsConfiguration -Identity "global" | Select-Object -ExpandProperty Scenarios

Il cmdlet **Get-CsClsConfiguration** visualizza sempre gli scenari che fanno parte della configurazione di un determinato ambito. Nella maggior parte dei casi, non sono visualizzati tutti gli scenari e sono presenti troncamenti. Il comando usato in questo caso elenca tutti gli scenari e informazioni parziali sui provider, le impostazioni e i flag in uso.

## Per aggiornare un ambito globale per il servizio di registrazione centralizzato mediante Windows PowerShell

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Digitare quanto segue al prompt dei comandi:
    
        Set-CsClsConfiguration -Identity <scope> -EtlFileRolloverSizeMB <size for logging file in megabytes>
    
    Esempio:
    
        Set-CsClsConfiguration -Identity "global" -EtlFileRolloverSizeMB 40

Il comando indica al CLSAgent in ogni computer e pool della distribuzione di impostare le dimensioni del valore di rollover per il file di traccia su 40 megabyte. Il comando si applica a tutti i computer e i pool in tutti i siti e imposta il valore di rollover del log di traccia configurato su 40 megabyte.

## Per aggiornare un ambito a livello di sito per il servizio di registrazione centralizzato mediante Windows PowerShell

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Digitare quanto segue al prompt dei comandi:
    
        Set-CsClsConfiguration -Identity <scope/site name> -EtlFileRolloverSizeMB <size for logging file in megabytes> -EtlFileFolder <default location %TEMP%\Tracing>
    
    Esempio:
    
        Set-CsClsConfiguration -Identity "site/Redmond" -EtlFileRolloverSizeMB 40 -EtlFileFolder "C:\LogFiles\Tracing" 
    

    > [!NOTE]
    > Come si nota nell'esempio, il percorso predefinito dei file di log è %TEMP%\Tracing. Tuttavia, poiché il file viene in effetti scritto da CLSAgent il quale viene eseguito con l'account Servizio di rete, la variabile %TEMP% si espande in %WINDIR%\ServiceProfiles\NetworkService\AppData\Local.



Il comando indica al CLSAgent in ogni computer e pool del sito Redmond di impostare le dimensioni del valore di rollover per il file di traccia su 40 megabyte. I computer e i pool in altri siti non verranno modificati dal comando e continueranno a usare il valore di rollover del log di traccia definito per impostazione predefinita (20 megabyte) o durante l'avvio della sessione di registrazione.

## Per creare una nuova configurazione del servizio di registrazione centralizzato

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Digitare quanto segue al prompt dei comandi:
    
        New-CsClsConfiguration -Identity <scope and name> [CsClsConfiguration options for this site]
    

    > [!NOTE]
    > New-CsClsConfiguration offre accesso a numerose impostazioni di configurazione facoltative. Per dettagli sulle opzioni di configurazioni, vedere <A href="https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsClsConfiguration">Get-CsClsConfiguration</A> e <A href="lync-server-2013-understanding-centralized-logging-service-configuration-settings.md">Informazioni sulle impostazioni di configurazione del servizio di registrazione centralizzato</A>.

    
    Ad esempio, per creare una nuova configurazione che definisce una cartella di rete per i file di cache, il periodo di rollover per i file di log e le dimensioni di rollover per tali file, occorre digitare quanto segue:
    
        New-CsClsConfiguration -Identity "site:Redmond" -CacheFileNetworkFolder "\\fs01.contoso.net\filestore\logfiles" -EtlFileRolloverMinutes 120 -EtlFileRolloverSizeMB 40

È consigliabile pianificare con attenzione la creazione di nuove configurazioni e la modalità di definizione di nuove proprietà per il servizio di registrazione centralizzato. È anche opportuno prestare attenzione alle modifiche che vi si apportano accertandosi di comprenderne l'impatto sulla capacità di registrare correttamente gli scenari dei problemi. È consigliabile apportare alla configurazione modifiche in grado di migliorare la gestione dei log con dimensioni e periodi di rollover che consentano di risolvere i problemi quando si verificano.

## Per rimuovere una configurazione esistente del servizio di registrazione centralizzato

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Digitare quanto segue al prompt dei comandi:
    
        Remove-CsClsConfiguration -Identity <scope and name>
    
    Ad esempio, per rimuovere una configurazione del servizio di registrazione centralizzato creata per aumentare il tempo di rollover dei file di log, aumentarne le dimensioni e impostare il percorso della cache dei file di log su una condivisione di rete, procedere nel modo seguente:
    
        Remove-CsClsConfiguration -Identity "site:Redmond"
    

    > [!NOTE]
    > Questa è la nuova configurazione creata nella procedura "Per creare una nuova configurazione del servizio di registrazione centralizzato".



Se si sceglie di rimuovere una configurazione a livello di sito, il sito userà le impostazioni globali.

## Vedere anche

#### Concetti

[Panoramica del servizio di registrazione centralizzato](lync-server-2013-overview-of-the-centralized-logging-service.md)  

#### Ulteriori risorse

[Gestione delle impostazioni di configurazione del servizio di registrazione centralizzato tramite PowerShell](lync-server-2013-managing-the-centralized-logging-service-configuration-settings.md)  
[Set-CsClsConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsClsConfiguration)  
[Get-CsClsConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsClsConfiguration)  
[New-CsClsConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsClsConfiguration)  
[Remove-CsClsConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsClsConfiguration)

