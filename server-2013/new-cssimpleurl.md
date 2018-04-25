---
title: New-CsSimpleUrl
TOCTitle: New-CsSimpleUrl
ms:assetid: 0dcf919e-9896-4428-8f12-0fc611661fa8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398180(v=OCS.15)
ms:contentKeyID: 49299673
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSimpleUrl

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo URL semplice che può essere poi aggiunto alla raccolta di configurazioni di URL semplici. Gli URL semplici agevolano la partecipazione degli utenti a riunioni e conferenze e l'accesso degli amministratori al Pannello di controllo di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsSimpleUrl -Component <String> -Domain <String> [-ActiveUrl <String>] [-SimpleUrlEntry <PSListModifier>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene illustrato come aggiungere un nuovo URL a una raccolta esistente di URL semplici. Il primo comando nell'esempio utilizza innanzitutto il cmdlet **New-CsSimpleUrlEntry** per creare una voce URL che punta a https://meet.fabrikam.com. Questa voce URL viene archiviata in una variabile denominata $urlEntry.

Nel secondo comando viene utilizzato il cmdlet **New-CsSimpleUrl** per creare un'istanza solo in memoria di un URL semplice. In questo esempio, il parametro Component dell'URL è impostato su Meet, il dominio è impostato su fabrikam.com, ActiveUrl è impostato su https://meet.fabrikam.com, la proprietà SimpleUrl è impostata su $urlEntry, dove $urlEntry è la voce URL creata nel primo comando.

Dopo aver creato l'URL e averlo memorizzato nel riferimento oggetto $simpleUrl, l'ultimo comando nell'esempio consente di aggiungere il nuovo URL alla raccolta di URL semplificati per il sito Redmond. Per ottenere questo risultato viene utilizzato il cmdlet **Set-CsSimpleUrlConfiguration**, il parametro SimpleUrl e il valore del parametro @{Add=$simpleUrl}. Questa sintassi fa in modo che l'URL memorizzato nel riferimento oggetto $simpleUrl venga aggiunto alla proprietà SimpleUrl.

    $urlEntry = New-CsSimpleUrlEntry -Url "https://meet.fabrikam.com"
    $simpleUrl = New-CsSimpleUrl -Component "meet" -Domain "fabrikam.com" -SimpleUrlEntry $urlEntry -ActiveUrl "https://meet.fabrikam.com"
    Set-CsSimpleUrlConfiguration -Identity "site:Redmond" -SimpleUrl @{Add=$simpleUrl}

## Descrizione dettagliata

In Microsoft Office Communications Server 2007 R2, per le riunioni si utilizzavano URL simili al seguente:

https://imdf.litwareinc.com/Join?uri=sip%3Akenmyer%40litwareinc.com%3Bgruu%3Bopaque%3Dapp%3Aconf%3Afocus%3Aid%3A125f95a0b0184dcea706f1a0191202a8\&key=EcznhLh5K5t

Tuttavia, URL di questo tipo non sono particolarmente intuitivi e facili da comunicare ad altri utenti. Gli URL semplificati introdotti in Lync Server 2010 risolvono questo tipo di problema mettendo a disposizione degli utenti degli URL simili al seguente:

https://meet.litwareinc.com/kenmyer/071200

Gli URL semplificati rappresentano un miglioramento notevole rispetto agli URL utilizzati in Office Communications Server. Tenere presente che gli URL semplificati non vengono creati automaticamente, ma devono essere configurati dall'utente. Inoltre, è necessario creare i record DNS (Domain Name System) per ciascun URL, configurare regole proxy inverse per gli accessi esterni, aggiungere gli URL semplificati ai certificati Front End Server e così via.

Lync Server consente di creare tre diversi tipi di URL semplici:

Meet: utilizzato per le riunioni. Occorre avere almeno un URL di tipo Meet per ciascuno dei propri domini SIP.

Admin: utilizzato per consentire agli amministratori di accedere al Pannello di controllo di Lync Server.

Dialin: utilizzato per le pagine Web delle conferenze telefoniche con accesso esterno.

Gli URL semplici vengono archiviati nelle raccolte di configurazioni di URL semplici. Quando si installa Lync Server, viene creata automaticamente una raccolta globale. È inoltre possibile creare raccolte personalizzate nell'ambito del sito. In questo modo, è possibile utilizzare diversi URL semplici nei singoli siti.

Per aggiungere un URL effettivo a una raccolta di URL semplici, è necessario innanzitutto creare l'URL utilizzando i cmdlet **New-CsSimpleUrl** e **New-CsSimpleUrlEntry**. Il cmdlet **New-CsSimpleUrlEntry** consente di creare una voce URL: un URL (ad esempio, https://meet.litwareinc.com) che può essere utilizzato come URL semplice per riunioni, amministrazione o conferenze telefoniche con accesso esterno. L'oggetto creato dal cmdlet **New-CsSimpleUrlEntry** viene aggiunto alla proprietà SimpleUrlEntry di un nuovo URL semplice. È necessario utilizzare un altro cmdlet per creare l'oggetto, in quanto la proprietà SimpleUrlEntry può contenere diversi URL. Tuttavia, è possibile designare solo uno di questi URL come URL attivo. L'URL attivo rappresenta l'URL effettivo utilizzato per riunioni, amministrazione o conferenze telefoniche con accesso esterno.

Dopo avere creato una voce URL semplificato, utilizzare il cmdlet **New-CsSimpleUrl** per creare nella sola memoria un'istanza di un URL semplificato, definendo alcune impostazioni come il componente (il tipo di URL semplificato), il dominio, l'URL attivo e tutte le voci relative all'URL semplificato. Una volta creato, l'oggetto che rappresenta l'URL semplificato può essere aggiunto a una raccolta nuova o esistente di URL semplificati. Dopo aver aggiornato una raccolta di URL semplificati, è necessario utilizzare il cmdlet **Enable-CsComputer**.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **New-CsSimpleUrl** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets -match "New-CsSimpleUrl\\b"}

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
<td><p><em>Component</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Indica il tipo di URL semplificato da creare. I valori validi sono:</p>
<p>Meet - URL utilizzato per la gestione delle riunioni.</p>
<p>Admin - URL che punta al Pannello di controllo di Lync Server.</p>
<p>Dialin - URL utilizzato per le conferenze telefoniche con accesso esterno.</p>
<p>Ad esempio: -Component &quot;Meet&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Domain</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Dominio SIP dell'URL semplificato. Ad esempio: -Domain &quot;litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>ActiveUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indica l'URL a cui stanno effettivamente accedendo gli utenti. La proprietà SimpleUrlEntry può contenere diversi URL, ma solo uno di quegli URL può essere attivo in un dato momento nel tempo. Se si tenta di impostare il parametro ActiveUrl su un valore non incluso nella proprietà SimpleUrlEntry, si riceve un messaggio di errore.</p>
<p>Per assegnare un URL attivo, utilizzare semplicemente lo stesso URL come valore del parametro. Ad esempio: -ActiveUrl https://meet.litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>SimpleUrlEntry</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Raccolta di URL per il componente specificato. Ad esempio, sia https://meet.litwareinc.com sia https://litwareinc.com/meet potrebbero essere configurati come voci URL per il componente Meet. Tuttavia, solo uno di quei due URL può (e deve) essere configurato come URL attivo.</p>
<p>Le voci URL semplificati devono essere create tramite il cmdlet <strong>New-CsSimpleUrlEntry</strong>.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsSimpleUrl** non accetta dati da pipeline.

## Tipi restituiti

Il cmdlet **New-CsSimpleUrl** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.SimpleUtl.SimpleUrl.

## Vedere anche

#### Ulteriori risorse

[New-CsSimpleUrlConfiguration](new-cssimpleurlconfiguration.md)  
[New-CsSimpleUrlEntry](new-cssimpleurlentry.md)

