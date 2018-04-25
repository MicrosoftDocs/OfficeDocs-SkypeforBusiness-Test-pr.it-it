---
title: New-CsClientVersionConfiguration
TOCTitle: New-CsClientVersionConfiguration
ms:assetid: e7aac850-9e29-4d18-8929-74a89e9355cd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399029(v=OCS.15)
ms:contentKeyID: 49302298
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClientVersionConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta delle impostazioni di configurazione della versione del client. Le impostazioni di configurazione della versione del client determinano se Lync Server verifica il numero di versione di ogni applicazione client che accede al sistema. Se il filtro versione client è abilitato, la capacità dell'applicazione client di accedere al sistema dipenderà dalle impostazioni configurate nel criterio di versione client appropriato. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsClientVersionConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-DefaultAction <Allow | AllowWithUrl | Block | BlockWithUrl>] [-DefaultURL <String>] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 consente di creare una nuova raccolta di impostazioni di configurazione per la versione client per il sito Redmond. In tale comando il parametro Enabled è impostato su False, pertanto il filtro client è disabilitato per il sito Redmond.

    New-CsClientVersionConfiguration -Identity site:Redmond -Enabled $False

## ESEMPIO 2

Nell'esempio 2 viene mostrato come creare una nuova raccolta di impostazioni di configurazione per la versione client nella memoria, modificare tale raccolta e quindi rendere tali impostazioni virtuali una raccolta effettiva di impostazioni applicate al sito Redmond. A tale scopo, nel primo comando vengono utilizzati il cmdlet **New-CsClientVersionConfiguration** e il parametro InMemory per creare una raccolta di impostazioni con valore Identity site:Redmond solo in memoria. La raccolta viene archiviata in una variabile denominata $x ed è presente soltanto in memoria: se la sessione di Windows PowerShell viene terminata o se viene eliminata la variabile $x, tali impostazioni di configurazione per la versione client scompariranno e non verranno mai applicate al sito Redmond.

Nel comando 2 il valore della proprietà DefaultAction per le impostazioni virtuali è impostato su Block. Nel comando 3 il cmdlet **Set-CsClientVersionConfiguration** viene utilizzato per trasformare le impostazioni virtuali in una raccolta effettiva di impostazioni di configurazione per la versione client, applicata al sito Redmond.

    $x = New-CsClientVersionConfiguration -Identity site:Redmond -InMemory
    $x.DefaultAction = "Block" 
    Set-CsClientVersionConfiguration -Instance $x

## Descrizione dettagliata

Con Lync Server gli amministratori dispongono di uno spazio di manovra considerevole quando devono specificare il software client (e, ugualmente importante, il numero di versione del software) che gli utenti possono utilizzare per accedere al sistema. Ad esempio, non vi sono motivi tecnici che impongono agli utenti di accedere a Lync Server utilizzando Lync. Da un punto di vista tecnico, niente impedisce agli utenti di accedere utilizzando Microsoft Office Communicator 2007 R2.

Vi potrebbero essere invece motivi di carattere non tecnico per cui si preferisce che gli utenti non accedano tramite Office Communicator 2007 R2. Office Communicator 2007 R2 ad esempio non supporta tutte le caratteristiche e le funzionalità disponibili in Lync. Agli utenti che effettuano l'accesso mediante Office Communicator 2007 R2 verrà pertanto offerta un'esperienza diversa rispetto agli utenti che per l'accesso utilizzano Lync. Ciò può creare difficoltà per gli utenti; può inoltre creare difficoltà per il personale del supporto tecnico che deve fornire assistenza per varie applicazioni client diverse.

Se questo può costituire un problema per l'organizzazione, è possibile utilizzare il filtro versione client per specificare quali applicazioni client possono essere utilizzate per accedere a Lync Server. Quando si installa Lync Server, viene installato e abilitato un insieme globale di impostazioni di configurazione per la versione client. Tali impostazioni vengono utilizzate per determinare se il filtro versione client è abilitato o meno.

Oltre alle impostazioni globali, il cmdlet **New-CsClientVersionConfiguration** consente di creare impostazioni di configurazione per la versione client nell'ambito del sito. Quando tali impostazioni vengono applicate nell'ambito del sito, hanno la precedenza sulle impostazioni globali. Si supponga ad esempio che il filtro versione client sia stato abilitato nell'ambito globale e che quindi si provveda a creare una raccolta di impostazioni diversa per il sito Redmond, ovvero una raccolta di impostazioni in cui il filtro versione client è disabilitato. In tal caso, il filtro versione client verrà disabilitato per tutti gli utenti che dispongono di account nel sito Redmond.

Si noti, tuttavia, che agli utenti anonimi vengono applicate solo le impostazioni globali, in quanto tali utenti non sono associati a un sito.

La configurazione della versione client non è una funzionalità di protezione. La tecnologia si basa su funzioni di auto-reporting da applicazioni client e non viene verificato se un'applicazione e il relativo numero di versione sono realmente quelli dichiarati.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsClientVersionConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClientVersionConfiguration"}

## Parametri


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Obbligatorio</th>
<th>Tipo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Rappresenta l'identificatore univoco da assegnare alla nuova raccolta delle impostazioni di configurazione per la versione client. Poiché è possibile creare nuove raccolte solo nell'ambito del sito, il valore Identity avrà sempre il prefisso &quot;site:&quot; seguito dal nome del sito, come, ad esempio, &quot;site:Redmond&quot;. Il comando riportato sopra non viene eseguito correttamente se è già presente una raccolta di impostazioni con identità site:Redmond.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultAction</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.DefaultAction</p></td>
<td><p>Indica l'azione da eseguire se un utente tenta di accedere da un'applicazione client il cui numero di versione non è presente nel criterio della versione client appropriato. DefaultAction deve essere impostato su uno dei seguenti valori:</p>
<p>Allow. All'applicazione client viene consentito di accedere.</p>
<p>AllowWithUrl. All'applicazione client viene consentito di accedere. Verrà inoltre visualizzata una finestra di messaggio con l'URL di una pagina Web da cui l'utente può scaricare un'applicazione client approvata. L'URL della pagina Web deve essere specificato come valore della proprietà DefaultUrl.</p>
<p>Block. All'applicazione client viene impedito di accedere.</p>
<p>BlockWithUrl. All'applicazione client viene impedito di accedere. Nella finestra di messaggio &quot;Accesso negato&quot; visualizzata sarà tuttavia incluso l'URL di una pagina Web da cui l'utente può scaricare un'applicazione client approvata. L'URL della pagina Web deve essere specificato come valore della proprietà DefaultUrl.</p>
<p>Tale proprietà viene ignorata se la proprietà Enabled è impostata su False. Quando la proprietà Enabled è impostata su False, non viene applicato alcun tipo di filtro versione client.</p></td>
</tr>
<tr class="even">
<td><p><em>DefaultURL</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Specifica l'URL della pagina Web da cui gli utenti possono scaricare un'applicazione client approvata. Se tale parametro è specificato e se DefaultAction è impostato su BlockWithUrl, l'URL verrà indicato nella finestra di messaggio &quot;Accesso negato&quot; visualizzata ogni volta che un utente tenta di accedere da un'applicazione client non supportata.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Consente di indicare se il filtro versione client è abilitato o disabilitato. Se la proprietà Enabled è True, il server verificherà il numero di versione di ciascuna applicazione client che tenta di accedere, quindi consentirà o negherà l'accesso in base al criterio di versione client appropriato. Se la proprietà Enabled è False, qualsiasi applicazione client in grado di eseguire l'accesso potrà accedere.</p>
<p>Il valore predefinito è True.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsClientVersionConfiguration** non accetta input inviato tramite pipeline.

## Tipi restituiti

Crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsClientVersionConfiguration](get-csclientversionconfiguration.md)  
[Remove-CsClientVersionConfiguration](remove-csclientversionconfiguration.md)  
[Set-CsClientVersionConfiguration](set-csclientversionconfiguration.md)

