---
title: Get-CsSite
TOCTitle: Get-CsSite
ms:assetid: 0e5fd5b8-17aa-433d-9915-3b88281fa2c2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398185(v=OCS.15)
ms:contentKeyID: 49299682
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsSite

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui siti creati come parte dell'infrastruttura di Lync Server. I siti rappresentano una raccolta di pool di Lync Server e generalmente sono dislocati in diverse aree geografiche. Lync Server include due tipi di siti: siti data center e siti remoti (siti di succursale). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsSite [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsSite [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS:

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono recuperate informazioni su tutti i siti di Lync Server.

    Get-CsSite

## ESEMPIO 2

Nell'esempio 2, vengono restituite le informazioni su un singolo sito: il sito con Identity Redmond.

    Get-CsSite -Identity "Redmond"

## ESEMPIO 3

Il comando riportato nell'esempio 3 restituisce le informazioni sul sito centrale. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsSite** per restituire una raccolta di tutti i siti configurati per l'utilizzo nell'organizzazione. La raccolta così ottenuta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona l'unico sito in cui la proprietà SiteType è uguale a "CentralSite".

    Get-CsSite | Where-Object {$_.SiteType -eq "CentralSite"}

## ESEMPIO 4

Nell'esempio 4 viene visualizzato l'elenco dei pool che si trovano nel sito Redmond. A tale scopo, il comando innanzitutto recupera le informazioni complete sul sito Redmond e quindi invia tramite pipe i dati al cmdlet **Select-Object**. A sua volta, il cmdlet **Select-Object** utilizza il parametro ExpandProperty per "espandere" il valore della proprietà Pools. L'espansione del valore di una proprietà significa che tutti i valori archiviati in tale proprietà verranno visualizzati in un formato facilmente leggibile.

    Get-CsSite -Identity "Redmond" | Select-Object -ExpandProperty Pools

## Descrizione dettagliata

Con Lync Server 2010 è stato introdotto un nuovo concetto nella topologia di Lync Server: i siti. I siti (che non devono essere confusi con i siti Active Directory o Microsoft Exchange Server) sono una raccolta di server e pool di Lync Server generalmente organizzati in base all'area geografica e alla larghezza di banda della rete. Se ad esempio a Redmond tutti i computer si trovano sulla stessa rete LAN con connessioni a bassa latenza ed elevata velocità, è possibile specificare un sito Redmond che includa tutti questi computer. Allo stesso modo, se i computer di Dublino si trovano su una propria LAN e condividono le connessioni ad alta velocità e bassa latenza, si potrebbe creare un sito Dublino a sé stante. I siti svolgono un ruolo chiave nella gestione di Lync Server: molti criteri e impostazioni possono essere configurati nell'ambito del sito semplificando in modo significativo operazioni quali l'applicazione di un set di dial plan agli utenti di Redmond e di un set completamente diverso di dial plan agli utenti di Dublino.

Il cmdlet **Get-CsSite** consente di ottenere le informazioni su tutti i siti dell'organizzazione, inclusi i dati sui pool che costituiscono ciascuno di questi siti.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsSite** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsSite"}

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
<td><p>Consente di utilizzare i caratteri jolly per specificare l'identità del sito (o dei siti) da ottenere. Ad esempio, questa sintassi restituisce tutti i pool la cui identità include la stringa &quot;Dublin&quot;: -Filter &quot;*Dublin*&quot;.</p>
<p>Si noti che non è possibile utilizzare entrambi i parametri Filter e Identity nello stesso comando.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Il nome del sito da ottenere. Si noti che basta specificare il nome del sito; ad esempio: -Identity &quot;Redmond&quot;. Non utilizzare il formato &quot;site:Redmond&quot; per specificare l'identità.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsSite** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsSite** restituisce istanze dell'oggetto Microsoft.Rtc.Management.Deploy.Internal.Site+CentralSite.

## Vedere anche

#### Ulteriori risorse

[Set-CsSite](set-cssite.md)

