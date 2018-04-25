---
title: Set-CsRgsHoursOfBusiness
TOCTitle: Set-CsRgsHoursOfBusiness
ms:assetid: be976e84-00aa-46d5-94d3-527c4c9f3963
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412929(v=OCS.15)
ms:contentKeyID: 49301838
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsRgsHoursOfBusiness

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Configura un insieme esistente di orari di ufficio di Response Group. Gli insiemi di orari di ufficio sono utilizzati per indicare i giorni della settimana e le ore del giorno in cui gli agenti di Response Group sono in genere disponibili per rispondere alle chiamate telefoniche. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsRgsHoursOfBusiness -Instance <BusinessHours> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene mostrato che è possibile assegnare un nuovo valore di intervallo di tempo alle proprietà SaturdayHours1 e SundayHours1 dell'insieme di orari di ufficio Help Desk Business Hours. A tale scopo, nel primo comando dell'esempio viene utilizzato **New-CsRgsTimeRange** per creare un nuovo oggetto intervallo di tempo (Weekend Hours) con orario di apertura alle 12.00 (12:00) e orario di chiusura alle 17.00 (17:00). L'oggetto viene archiviato in una variabile denominata $weekend.

Il prossimo comando crea un riferimento oggetto ($x) nell'insieme di orari d'ufficio del supporto tecnico su ApplicationServer:atl-cs-001.litwareinc.com. Al termine dell'esecuzione di questo comando, vengono utilizzati il terzo e il quarto comando per impostare le proprietà SaturdayHours1 e SundayHours1 sul valore di intervallo di tempo archiviato in $weekend. Nell'ultimo comando dell'esempio viene infine utilizzato **Set-CsRgsHoursOfBusiness** per scrivere tali modifiche nell'insieme di orari d'ufficio effettivo.

    $weekend = New-CsRgsTimeRange -Name "Weekend Hours" -OpenTime "12:00" -CloseTime "17:00"
    
    $x = Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "Help Desk Business Hours"
    $x.SaturdayHours1 = $weekend
    $x.SundayHours1 = $weekend
    Set-CsRgsHoursOfBusiness -Instance $x

## ESEMPIO 2

I comandi mostrati nell'esempio 2 eliminano i valori configurati per le proprietà SaturdayHours1 e SaturdayHours2 nell'insieme di orari d'ufficio Help Desk Business Hours. Per effettuare questa operazione, il primo comando crea un riferimento oggetto ($x) nell'insieme di orari d'ufficio Help Desk Business Hours su ApplicationServer:atl-cs-001.litwareinc.com. Dopo la creazione del riferimento oggetto, il secondo comando imposta la proprietà SaturdayHours1 su un valore null ($Null) e cancella concretamente ogni valore precedentemente assegnato a SaturdayHours1. Viene quindi utilizzato un comando analogo per cancellare qualsiasi valore precedentemente assegnato a SaturdayHours2.

Nel comando finale dell'esempio viene quindi utilizzato **Set-CsRgsHoursOfBusiness** per scrivere tali modifiche nell'insieme di orari d'ufficio effettivo. Al termine dell'esecuzione di questo comando, a Help Desk Business Hours non saranno più assegnati orari d'ufficio per il sabato.

    $x = Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "Help Desk Business Hours"
    $x.SaturdayHours1 = $Null
    $x.SaturdayHours2 = $Null
    
    Set-CsRgsHoursOfBusiness -Instance $x

## Descrizione dettagliata

Allo scopo di garantire ai chiamanti la migliore esperienza di utilizzo possibile, l'applicazione Response Group consente di stabilire chiaramente quando gli agenti di Response Group sono disponibili per rispondere alle chiamate e quando non lo sono. Con l'applicazione Response Group, è infatti possibile definire gli orari d'ufficio, che indicano i giorni della settimana e le ore del giorno in cui gli agenti sono a disposizione per rispondere alle chiamate. Ad esempio, se l'organizzazione è aperta in genere dal lunedì al venerdì dalle 09.00 alle 17.00, sarà possibile configurare gli orari d'ufficio in maniera tale che indichino che gli agenti sono disponibili dal lunedì al venerdì dalle 09.00 alle 17.00 e, di conseguenza, che non sono disponibili il giovedì alle 20.00 o la domenica alle 14.30.

È possibile creare insiemi di orari d'ufficio utilizzando il cmdlet **New-CsRgsHoursOfBusiness**. Dopo essere stati creati, questi insiemi possono essere modificati utilizzando il cmdlet **Set-CsRgsHoursOfBusiness**. In genere, ciò comporta la modifica degli orari d'ufficio per uno o più giorni della settimana. Ad esempio, se il supporto tecnico di venerdì era aperto fino alle 17.00 ma ora resta aperto fino alle 19.00, sarà necessario modificare gli orari d'ufficio relativi al venerdì. Se il supporto tecnico di sabato restava aperto ma adesso è chiuso, sarà ugualmente necessario modificare gli orari d'ufficio relativi al sabato. Per indicare che un gruppo non è disponibile in un determinato giorno, è sufficiente impostare gli orari d'ufficio per quel giorno su un valore Null: -SundayTimeRange1 $Null.)

Quando si configurano gli orari d'ufficio all'interno di un insieme di orari d'ufficio, ricordare che ogni giorno della settimana ha sia la proprietà Hours1 che la proprietà Hours2. Se il supporto tecnico è aperto dalle 08.00 alle 17.00, sarà necessario semplicemente assegnare i valori alla proprietà Hours1 appropriata. Si supponga invece che il supporto tecnico sia aperto dalle 08.00 alle 14.00 e quindi dalle 17.00 alle 23.00. In questo caso, sarà necessario assegnare l'intervallo dalle 08.00 alle 14.00 a Hours1 e quello dalle 17.00 alle 23.00 a Hours2.

**Set-CsRgsHoursOfBusiness** non modifica direttamente un insieme di orari d'ufficio. È invece necessario utilizzare **Get-CsRgsHoursOfBusiness** per creare un riferimento oggetto all'insieme da modificare. Quando si crea un riferimento oggetto, si recupera una copia dell'insieme di orari d'ufficio e la si archivia in una variabile. Dopo avere creato un riferimento oggetto, è possibile modificare le proprietà di tale oggetto solo in memoria. Dopo aver apportato le modifiche desiderate, è possibile utilizzare **Set-CsRgsHoursOfBusiness** per scrivere queste modifiche nell'insieme di orari d'ufficio effettivo.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsRgsHoursOfBusiness** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsRgsHoursOfBusiness"}

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
<td><p><em>Instance</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.BusinessHours</p></td>
<td><p>Riferimento oggetto per l'insieme di orari d'ufficio da modificare. Un riferimento oggetto in genere viene recuperato utilizzando il cmdlet <strong>Get-CsRgsHoursOfBusiness</strong> e assegnando il valore restituito a una variabile. Questo comando ad esempio restituisce un riferimento oggetto all'insieme di orari d'ufficio Help Desk e archivia tale riferimento in una variabile denominata $x:</p>
<p>$x = Get-CsRgsHoursOfBusiness -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name &quot;Help Desk&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
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

Oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.BusinessHours. **Set-CsRgsHoursOfBusiness** accetta le istanze da pipeline dell'oggetto orari d'ufficio di Response Group.

## Tipi restituiti

Modifica istanze esistenti dell'oggetto Microsoft.Rtc.Rgs.Management.WriteableSettings.BusinessHours.

## Vedere anche

#### Ulteriori risorse

[Get-CsRgsHoursOfBusiness](get-csrgshoursofbusiness.md)  
[New-CsRgsHoursOfBusiness](new-csrgshoursofbusiness.md)  
[New-CsRgsTimeRange](new-csrgstimerange.md)  
[Remove-CsRgsHoursOfBusiness](remove-csrgshoursofbusiness.md)

