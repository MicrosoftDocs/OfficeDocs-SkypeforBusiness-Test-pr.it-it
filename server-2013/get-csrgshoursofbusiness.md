---
title: Get-CsRgsHoursOfBusiness
TOCTitle: Get-CsRgsHoursOfBusiness
ms:assetid: 2008d55c-fd53-4004-b6e6-08cdf0175af8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398284(v=OCS.15)
ms:contentKeyID: 49299898
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsRgsHoursOfBusiness

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera informazioni sulle raccolte di orari d'ufficio di Response Group configurate per l'utilizzo nell'organizzazione. Le raccolte degli orari d'ufficio sono utilizzate per indicare i giorni della settimana e le ore del giorno in cui gli agenti di Response Group sono in genere disponibili per rispondere alle chiamate telefoniche. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsRgsHoursOfBusiness [-Identity <RgsIdentity>] [-Name <String>] [-Owner <RgsIdentity>] [-ShowAll <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono restituite informazioni su tutte le raccolte di orari d'ufficio configurate per l'utilizzo nell'organizzazione. A tale scopo, viene chiamato **Get-CsRgsHoursOfBusiness** senza alcun parametro.

    Get-CsRgsHoursOfBusiness

## ESEMPIO 2

Il comando mostrato nell'esempio 2 restituisce tutte le raccolte di orari d'ufficio configurate per l'utilizzo in atl-cs-001.litwareinc.com.

    Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com"

## ESEMPIO 3

Nell'esempio 3 viene restituita una singola raccolta di orari d'ufficio da atl-cs-001.litwareinc.com, ovvero la raccolta con nome "Help Desk Business Hours".

    Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "Help Desk Business Hours"

## ESEMPIO 4

Il comando illustrato nell'esempio 4 restituisce tutte le raccolte di orari d'ufficio che hanno orari d'ufficio configurati per la domenica. A tale scopo, nel comando viene innanzitutto chiamato **Get-CsRgsHoursOfBusiness** per restituire tutte le raccolte di orari d'ufficio trovate in atl-cs-001.litwareinc.com. Questi dati vengono quindi inviati tramite pipe al cmdlet **Where-Object**, che seleziona solo gli elementi per cui si verifica una delle due condizioni seguenti: la proprietà SundayTimeRange1 non è uguale a un valore Null e/o la proprietà SundayTimeRange2 non è uguale a un valore Null. Se una proprietà relativa a un intervallo di tempo non è Null, significa che per tale intervallo di tempo sono stati configurati orari d'ufficio.

    Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" | Where-Object {$_.SundayTimeRange1 -ne $Null -or $_.SundayTimeRange2 -ne $Null}

## ESEMPIO 5

Il comando mostrato nell'esempio 5 restituisce tutte le raccolte di orari d'ufficio di atl-cs-001.litwareinc.com in cui l'orario di apertura per la proprietà MondayTimeRange1 è uguale o antecedente alle 08.00 (08:00:00). A tale scopo, nel comando viene innanzitutto utilizzato **Get-CsRgsHoursOfBusiness** per restituire tutte le raccolte di orari d'ufficio di atl-cs-001.litwareinc.com. Questi dati vengono quindi inviati tramite pipe al cmdlet **Where-Object**, che seleziona solo le raccolte in cui il valore della proprietà MondayTimeRange1.OpenTime è minore o uguale alle 08.00 (08:00:00).

    Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" | Where-Object {$_.MondayTimeRange1.OpenTime -le "08:00:00"}

## ESEMPIO 6

Il comando mostrato nell'esempio 6 restituisce tutte le raccolte di orari d'ufficio pubbliche, ovvero le raccolte che possono essere condivise tra flussi di lavoro. A tale scopo, nel comando viene innanzitutto utilizzato **Get-CsRgsHoursOfBusiness** per restituire tutte le raccolte di orari d'ufficio trovate in atl-cs-001.litwareinc.com. Questi dati vengono quindi inviati tramite pipe al cmdlet **Where-Object**, che seleziona solo le raccolte in cui la proprietà Custom è uguale a False.

    Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" | Where-Object {$_.Custom -eq $False}

## Descrizione dettagliata

Allo scopo di garantire ai chiamanti la migliore esperienza di utilizzo possibile, l'applicazione Response Group consente di stabilire chiaramente quando gli agenti di Response Group sono disponibili per rispondere alle chiamate e quando non lo sono. Con l'applicazione Response Group, è infatti possibile definire gli orari d'ufficio, che indicano i giorni della settimana e le ore del giorno in cui gli agenti sono a disposizione per rispondere alle chiamate. Ad esempio, se l'organizzazione è aperta in genere dal lunedì al venerdì dalle 09.00 alle 17.00, sarà possibile configurare gli orari d'ufficio in maniera tale che indichino che gli agenti sono disponibili dal lunedì al venerdì dalle 09.00 alle 17.00 e, di conseguenza, che non sono disponibili il giovedì alle 20.00 o la domenica alle 14.30.

Il cmdlet **Get-CsRgsHoursOfBusiness** consente di recuperare informazioni sulle raccolte di orari d'ufficio configurate per l'utilizzo nell'organizzazione.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsRgsHoursOfBusiness** i membri dei seguenti gruppi: RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsRgsHoursOfBusiness"}

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
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>Rappresenta l'identità del servizio in cui è ospitata la raccolta degli orari d'ufficio o l'identità completa della stessa raccolta. Se si specifica l'identità del servizio (ad esempio, service:ApplicationServer:atl-cs-001.litwareinc.com), verranno restituite tutte le raccolte di orari d'ufficio ospitate nel servizio. Se si specifica l'identità della raccolta, verrà restituita solo la raccolta di orari d'ufficio specificata. Si noti che l'identità di una raccolta di orari d'ufficio è costituita dall'identità del servizio seguita da un identificatore univoco globale (GUID), ad esempio service:ApplicationServer-1/1987d3c2-4544-489d-bbe3-59f79f530a83.</p>
<p>Un modo alternativo per restituire una raccolta di orari d'ufficio consiste nello specificare l'identità del servizio e nell'includere il parametro Name e il nome della raccolta. In questo modo è possibile recuperare una specifica raccolta di orari d'ufficio senza conoscere il GUID assegnato alla raccolta stessa.</p>
<p>Se chiamato senza alcun parametro, <strong>Get-CsRgsHoursOfBusiness</strong> restituirà tutte le raccolte di orari d'ufficio configurate per l'utilizzo nell'organizzazione.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome univoco assegnato alla raccolta degli orari d'ufficio nel momento stesso in cui la raccolta è stata creata.</p></td>
</tr>
<tr class="odd">
<td><p><em>Owner</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>Nome di dominio completo del pool &quot;proprietario&quot; degli orari d'ufficio. L'ID del pool proprietario e l'ID del pool di una raccolta di orari d'ufficio in genere coincidono. Se tuttavia è necessario spostare temporaneamente una raccolta, ad esempio in una procedura di ripristino di emergenza, l'ID del pool cambia. L'ID del proprietario invece continuerà a puntare al pool originale.</p></td>
</tr>
<tr class="even">
<td><p><em>ShowAll</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se specificato, mostra tutte le raccolte di orari d'ufficio di Response Group, incluse quelle in cui l'ID del pool proprietario e l'ID del pool sono diversi. Per impostazione predefinita, Get-CsRgsHoursOfBusiness restituisce informazioni solo sulle raccolte di orari d'ufficio in cui l'ID del pool proprietario e l'ID del pool sono identici.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. **Get-CsRgsHoursOfBusiness** non accetta l'input da pipeline.

## Tipi restituiti

Restituisce istanze dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.BusinessHours.

## Vedere anche

#### Ulteriori risorse

[New-CsRgsHoursOfBusiness](new-csrgshoursofbusiness.md)  
[Remove-CsRgsHoursOfBusiness](remove-csrgshoursofbusiness.md)  
[Set-CsRgsHoursOfBusiness](set-csrgshoursofbusiness.md)

