---
title: Get-CsRgsHolidaySet
TOCTitle: Get-CsRgsHolidaySet
ms:assetid: eef7c046-088f-4334-808a-9036470919b1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412983(v=OCS.15)
ms:contentKeyID: 49302391
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsRgsHolidaySet

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui set di festività di Response Group configurati per l'utilizzo nell'organizzazione. Un set di festività di Response Group è una raccolta di festività. È ad esempio possibile disporre di un set di festività per una coda per gli Stati Uniti (ovvero un set che può includere la festività del 4 luglio) e un set diverso per una coda per la Francia. Quest'ultima coda può definire una festività per la presa della Bastiglia, ma non per il 4 luglio. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsRgsHolidaySet [-Identity <RgsIdentity>] [-Name <String>] [-Owner <RgsIdentity>] [-ShowAll <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono restituite informazioni su tutti i set di festività configurati per l'utilizzo nell'organizzazione.

    Get-CsRgsHolidaySet

## ESEMPIO 2

Il comando mostrato nell'esempio 2 restituisce informazioni su tutti i set di festività configurati per il servizio ApplicationServer:atl-cs-001.litwareinc.com.

    Get-CsRgsHolidaySet -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com"

## ESEMPIO 3

Nell'esempio 3 viene restituito un solo set di festività del servizio ApplicationServer:atl-cs-001.litwareinc.com, ovvero il set denominato "2013 Holidays". Poiché i nomi devono essere univoci per ogni servizio, questo comando non restituirà mai più di un elemento.

    Get-CsRgsHolidaySet -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "2013 Holidays"

## ESEMPIO 4

Nell'esempio 4 vengono visualizzate informazioni dettagliate sulle festività del set "2013 Holidays" trovato nel servizio ApplicationServer:atl-cs-001.litwareinc.com. A tale scopo, viene innanzitutto utilizzato il comando **Get-CsRgsHolidaySet** per recuperare il set di festività specificato. Il set viene quindi passato al cmdlet **Select-Object**, che utilizza il parametro ExpandProperty per visualizzare informazioni dettagliate per ogni festività presente nel set.

    Get-CsRgsHolidaySet -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "2013 Holidays"| Select-Object -ExpandProperty HolidayList

## ESEMPIO 5

Il comando mostrato nell'esempio 5 restituisce l'identità di ogni set di festività presente in ApplicationServer:atl-cs-001.litwareinc.com che include una festività denominata Christmas Day. A tale scopo, nel comando viene innanzitutto chiamato **Get-CsRgsHolidaySet** per restituire una raccolta di tutti i set di festività trovati in ApplicationServer:atl-cs-001.litwareinc.com. Questa raccolta viene quindi inviata tramite pipe a **Select-Object**, che esegue due operazioni, ovvero seleziona la proprietà Identity ed espande la proprietà HolidayList.

Queste due informazioni, Identity e il valore espanso della proprietà HolidayList, vengono quindi inviate tramite pipe al cmdlet **Where-Object**, che a sua volta seleziona solo gli elementi in cui il nome della festività è uguale a Christmas Day. La raccolta filtrata viene infine inviata tramite pipe al cmdlet **ForEach-Object**. Tale cmdlet individua ogni identità presente nella raccolta e per ciascuna utilizza **Get-CsRgsHolidaySet** per recuperare il set di festività corrispondente. Il risultato è un elenco di tutti i set di festività che includano la festività Christmas Day.

    Get-CsRgsHolidaySet -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" | Select-Object Identity -ExpandProperty HolidayList | Where-Object {$_.Name -eq "Christmas Day"} | ForEach-Object {Get-CsRgsHolidaySet -Identity $_.Identity}

## Descrizione dettagliata

Allo scopo di garantire ai chiamanti la migliore esperienza di utilizzo possibile, l'applicazione Response Group consente di stabilire chiaramente quando gli agenti di Response Group sono disponibili per rispondere alle chiamate e quando non lo sono. Con l'applicazione Response Group, è infatti possibile definire gli orari d'ufficio, che indicano i giorni della settimana e le ore del giorno in cui gli agenti sono a disposizione per rispondere alle chiamate. Ad esempio, se l'organizzazione è aperta in genere dal lunedì al venerdì dalle 09.00 alle 17.00, sarà possibile configurare gli orari d'ufficio in maniera tale che indichino che gli agenti sono disponibili dal lunedì al venerdì dalle 09.00 alle 17.00 e, di conseguenza, che non sono disponibili il giovedì alle 20.00 o la domenica alle 14.30.

In molte organizzazioni vi sono tuttavia eccezioni alla settimana lavorativa tipica. Negli Stati Uniti, ad esempio, un'organizzazione può essere chiusa a Natale o durante il Giorno del Ringraziamento. Per gestire tali chiusure atipiche, l'applicazione Response Group consente di designare come festività determinati giorni, ovvero giorni in cui l'organizzazione sarebbe in genere aperta ma che, per qualche ragione, in questo caso non lo è. Le singole festività (create utilizzando il cmdlet **New-CsRgsHoliday**) sono raccolte in set di festività. Le festività relative agli Stati Uniti, ad esempio, possono essere raccolte in un set denominato US\_Holidays, mentre le festività relative al Giappone in un set denominato Japanese\_Holidays. Una volta raccolti, i set di festività possono essere assegnati ai flussi di lavoro di Response Group.

Il cmdlet **Get-CsRgsHolidaySet** consente di restituire informazioni sui set di festività di Response Group configurati per l'utilizzo nell'organizzazione.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsRgsHolidaySet** i membri dei seguenti gruppi: RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsRgsHolidaySet"}

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
<td><p>Rappresenta l'identità del servizio in cui è ospitato il set di festività o l'identità completa del set di festività. Se si specifica l'identità del servizio (ad esempio, service:ApplicationServer:atl-cs-001.litwareinc.com), verranno restituiti tutti i set di festività ospitati nel servizio. Se si specifica l'identità del set di festività, verrà restituito solo il set specificato. L'identità di un set di festività è costituita dall'identità del servizio seguita da un identificatore univoco globale (GUID), ad esempio service:ApplicationServer:atl-cs-001.litwareinc.com /1987d3c2-4544-489d-bbe3-59f79f530a83.</p>
<p>Un modo alternativo per restituire un singolo set di festività consiste nello specificare l'identità del servizio e nell'includere il parametro Name e il nome del set di festività. Ciò consente di recuperare un set di festività specifico senza conoscere il GUID assegnato al set stesso.</p>
<p>Se chiamato senza alcun parametro, <strong>Get-CsRgsHolidaySet</strong> restituirà una raccolta di tutti i set di festività configurati per l'utilizzo nell'organizzazione.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome univoco assegnato al set di festività nel momento stesso in cui il gruppo è stato creato.</p></td>
</tr>
<tr class="odd">
<td><p><em>Owner</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>Nome di dominio completo del pool &quot;proprietario&quot; del set di festività. L'ID del pool proprietario e l'ID del pool di un set di festività in genere coincidono. Se tuttavia è necessario spostare temporaneamente un set di festività, ad esempio in una procedura di ripristino di emergenza, l'ID del pool cambia. L'ID del proprietario invece continuerà a puntare al pool originale.</p></td>
</tr>
<tr class="even">
<td><p><em>ShowAll</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se specificato, mostra tutti i set di festività di Response Group, inclusi quelli in cui l'ID del pool proprietario e l'ID del pool sono diversi. Per impostazione predefinita, Get-CsRgsHolidaySet restituisce informazioni solo sui set di festività in cui l'ID del pool proprietario e l'ID del pool sono identici.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. **Get-CsRgsHolidaySet** non accetta l'input da pipeline.

## Tipi restituiti

**Get-CsRgsHolidaySet** restituisce istanze dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.HolidaySet.

## Vedere anche

#### Ulteriori risorse

[New-CsRgsHolidaySet](new-csrgsholidayset.md)  
[Remove-CsRgsHolidaySet](remove-csrgsholidayset.md)  
[Set-CsRgsHolidaySet](set-csrgsholidayset.md)

