---
title: New-CsSimpleUrlEntry
TOCTitle: New-CsSimpleUrlEntry
ms:assetid: 3d9dbebf-d23f-40da-9676-19e7906decda
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425902(v=OCS.15)
ms:contentKeyID: 49300291
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSimpleUrlEntry

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova voce URL semplice, un elemento necessario quando si crea un URL semplice. Gli URL semplici agevolano la partecipazione degli utenti a riunioni e conferenze e l'accesso degli amministratori al Pannello di controllo di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsSimpleUrlEntry -Url <String>

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene illustrato come aggiungere un nuovo URL a una raccolta esistente di URL semplici. Il primo comando nell'esempio utilizza innanzitutto il cmdlet **New-CsSimpleUrlEntry** per creare una voce URL che punta a https://meet.fabrikam.com. Questa voce URL viene archiviata in una variabile denominata $urlEntry.

Nel secondo comando viene utilizzato il cmdlet **New-CsSimpleUrl** per creare un'istanza solo in memoria di un URL semplice. In questo esempio, il parametro Component dell'URL è impostato su Meet, il dominio è impostato su fabrikam.com, ActiveUrl è impostato su https://meet.fabrikam.com, la proprietà SimpleUrl è impostata su $urlEntry, dove $urlEntry è la voce URL creata nel primo comando.

Dopo aver creato l'URL e averlo memorizzato nel riferimento oggetto $simpleUrl, l'ultimo comando nell'esempio consente di aggiungere il nuovo URL alla raccolta di URL semplificati per il sito Redmond. Per ottenere questo risultato viene utilizzato il cmdlet **Set-CsSimpleUrlConfiguration**, il parametro SimpleUrl e il valore del parametro @{Add=$simpleUrl}. Questa sintassi fa in modo che l'URL memorizzato nel riferimento oggetto $simpleUrl venga aggiunto alla proprietà SimpleUrl.

    $urlEntry = New-CsSimpleUrlEntry -Url "https://meet.fabrikam.com"
    $simpleUrl = New-CsSimpleUrl -Component "meet" -Domain "fabrikam.com" -SimpleUrlEntry $urlEntry -ActiveUrl "https://meet.fabrikam.com"
    
    Set-CsSimpleUrlConfiguration -Identity "site:Redmond" -SimpleUrl @{Add=$simpleUrl}

## ESEMPIO 2

Nell'esempio 2, a una raccolta esistente di URL semplici vengono aggiunte alcune voci URL. A tale scopo, il primo comando nell'esempio utilizza il cmdlet **New-CsSimpleUrlEntry** per creare una voce URL che punta a https://meet.fabrikam.com. Questa voce URL viene archiviata in una variabile denominata $urlEntry. Il secondo comando crea quindi una seconda voce URL che punta a https://dialin.fabrikam.com e che viene archiviata nella variabile $urlEntry2.

Dopo che le due voci URL sono state create, il cmdlet **New-CsSimpleUrl** viene utilizzato per creare due istanze solo in memoria di un URL semplice. Nella prima istanza, il parametro Component dell'URL è impostato su Meet, il dominio è impostato su fabrikam.com e ActiveUrl è impostato su https://meet.fabrikam.com. Nella seconda istanza, il parametro Component è impostato su Dialin, il dominio su un asterisco (\*) e la proprietà ActiveURL è impostata su https://dialin.fabrikam.com.

Dopo aver creato gli URL e averli memorizzati nei riferimenti oggetto $simpleUrl e $simpleUrl2, l'ultimo comando nell'esempio consente di aggiungere il nuovo URL alla raccolta di URL semplificati per il sito Redmond. Per ottenere questo risultato viene utilizzato il cmdlet **Set-CsSimpleUrlConfiguration**, il parametro SimpleUrl e il valore del parametro @{Add=$simpleUrl, $simpleUrl2}. Questa sintassi fa in modo che gli URL memorizzati nei riferimenti oggetto $simpleUrl e $simpleUrl2 vengano aggiunti alla proprietà SimpleUrl.

    $urlEntry = New-CsSimpleUrlEntry -Url "https://meet.fabrikam.com"
    $urlEntry2 = New-CsSimpleUrlEntry -Url "https://dialin.fabrikam.com"
    
    $simpleUrl = New-CsSimpleUrl -Component "meet" -Domain "fabrikam.com" -SimpleUrlEntry $urlEntry -ActiveUrl "https://meet.fabrikam.com"
    $simpleUrl2 = New-CsSimpleUrl -Component "dialin" -Domain "*" -SimpleUrlEntry $urlEntry -ActiveUrl "https://dialin.fabrikam.com"
    
    Set-CsSimpleUrlConfiguration -Identity "site:Redmond" -SimpleUrl @{Add=$simpleUrl, $simpleUrl2}

## Descrizione dettagliata

In Microsoft Office Communications Server 2007 R2, per le riunioni si utilizzavano URL simili al seguente:

https://imdf.litwareinc.com/Join?uri=sip%3Akenmyer%40litwareinc.com%3Bgruu%3Bopaque%3Dapp%3Aconf%3Afocus%3Aid%3A125f95a0b0184dcea706f1a0191202a8\&key=EcznhLh5K5t

Tuttavia, URL di questo tipo non sono particolarmente intuitivi e facili da comunicare ad altri utenti. Gli URL semplificati introdotti in Lync Server 2010 risolvono questo tipo di problema mettendo a disposizione degli utenti degli URL simili al seguente:

https://meet.litwareinc.com/kenmyer/071200

Gli URL semplificati rappresentano un evidente miglioramento rispetto agli URL utilizzati in Office Communications Server. Tenere presente che gli URL semplificati non vengono creati automaticamente, ma devono essere configurati dall'utente. Inoltre, è necessario creare i record DNS (Domain Name System) per ciascun URL, configurare regole proxy inverse per gli accessi esterni, aggiungere gli URL semplificati ai certificati Front End Server e così via.

Lync Server consente di creare tre diversi tipi di URL semplificati:

Meet: utilizzato per le riunioni. Occorre avere almeno un URL di tipo Meet per ciascuno dei propri domini SIP.

Admin - Utilizzati per consentire agli amministratori di accedere al Pannello di controllo di Lync Server.

Dialin: utilizzato per le pagine Web delle conferenze telefoniche con accesso esterno.

Gli URL semplici vengono archiviati nelle raccolte di configurazioni di URL semplici. Quando si installa Lync Server, viene creata automaticamente una raccolta globale. È inoltre possibile creare raccolte personalizzate nell'ambito del sito. In questo modo, è possibile utilizzare diversi URL semplici nei singoli siti.

Per aggiungere un URL effettivo a una raccolta di URL semplici, è necessario innanzitutto creare l'URL utilizzando i cmdlet **New-CsSimpleUrl** e **New-CsSimpleUrlEntry**. Il cmdlet **New-CsSimpleUrlEntry** consente di creare una voce URL: un URL (ad esempio, https://meet.litwareinc.com) che può essere utilizzato come URL semplice per riunioni, amministrazione o conferenze telefoniche con accesso esterno. L'oggetto creato dal cmdlet **New-CsSimpleUrlEntry** viene quindi aggiunto alla proprietà SimpleUrlEntry di un nuovo URL semplice. È necessario utilizzare un altro cmdlet per creare l'oggetto, in quanto la proprietà SimpleUrlEntry può contenere diversi URL. Tuttavia, è possibile designare solo uno di questi URL come URL attivo. L'URL attivo rappresenta l'URL effettivo utilizzato per riunioni, amministrazione o conferenze telefoniche con accesso esterno.

Dopo avere creato una voce URL semplificato, utilizzare il cmdlet **New-CsSimpleUrl** per creare nella sola memoria un'istanza di un URL semplificato, definendo alcune impostazioni come il componente (il tipo di URL semplificato), il dominio, l'URL attivo e tutte le voci relative all'URL semplificato. Una volta creato, l'oggetto che rappresenta l'URL semplificato può essere aggiunto a una raccolta nuova o esistente di URL semplificati. Dopo aver aggiornato una raccolta di URL semplificati, è necessario utilizzare il cmdlet **Enable-CsComputer**.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **New-CsSimpleUrlEntry** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets -match "New-CsSimpleUrlEntry"}

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
<td><p><em>Url</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>URL da aggiungere alla proprietà SimpleUrlEntry di un URL semplificato. Ad esempio: -Url &quot;https://meet.litwareinc.com&quot;. Gli URL devono iniziare con il prefisso &quot;https:&quot;.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Il cmdlet **New-CsSimpleUrlEntry** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.SimpleUtl.SimpleUrlEntry.

## Vedere anche

#### Ulteriori risorse

[New-CsSimpleUrl](new-cssimpleurl.md)  
[New-CsSimpleUrlConfiguration](new-cssimpleurlconfiguration.md)

