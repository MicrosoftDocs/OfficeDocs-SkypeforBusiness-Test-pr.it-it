---
title: New-CsRgsHoursOfBusiness
TOCTitle: New-CsRgsHoursOfBusiness
ms:assetid: 21869ba6-526e-4c70-b84d-de73536d8a43
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398291(v=OCS.15)
ms:contentKeyID: 49299916
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRgsHoursOfBusiness

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo insieme di orari d'ufficio dell'applicazione Response Group. Gli insiemi degli orari d'ufficio sono utilizzati per indicare i giorni della settimana e le ore del giorno in cui gli agenti di Response Group sono in genere disponibili per rispondere alle chiamate telefoniche. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsRgsHoursOfBusiness -Name <String> -Parent <RgsIdentity> [-Confirm [<SwitchParameter>]] [-Custom <$true | $false>] [-Force <SwitchParameter>] [-FridayHours1 <TimeRange>] [-FridayHours2 <TimeRange>] [-InMemory <SwitchParameter>] [-MondayHours1 <TimeRange>] [-MondayHours2 <TimeRange>] [-SaturdayHours1 <TimeRange>] [-SaturdayHours2 <TimeRange>] [-SundayHours1 <TimeRange>] [-SundayHours2 <TimeRange>] [-ThursdayHours1 <TimeRange>] [-ThursdayHours2 <TimeRange>] [-TuesdayHours1 <TimeRange>] [-TuesdayHours2 <TimeRange>] [-WednesdayHours1 <TimeRange>] [-WednesdayHours2 <TimeRange>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 crea in ApplicationServer:atl-cs-001.litwareinc.com un nuovo insieme di orari d'ufficio denominato Help Desk Business Hours. In questo esempio, non ci sono orari d'ufficio configurati per l'insieme.

    New-CsRgsHoursOfBusiness -Parent "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "Help Desk Business Hours" 

## ESEMPIO 2

Nell'esempio 2 viene creato un nuovo insieme di orari d'ufficio denominato Help Desk Business Hours in ApplicationServer:atl-cs-001.litwareinc.com. In questo esempio gli orari d'ufficio vengono configurati per ogni giorno della settimana, dal lunedì al venerdì. A tale scopo, nel primo comando dell'esempio viene utilizzato il cmdlet **New-CsRgsTimeRange** per creare un intervallo di tempo con OpenTime uguale alle 08.00 (8:00) e CloseTime uguale alle 18.00 (18:00). L'intervallo di tempo viene archiviato in una variabile denominata $weekday.

Il secondo comando nell'esempio crea quindi il nuovo insieme di orari d'ufficio. Oltre a specificare l'elemento padre (Parent) e il nome (Name) dell'insieme, è possibile utilizzare i parametri aggiuntivi (come ad esempio MondayHours1) per configurare gli orari d'ufficio relativi ai giorni della settimana dal lunedì al venerdì. In ogni caso, tali orari d'ufficio vengono impostati dalle 08.00 alle 18.00, utilizzando la variabile dell'intervallo di tempo $weekday.

    $weekday = New-CsRgsTimeRange -Name "Weekday Hours" -OpenTime "8:00" -CloseTime "18:00" 
    
    New-CsRgsHoursOfBusiness -Parent "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "Help Desk Business Hours" -MondayHours1 $weekday -TuesdayHours1 $weekday -WednesdayHours1 $weekday -ThursdayHours1 $weekday -FridayHours1 $weekday

## Descrizione dettagliata

Allo scopo di garantire ai chiamanti la migliore esperienza di utilizzo possibile, l'applicazione Response Group consente di stabilire chiaramente quando gli agenti di Response Group sono disponibili per rispondere alle chiamate e quando non lo sono. Con l'applicazione Response Group, è infatti possibile definire gli orari d'ufficio, che indicano i giorni della settimana e le ore del giorno in cui gli agenti sono a disposizione per rispondere alle chiamate. Ad esempio, se l'organizzazione è aperta in genere dal lunedì al venerdì dalle 09.00 alle 17.00, sarà possibile configurare gli orari d'ufficio in maniera tale che indichino che gli agenti sono disponibili dal lunedì al venerdì dalle 09.00 alle 17.00 e, di conseguenza, che non sono disponibili il giovedì alle 20.00 o la domenica alle 14.30.

È possibile creare nuovi insiemi di orari d'ufficio utilizzando il cmdlet **New-CsRgsHoursOfBusiness**. Quando si configurano gli orari d'ufficio di un insieme di orari d'ufficio, tenere presente che ogni giorno della settimana dispone sia della proprietà Hours1 che della proprietà Hours2. Se il supporto tecnico è aperto dalle 08.00 alle 17.00, sarà necessario semplicemente assegnare i valori alla proprietà Hours1 appropriata. Si supponga tuttavia che il supporto tecnico sia aperto dalle 08.00 alle 14.00 e quindi dalle 17.00 alle 23.00. In questo caso, sarà necessario assegnare l'intervallo dalle 08.00 alle 14.00 a Hours1 e quello dalle 17.00 alle 23.00 a Hours2.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsRgsHoursOfBusiness** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsRgsHoursOfBusiness"}

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
<td><p><em>Name</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome univoco da assegnare all'insieme di orari d'ufficio. La combinazione della proprietà Parent e della proprietà Name consente di identificare in modo univoco gli insiemi di orari d'ufficio senza dover fare riferimento all'identificatore univoco globale (GUID) della raccolta.</p></td>
</tr>
<tr class="even">
<td><p><em>Parent</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>Il servizio in cui sarà ospitato il nuovo insieme di orari d'ufficio. Ad esempio: -Parent &quot;service:ApplicationServer:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Custom</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se questo parametro è impostato su True, gli orari d'ufficio potranno essere utilizzati solo dal flusso di lavoro specificato. Se questo parametro è impostato su False (valore predefinito), gli orari d'ufficio potranno essere condivisi tra più flussi di lavoro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>FridayHours1</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>Primo insieme di orari di apertura e chiusura per il venerdì. Se l'organizzazione è aperta il venerdì dalle 09.00 alle 17.00, sarà necessario configurare un solo intervallo di tempo. Se invece l'organizzazione è aperta dalle 08.00 a mezzogiorno, chiude un'ora per pranzo e quindi è di nuovo aperta dalle 13.00 alle 17.00, sarà necessario creare due intervalli di tempo per il venerdì.</p>
<p>Se il venerdì l'organizzazione resta chiusa, non configurare alcun valore per FridayHours1 e per FridayHours2.</p></td>
</tr>
<tr class="odd">
<td><p><em>FridayHours2</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>Secondo insieme di orari di apertura e chiusura per il venerdì. Se l'organizzazione è aperta il venerdì dalle 09.00 alle 17.00, sarà necessario configurare un solo intervallo di tempo. Se invece l'organizzazione è aperta dalle 08.00 a mezzogiorno, chiude un'ora per pranzo e quindi è di nuovo aperta dalle 13.00 alle 17.00, sarà necessario creare due intervalli di tempo per il venerdì.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>MondayHours1</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>Primo insieme di orari di apertura e chiusura per il lunedì. Se l'organizzazione è aperta il lunedì dalle 09.00 alle 17.00, sarà necessario configurare un solo intervallo di tempo. Se invece l'organizzazione è aperta dalle 08.00 a mezzogiorno, chiude un'ora per pranzo e quindi è di nuovo aperta dalle 13.00 alle 17.00, sarà necessario creare due intervalli di tempo per il lunedì.</p>
<p>Se il lunedì l'organizzazione resta chiusa, non configurare alcun valore per MondayHours1 e per MondayHours2.</p></td>
</tr>
<tr class="even">
<td><p><em>MondayHours2</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>Secondo insieme di orari di apertura e chiusura per il lunedì. Se l'organizzazione è aperta il lunedì dalle 09.00 alle 17.00, sarà necessario configurare un solo intervallo di tempo. Se invece l'organizzazione è aperta dalle 08.00 a mezzogiorno, chiude un'ora per pranzo e quindi è di nuovo aperta dalle 13.00 alle 17.00, sarà necessario creare due intervalli di tempo per il lunedì.</p></td>
</tr>
<tr class="odd">
<td><p><em>SaturdayHours1</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>Primo insieme di orari di apertura e chiusura per il sabato. Se l'organizzazione è aperta il sabato dalle 09.00 alle 17.00, sarà necessario configurare un solo intervallo di tempo. Se invece l'organizzazione è aperta dalle 08.00 a mezzogiorno, chiude un'ora per pranzo e quindi è di nuovo aperta dalle 13.00 alle 17.00, sarà necessario creare due intervalli di tempo per il sabato.</p>
<p>Se il sabato l'organizzazione resta chiusa, non configurare alcun valore per SaturdayHours1 e per SaturdayHours2.</p></td>
</tr>
<tr class="even">
<td><p><em>SaturdayHours2</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>Secondo insieme di orari di apertura e chiusura per il sabato. Se l'organizzazione è aperta il sabato dalle 09.00 alle 17.00, sarà necessario configurare un solo intervallo di tempo. Se invece l'organizzazione è aperta dalle 08.00 a mezzogiorno, chiude un'ora per pranzo e quindi è di nuovo aperta dalle 13.00 alle 17.00, sarà necessario creare due intervalli di tempo per il sabato.</p></td>
</tr>
<tr class="odd">
<td><p><em>SundayHours1</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>Primo insieme di orari di apertura e chiusura per la domenica. Se l'organizzazione è aperta la domenica dalle 09.00 alle 17.00, sarà necessario configurare un solo intervallo di tempo. Se invece l'organizzazione è aperta dalle 08.00 a mezzogiorno, chiude un'ora per pranzo e quindi è di nuovo aperta dalle 13.00 alle 17.00, sarà necessario creare due intervalli di tempo per la domenica.</p>
<p>Se la domenica l'organizzazione resta chiusa, non configurare alcun valore per SundayHours1 e per SundayHours2.</p></td>
</tr>
<tr class="even">
<td><p><em>SundayHours2</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>Secondo insieme di orari di apertura e chiusura per la domenica. Se l'organizzazione è aperta la domenica dalle 09.00 alle 17.00, sarà necessario configurare un solo intervallo di tempo. Se invece l'organizzazione è aperta dalle 08.00 a mezzogiorno, chiude un'ora per pranzo e quindi è di nuovo aperta dalle 13.00 alle 17.00, sarà necessario creare due intervalli di tempo per la domenica.</p></td>
</tr>
<tr class="odd">
<td><p><em>ThursdayHours1</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>Primo insieme di orari di apertura e chiusura per il giovedì. Se l'organizzazione è aperta il giovedì dalle 09.00 alle 17.00, sarà necessario configurare un solo intervallo di tempo. Se invece l'organizzazione è aperta dalle 08.00 a mezzogiorno, chiude un'ora per pranzo e quindi è di nuovo aperta dalle 13.00 alle 17.00, sarà necessario creare due intervalli di tempo per il giovedì.</p>
<p>Se il giovedì l'organizzazione resta chiusa, non configurare alcun valore per ThursdayHours1 e per ThursdayHours2.</p></td>
</tr>
<tr class="even">
<td><p><em>ThursdayHours2</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>Secondo insieme di orari di apertura e chiusura per il giovedì. Se l'organizzazione è aperta il giovedì dalle 09.00 alle 17.00, sarà necessario configurare un solo intervallo di tempo. Se invece l'organizzazione è aperta dalle 08.00 a mezzogiorno, chiude un'ora per pranzo e quindi è di nuovo aperta dalle 13.00 alle 17.00, sarà necessario creare due intervalli di tempo per il giovedì.</p></td>
</tr>
<tr class="odd">
<td><p><em>TuesdayHours1</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>Primo insieme di orari di apertura e chiusura per il martedì. Se l'organizzazione è aperta il martedì dalle 09.00 alle 17.00, sarà necessario configurare un solo intervallo di tempo. Se invece l'organizzazione è aperta dalle 08.00 a mezzogiorno, chiude un'ora per pranzo e quindi è di nuovo aperta dalle 13.00 alle 17.00, sarà necessario creare due intervalli di tempo per il martedì.</p>
<p>Se il martedì l'organizzazione resta chiusa, non configurare alcun valore per TuesdayHours1 e per TuesdayHours2.</p></td>
</tr>
<tr class="even">
<td><p><em>TuesdayHours2</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>Secondo insieme di orari di apertura e chiusura per il martedì. Se l'organizzazione è aperta il martedì dalle 09.00 alle 17.00, sarà necessario configurare un solo intervallo di tempo. Se invece l'organizzazione è aperta dalle 08.00 a mezzogiorno, chiude un'ora per pranzo e quindi è di nuovo aperta dalle 13.00 alle 17.00, sarà necessario creare due intervalli di tempo per il martedì.</p></td>
</tr>
<tr class="odd">
<td><p><em>WednesdayHours1</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>Primo insieme di orari di apertura e chiusura per il mercoledì. Se l'organizzazione è aperta il mercoledì dalle 09.00 alle 17.00, sarà necessario configurare un solo intervallo di tempo. Se invece l'organizzazione è aperta dalle 08.00 a mezzogiorno, chiude un'ora per pranzo e quindi è di nuovo aperta dalle 13.00 alle 17.00, sarà necessario creare due intervalli di tempo per il mercoledì.</p>
<p>Se il mercoledì l'organizzazione resta chiusa, non configurare alcun valore per WednesdayHours1 e per WednesdayHours2.</p></td>
</tr>
<tr class="even">
<td><p><em>WednesdayHours2</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange</p></td>
<td><p>Secondo insieme di orari di apertura e chiusura per il mercoledì. Se l'organizzazione è aperta il mercoledì dalle 09.00 alle 17.00, sarà necessario configurare un solo intervallo di tempo. Se invece l'organizzazione è aperta dalle 08.00 a mezzogiorno, chiude un'ora per pranzo e quindi è di nuovo aperta dalle 13.00 alle 17.00, sarà necessario creare due intervalli di tempo per il mercoledì.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. **New-CsRgsHoursOfBusiness** non accetta l'input da pipeline.

## Tipi restituiti

Crea nuove istanze dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.BusinessHours.

## Vedere anche

#### Ulteriori risorse

[Get-CsRgsHoursOfBusiness](get-csrgshoursofbusiness.md)  
[New-CsRgsTimeRange](new-csrgstimerange.md)  
[Remove-CsRgsHoursOfBusiness](remove-csrgshoursofbusiness.md)  
[Set-CsRgsHoursOfBusiness](set-csrgshoursofbusiness.md)

