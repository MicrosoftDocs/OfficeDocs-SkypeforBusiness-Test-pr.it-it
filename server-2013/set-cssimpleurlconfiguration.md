---
title: Set-CsSimpleUrlConfiguration
TOCTitle: Set-CsSimpleUrlConfiguration
ms:assetid: f0334ae9-e6c1-4134-8749-af202169bb2a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412991(v=OCS.15)
ms:contentKeyID: 49302407
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsSimpleUrlConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una raccolta esistente di configurazioni di URL semplici. Gli URL semplici agevolano la partecipazione degli utenti a riunioni e conferenze e l'accesso degli amministratori al Pannello di controllo di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsSimpleUrlConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsSimpleUrlConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-SimpleUrl <PSListModifier>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando indicato nell'esempio 1 consente di rimuovere tutti gli URL semplici dal sito di Redmond, ma non di rimuovere la raccolta effettiva degli URL semplici. La raccolta sarà ancora presente, ma non conterrà alcun URL. A tale scopo, il comando utilizza il parametro -SimpleUrl ed imposta il valore del parametro su NULL ($Null). Questo consente di rimuovere tutti gli URL semplici dalla raccolta.

    Set-CsSimpleUrlConfiguration -Identity "site:Redmond" -SimpleUrl $Null

## ESEMPIO 2

Nell'esempio 2 viene illustrato come aggiungere un nuovo URL a una raccolta esistente di URL semplici. Per iniziare, il primo comando nell'esempio utilizza il cmdlet **New-CsSimpleUrlEntry** per creare una voce URL che punta a https://meet.fabrikam.com. Questa voce URL viene archiviata in una variabile denominata $urlEntry.

Nel secondo comando viene utilizzato il cmdlet **New-CsSimpleUrl** per creare un'istanza solo in memoria di un URL semplice. In questo esempio, il parametro Component dell'URL è impostato su Meet, il dominio è impostato su fabrikam.com, ActiveUrl è impostato su https://meet.fabrikam.com, la proprietà SimpleUrl è impostata su $urlEntry, dove $urlEntry è la voce URL creata nel primo comando.

Dopo aver creato l'URL e averlo memorizzato nel riferimento oggetto $simpleUrl, l'ultimo comando riportato nell'esempio consente di aggiungere un nuovo URL alla raccolta di URL semplificati per il sito Redmond. Questo si esegue utilizzando il cmdlet **Set-CsSimpleUrlConfiguration**, il parametro -SimpleUrl e il valore del parametro @{Add=$simpleUrl}. Questa sintassi indica che l'URL memorizzato nel riferimento oggetto $simpleUrl deve essere aggiunto alla proprietà SimpleUrl.

    $urlEntry = New-CsSimpleUrlEntry -Url "https://meet.fabrikam.com"
    $simpleUrl = New-CsSimpleUrl -Component "meet" -Domain "fabrikam.com" -SimpleUrlEntry $urlEntry -ActiveUrl "https://meet.fabrikam.com"
    
    Set-CsSimpleUrlConfiguration -Identity "site:Redmond" -SimpleUrl @{Add=$simpleUrl}

## ESEMPIO 3

Nei comandi indicati nell'esempio 3 viene illustrato come eliminare un singolo URL dalla raccolta di URL semplici. Poiché il cmdlet **Set-CsSimpleUrlConfiguration** necessita di oggetti URL, l'esempio inizia con la creazione di un nuovo oggetto che contiene esattamente gli stessi valori di proprietà dell'URL da eliminare. A tale scopo, il primo comando utilizza il cmdlet **New-CsSimpleUrlEntry** per creare una voce URL che punta a https://meet.fabrikam.com. Questa voce URL viene archiviata in una variabile denominata $urlEntry.

Dopo aver creato l'URL, il secondo comando utilizza il cmdlet **New-CsSimpleUrl** per creare un'istanza solo in memoria di un URL semplice. In questo esempio, il parametro Component dell'URL è impostato su Meet, il dominio è impostato su fabrikam.com, ActiveUrl è impostato su https://meet.fabrikam.com, la proprietà SimpleUrl è impostata su $urlEntry, dove $urlEntry è la voce URL creata nel primo comando. In questo modo viene creato un URL in memoria ($simpleUrl) che presenta gli stessi valori di proprietà dell'URL da eliminare.

Il comando finale nell'esempio consente di eliminare l'URL dalla raccolta di URL semplici per il sito di Redmond. Questo si esegue utilizzando il cmdlet **Set-CsSimpleUrlConfiguration**, il parametro -SimpleUrl e il valore del parametro @{Remove=$simpleUrl}. Tale sintassi indica che l'URL memorizzato nel riferimento oggetto $simpleUrl deve essere rimosso dalla proprietà SimpleUrl.

    $urlEntry = New-CsSimpleUrlEntry -Url "https://fabrikam.vdomain.com"
    $simpleUrl = New-CsSimpleUrl -Component "meet" -Domain "fabrikam.com" -SimpleUrlEntry $urlEntry -ActiveUrl "https://meet.fabrikam.com"
    
    Set-CsSimpleUrlConfiguration -Identity "site:Redmond" -SimpleUrl @{Remove=$simpleUrl}

## Descrizione dettagliata

In Microsoft Office Communications Server 2007 R2, le riunioni presentano URL simili al seguente:

https://imdf.litwareinc.com/Join?uri=sip%3Adavidegarghentini%40litwareinc.com%3Bgruu%3Bopaque%3Dapp%3Aconf%3Afocus%3Aid%3A125f95a0b0184dcea706f1a0191202a8\&key=EcznhLh5K5t

Tuttavia, tali URL non sono particolarmente intuitivi e non risultano facili da comunicare a un altro utente. Gli URL semplificati introdotti in Lync Server risolvono questo tipo di problemi mettendo a disposizione degli utenti degli URL simili al seguente:

https://meet.litwareinc.com/davidegarghentini/071200

Gli URL semplici costituiscono un miglioramento degli URL utilizzati nella precedente versione di Office Communications Server. Tuttavia, gli URL semplici non vengono creati automaticamente, ma devono essere configurati dall'utente. È inoltre necessario creare record DNS per ciascun URL, configurare le regole del proxy inverso per l'accesso esterno, aggiungere gli URL semplici ai certificati Front End Server e così via.

Lync Server consente di creare tre diversi tipi di URL semplici:

Meet: utilizzato per le riunioni. È necessario disporre di almeno un URL Meet per i singoli domini SIP in uso.

Admin: utilizzato per consentire agli amministratori di accedere a Lync Server.

Dialin - utilizzato per la pagina Web delle conferenze telefoniche con accesso esterno.

Gli URL semplici vengono memorizzati nelle raccolte di configurazioni di URL semplici. Durante l'installazione di Lync Server, viene creata automaticamente una raccolta globale. È inoltre possibile creare raccolte personalizzate nell'ambito del sito. In questo modo è possibile utilizzare diversi URL semplici nei singoli siti.

Le raccolte di configurazioni di URL semplici vengono create tramite il cmdlet **New-CsSimpleUrlConfiguration**. È quindi possibile utilizzare cmdlet aggiuntivi (come i cmdlet **New-CsSimpleUrl** e **Set-CsSimpleUrlConfiguration**) per popolare queste raccolte con URL semplici. Dopo aver creato le raccolte, utilizzando il cmdlet **Set-CsSimpleUrlConfiguration** è inoltre possibile modificare gli URL archiviati in tali raccolte.

L'aggiunta di un URL semplice a una raccolta è ragionevolmente semplice. Per iniziare, utilizzare i cmdlet **New-CsSimpleUrl** e **New-CsSimpleUrlEntry** per creare un URL solo in memoria. Utilizzare quindi il comando Add per aggiungere il nuovo URL alla raccolta esistente. In alternativa, è possibile utilizzare il metodo della sostituzione per sostituire tutti gli URL esistenti con uno nuovo.

La rimozione di un URL da una raccolta risulta invece più difficile, in quanto si deve prima creare un nuovo riferimento oggetto per l'URL interessato (che simuli l'URL esistente), quindi si deve utilizzare tale riferimento oggetto e il metodo della sostituzione per eliminare l'URL.

Dopo aver aggiornato una raccolta di URL semplici, è necessario eseguire il cmdlet **Enable-CsComputer**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsSimpleUrlConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsSimpleUrlConfiguration"}

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
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>L'identificatore univoco per la raccolta di URL semplici da modificare. Per modificare la raccolta globale, utilizzare la seguente sintassi: -Identity global. Per modificare una raccolta dall'ambito sito, utilizzare una sintassi simile alla seguente: -Identity &quot;site:Redmond.&quot;</p>
<p>Se il parametro non viene specificato, verrà modificata la raccolta globale.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto SimpleUrlConfiguration</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>SimpleUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Gli URL semplici configurati per questa raccolta. Questi URL devono essere creati tramite i cmdlet <strong>New-SimpleUrl</strong> e <strong>New-SimpleUrlEntry</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di Skype for Business online per cui è necessario modificare le impostazioni di configurazione degli URL semplici. Ad esempio:</p>
<p>-Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SimpleUrl.SimpleUrlConfiguration. Il cmdlet **Set-CsSimpleUrlConfiguration** accetta istanze da pipeline dell'oggetto di configurazione URL semplice.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Get-CsSimpleUrlConfiguration](get-cssimpleurlconfiguration.md)  
[New-CsSimpleUrl](new-cssimpleurl.md)  
[New-CsSimpleUrlConfiguration](new-cssimpleurlconfiguration.md)  
[New-CsSimpleUrlEntry](new-cssimpleurlentry.md)  
[Remove-CsSimpleUrlConfiguration](remove-cssimpleurlconfiguration.md)

