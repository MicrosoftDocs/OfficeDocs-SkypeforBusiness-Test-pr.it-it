---
title: Get-CsNetworkInterface
TOCTitle: Get-CsNetworkInterface
ms:assetid: 06a5fedf-d87e-4469-9bd6-ad16c1f9a801
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398121(v=OCS.15)
ms:contentKeyID: 49299569
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsNetworkInterface

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce le informazioni sulle interfacce di rete utilizzate nei computer che eseguono i ruoli del server o i servizi Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsNetworkInterface [-Identity <NetworkInterfaceIdentity>] <COMMON PARAMETERS>

    Get-CsNetworkInterface [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-ComputerFqdn <Fqdn>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono restituite informazioni su tutte le interfacce di rete configurate per l'organizzazione.

    Get-CsNetworkInterface

## ESEMPIO 2

Il comando riportato nell'Esempio 2 consente di ottenere le informazioni su una singola interfaccia di rete: l'interfaccia con Identity atl-cs-001.litwareinc.com.com/Primary/1.

    Get-CsNetworkInterface -Identity atl-cs-001.litwareinc.com/Primary/1

## ESEMPIO 3

Nell'Esempio 3 si ottengono le informazioni su tutte le interfacce di rete nel dominio litwareinc.com. Per ottenere questo risultato, viene incluso il parametro Filter insieme al valore "\*.litwareinc.com\*". Il valore del filtro restituisce solo i dati relativi a quelle interfacce la cui identità (Identity) include il valore "litwareinc.com".

    Get-CsNetworkInterface -Filter "*.litwareinc.com*"

## ESEMPIO 4

Nell'esempio 4 vengono restituite informazioni su tutte le interfacce di rete configurate per l'indirizzo IP 192.168.0.240. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsNetworkInterface** senza alcun parametro per restituire una raccolta di tutte le interfacce di rete configurate per l'utilizzo nell'organizzazione. La raccolta così ottenuta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le interfacce in cui la proprietà IPAddress è uguale a 192.168.0.240.

    Get-CsNetworkInterface | Where-Object {$_.IPAddress -eq "192.168.0.240"}

## ESEMPIO 5

Il comando riportato nell'esempio 5 è una variante del comando riportato nell'esempio 4. In questo caso vengono però restituite informazioni per tutte le interfacce di rete configurate per la subnet "192.168.0.\*". A tale scopo, viene recuperata una raccolta di tutte le interfacce di rete, che viene quindi inviata tramite pipe al cmdlet **Where-Object**, che a sua volta seleziona solo le interfacce in cui IPAddress inizia con il valore stringa "192.168.0.".

    Get-CsNetworkInterface | Where-Object {$_.IPAddress -like "192.168.0.*"}

## ESEMPIO 6

Nell'esempio 6 vengono restituite tutte le interfacce di rete configurate per l'accesso esterno. A tale scopo, viene chiamato innanzitutto il cmdlet **Get-CsNetworkInterface** senza alcun parametro. In questo modo viene restituita una raccolta di tutte le interfacce di rete attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo gli elementi in cui la proprietà Interface è uguale a External.

    Get-CsNetworkInterface | Where-Object {$_.Interface -eq "External"}

## Descrizione dettagliata

Per trasmettere le informazioni da un computer a un altro, è necessario che i computer dispongano di interfacce di rete, ovvero connessioni tra un computer e la rete. I computer che eseguono i ruoli del server o i servizi Lync Server devono disporre almeno di un'interfaccia di rete, altrimenti non saranno in grado di comunicare con altri computer. I computer tuttavia possono disporre di più interfacce di rete, ad esempio il server perimetrale (server perimetrale) potrebbe disporre di un'interfaccia per la connessione alla rete interna e di una seconda interfaccia per la connessione a Internet. Il cmdlet **Get-CsNetworkInterface** consente agli amministratori di ottenere informazioni sulle interfacce di rete attualmente in uso nei computer che eseguono i ruoli del server o i servizi Lync Server.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsNetworkInterface** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsNetworkInterface"}

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
<td><p><em>ComputerFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del computer per cui si desidera ottenere informazioni sull'interfaccia di rete. Ad esempio, per ottenere le informazioni sull'interfaccia di rete del computer atl-cs-001.litwareinc.com (e solo per quel computer), utilizzare la seguente sintassi: -ComputerFqdn atl-cs-001.litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare i caratteri jolly per specificare le interfacce di rete da ottenere. Ad esempio, questa sintassi restituisce informazioni sull'interfaccia di rete Primary utilizzata su tutti i computer che eseguono un ruolo del server o un servizio Lync Server: -Filter &quot;*/Primary/*&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.NetworkInterfaceIdentity</p></td>
<td><p>Identificatore univoco dell'interfaccia di rete da ottenere. L'identità (Identity) di un'interfaccia di rete è composta da tre parti:</p>
<p>Il nome di dominio completo del computer (ad esempio, atl-cs-001.litwareinc.com).</p>
<p>Il &quot;lato&quot; dell'interfaccia di rete (Primary; Internal; External; PSTN). Il lato indica il tipo di traffico per cui viene utilizzata la porta.</p>
<p>Il numero dell'interfaccia di rete per il lato specifico.</p>
<p>Ad esempio: -Identity &quot;atl-cs-001.litwareinc.com/Primary/1&quot;.</p>
<p>I parametri Identity, ComputerFqdn e Filter devono essere utilizzati separatamente; ad esempio, non è possibile eseguire un comando che utilizza sia ComputerFqdn che Identity. Inoltre, non è possibile utilizzare i caratteri jolly per specificare l'identità (Identity). Per utilizzare i caratteri jolly, è necessario utilizzare il parametro Filter.</p>
<p>Se i parametri Identity, ComputerFqdn o Filter non vengono utilizzati, il cmdlet <strong>Get-CsNetworkInterface</strong> restituisce informazioni su tutte le interfacce di rete attualmente in uso nei computer che eseguono un ruolo del server o servizio di Lync Server.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsNetworkInterface** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsNetworkInterface** restituisce un'istanza dell'oggetto Microsoft.Rtc.Management.Xds.DisplayNetworkInterface.

## Vedere anche

#### Ulteriori risorse

[Get-CsComputer](get-cscomputer.md)

