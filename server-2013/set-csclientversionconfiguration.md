---
title: Set-CsClientVersionConfiguration
TOCTitle: Set-CsClientVersionConfiguration
ms:assetid: 7cd2e86f-2d31-4db2-9d0f-f1418fd4aba2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398623(v=OCS.15)
ms:contentKeyID: 49301092
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsClientVersionConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica la raccolta specificata delle impostazioni di configurazione della versione del client. Le impostazioni di configurazione della versione del client determinano se Lync Server verifica il numero di versione di ogni applicazione client che accede al sistema. Se il filtro versione client è abilitato, la capacità dell'applicazione client di accedere al sistema dipenderà dalle impostazioni configurate nel criterio di versione client appropriato. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsClientVersionConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsClientVersionConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-DefaultAction <Allow | AllowWithUrl | Block | BlockWithUrl>] [-DefaultURL <String>] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene utilizzato il cmdlet **Set-CsClientVersionConfiguration** per modificare la raccolta di impostazioni con Identity "site:Redmond". In questo caso, il parametro Enabled è impostato su False per disabilitare le impostazioni di configurazione della versione client.

    Set-CsClientVersionConfiguration -Identity site:Redmond -Enabled $False

## ESEMPIO 2

Nell'esempio 2 la proprietà DefaultUrl viene modificata per tutte le impostazioni di configurazione della versione client attualmente in uso nell'organizzazione. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsClientVersionConfiguration** senza alcun parametro aggiuntivo per restituire tutte le impostazioni di configurazione della versione client. Tali informazioni vengono quindi inviate tramite pipe al cmdlet **Set-CsClientVersionConfiguration**, che imposta su https://litwareinc.com/csclients il valore della proprietà DefaultUrl per ogni raccolta di configurazioni.

    Get-CsClientVersionConfiguration | Set-CsClientVersionConfiguration -DefaultURL "https://litwareinc.com/csclients"

## ESEMPIO 3

Nell'esempio 3 vengono apportate modifiche a tutte impostazioni di configurazione delle versioni client in cui il valore corrente di DefaultAction è impostato su Block. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsClientVersionConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione della versione client attualmente in uso. Queste informazioni vengono quindi inviate tramite pipe al cmdlet **Where-Object**, che seleziona solo gli elementi in cui la proprietà DefaultAction è uguale a "Block". La raccolta così filtrata viene a sua volta inviata tramite pipe al cmdlet **Set-CsClientVersionConfiguration**, che esegue due azioni su ogni elemento della raccolta: 1) imposta DefaultAction su BlockWithUrl e 2) imposta DefaultUrl su https://litwareinc.com/csclients.

    Get-CsClientVersionConfiguration | Where-Object {$_.DefaultAction -eq "Block"} | Set-CsClientVersionConfiguration -DefaultAction "BlockWithUrl" -DefaultURL "https://litwareinc.com/csclients"

## Descrizione dettagliata

Lync Server consente agli amministratori una considerevole libertà di azione nello specificare il software client (e, ugualmente importante, il numero di versione di tale software) che gli utenti possono utilizzare per eseguire l'accesso al sistema. Ad esempio, non esistono motivi tecnici che impongano a un utente di accedere a Lync Server utilizzando Lync. Da un punto di vista tecnico, non sono previste limitazioni che impediscano a un utente di accedere utilizzando Microsoft Office Communicator 2007 R2.

D'altra parte, potrebbero esservi motivi non di natura tecnica per cui si preferisce che gli utenti non accedano utilizzando Office Communicator 2007 R2. Ad esempio, Office Communicator 2007 R2 non supporta tutte le caratteristiche e funzionalità disponibili in Lync. Gli utenti che accedono con Office Communicator 2007 R2 avranno pertanto un'esperienza diversa dagli utenti che accedono utilizzando Lync. Questo può creare difficoltà agli utenti, ma anche al personale addetto all'assistenza tecnica che deve fornire supporto per diverse applicazioni client.

Se questo rischia di rappresentare un problema per l'organizzazione, è possibile utilizzare il filtro della versione client per specificare quali applicazioni client possono essere utilizzate per accedere a Lync Server. Quando si installa Lync Server, viene installato e abilitato un insieme globale di impostazioni di configurazione della versione client. Queste impostazioni vengono utilizzate per determinare se il filtro della versione client è abilitato o meno. Oltre alle impostazioni globali, le impostazioni di configurazione della versione client possono essere applicate nell'ambito del sito. In questi casi le impostazioni del sito avranno la precedenza sulle impostazioni globali.

Il cmdlet **Set-CsClientVersionConfiguration** consente di modificare una raccolta esistente di impostazioni di configurazione della versione client.

Si noti che la configurazione della versione client non è una funzionalità di sicurezza. La tecnologia si affida all'autosegnalazione da parte delle applicazioni client e non tenta di verificare che un'applicazione sia veramente quell'applicazione e che il numero della versione sia effettivamente quello indicato.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsClientVersionConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsClientVersionConfiguration"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DefaultAction</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.DefaultAction</p></td>
<td><p>Indica l'azione da intraprendere se un utente tenta di accedere da un'applicazione client il cui numero di versione non viene trovato nell'appropriato criterio di versione client. DefaultAction deve essere impostato su uno dei seguenti valori:</p>
<p>Allow. All'applicazione client viene consentito l'accesso.</p>
<p>AllowWithUrl. All'applicazione client viene consentito l'accesso. In aggiunta, verrà visualizzata all'utente una finestra di messaggio con incluso l'URL di una pagina Web da dove quell'utente può scaricare un'applicazione client approvata. L'URL per questa pagina Web deve essere specificato come valore della proprietà DefaultUrl.</p>
<p>Block. All'applicazione client viene impedito l'accesso.</p>
<p>BlockWithUrl. All'applicazione client viene impedito l'accesso. Tuttavia, nella finestra del messaggio &quot;Accesso negato&quot; visualizzata all'utente verrà incluso l'URL di una pagina Web da dove quell'utente può scaricare un'applicazione client approvata. L'URL per questa pagina Web deve essere specificato come valore della proprietà DefaultUrl.</p>
<p>Questa proprietà viene ignorata se la proprietà Enable è impostata su False. Quando la proprietà Enabled è impostata su False non viene effettuato nessun tipo di filtraggio versione client.</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultURL</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Specifica l'URL della pagina Web da cui gli utenti possono scaricare un'applicazione client approvata. Se tale parametro è specificato e se DefaultAction è impostato su BlockWithUrl, l'URL verrà indicato nella finestra di messaggio &quot;Accesso negato&quot; visualizzata ogni volta che un utente tenta di accedere da un'applicazione client non supportata.</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se il filtraggio versione client è abilitato o disabilitato. Se la proprietà Enabled è impostata su True, il server controllerà il numero di versione di ciascuna applicazione client che tenta di accedere, il server poi consentirà o negherà l'accesso basandosi sui criteri di versione client appropriati. Se la proprietà Enabled è impostata su False sarà consentito l'accesso a qualsiasi applicazione client in grado di effettuarlo.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Indica l'identificatore univoco delle impostazioni di configurazione della versione client da modificare. Per modificare le impostazioni globali, utilizzare la seguente sintassi: -Identity global. Per modificare le impostazioni assegnate nell'ambito del sito, utilizzare una sintassi simile alla seguente: &quot;site:Redmond&quot;.</p>
<p>Se non viene incluso questo parametro, il cmdlet <strong>Set-CsClientVersionConfiguration</strong> configurerà automaticamente le impostazioni globali.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto ClientVersionPolicy</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration. Il cmdlet **Set-CsClientVersionConfiguration** accetta le istanze dell'oggetto configurazione della versione client inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CsClientVersionConfiguration** non restituisce alcun oggetto o valore. Configura invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsClientVersionConfiguration](get-csclientversionconfiguration.md)  
[New-CsClientVersionConfiguration](new-csclientversionconfiguration.md)  
[Remove-CsClientVersionConfiguration](remove-csclientversionconfiguration.md)

