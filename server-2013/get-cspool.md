---
title: Get-CsPool
TOCTitle: Get-CsPool
ms:assetid: e0911c68-9a0a-461a-88d6-c610c6cd996c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398992(v=OCS.15)
ms:contentKeyID: 49302235
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPool

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui pool utilizzati nella distribuzione di Lync Server. I pool sono una raccolta di computer di un sito che eseguono lo stesso insieme di servizi di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsPool [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsPool [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Site <String>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono restituiti tutti i pool presenti nella distribuzione di Lync Server.

    Get-CsPool

## ESEMPIO 2

Nell'esempio 2 vengono visualizzate informazioni dettagliate sui computer presenti in ciascun pool. A tale scopo, viene chiamato il cmdlet **Get-CsPool**, quindi i dati restituiti vengono inviati tramite pipe al cmdlet **Select-Object**. Il parametro ExpandProperty viene quindi utilizzato per espandere il valore della proprietà Computers. Tale proprietà è una matrice di oggetti che rappresentano i singoli computer del pool. Quando si espande la proprietà Computers, vengono visualizzate informazioni dettagliate su ogni computer.

    Get-CsPool | Select-Object -ExpandProperty Computers

## ESEMPIO 3

Nell'esempio 3 il parametro Identity viene utilizzato per limitare i dati restituiti al pool con identità atl-cs-001.litwareinc.com.

    Get-CsPool -Identity atl-cs-001.litwareinc.com

## ESEMPIO 4

Con l'esempio 4 vengono restituiti tutti i pool presenti nel sito Redmond. A tale scopo, nel comando viene utilizzato il parametro Site. Il valore "Redmond" del parametro consente di limitare i dati restituiti ai pool la cui proprietà Site è uguale a Redmond.

    Get-CsPool -Site "Redmond"

## ESEMPIO 5

Il comando mostrato nell'esempio 5 restituisce una raccolta di tutti i pool in cui non è installato alcun servizio Lync Server. Per eseguire questa attività, nel comando viene innanzitutto chiamato il cmdlet **Get-CsPool** senza alcun parametro per restituire una raccolta di tutti i pool attualmente in uso nell'organizzazione. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona tutti i pool in cui la proprietà Services.Count è uguale a 0. Il conteggio (Count) uguale a 0 indica che per il pool non sono configurati servizi Lync Server.

    Get-CsPool | Where-Object {$_.Services.Count -eq 0}

## Descrizione dettagliata

In Lync Server un pool è costituito da uno o più computer dello stesso sito che eseguono lo stesso insieme di servizi. Se ad esempio nel sito Redmond vi è un solo server che esegue il servizio Mediation Server, si disporrà di un pool Mediation Server costituito da tale computer. Se invece nel sito Redmond vi sono due computer che eseguono il servizio Mediation Server, si disporrà di un pool Mediation Server costituito da due computer. Il numero di pool utilizzati nell'organizzazione dipende dal numero di server disponibili e dai diversi servizi eseguiti da tali server.

Il cmdlet **Get-CsPool** consente di recuperare informazioni su ogni pool in uso nell'organizzazione, incluse le informazioni sui servizi eseguiti in ciascuno di essi.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsPool** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPool"}

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare i caratteri jolly per specificare il valore Identity del pool (o dei pool) in questione. Ad esempio, con la sintassi seguente vengono restituiti tutti i pool il cui valore Identity termina con il valore stringa &quot;.fabrikam.com&quot;: -Filter &quot;*.fabrikam.com&quot;.</p>
<p>Si noti che non è possibile utilizzare i parametri Filter e Identity nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nome di dominio completo (FQDN) del pool da restituire. Ad esempio: -Identity atl-cs-001.litwareinc.com.</p>
<p>Se questo parametro non è presente, verranno restituiti tutti i pool presenti nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>Site</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di restituire tutti i pool presenti nel sito specificato. È necessario fare riferimento al sito in questione mediante il relativo valore DisplayName (ad esempio, Redmond) anziché mediante il relativo valore Identity (ad esempio, site:Redmond). Ad esempio: -Site &quot;Redmond&quot;. È possibile recuperare i nomi visualizzati dei siti eseguendo questo comando:</p>
<p>Get-CsSite | Select-Object Identity, DisplayName</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsPool** non accetta input inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsPool** restituisce istanze dell'oggetto Microsoft.Rtc.Management.Deploy.Internal.Cluster.

## Vedere anche

#### Ulteriori risorse

[Get-CsSite](get-cssite.md)  
[Get-CsTopology](get-cstopology.md)

