---
title: New-CsRgsTimeRange
TOCTitle: New-CsRgsTimeRange
ms:assetid: e8abc3cc-2b13-479d-83d6-2f542fa12e45
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399040(v=OCS.15)
ms:contentKeyID: 49302344
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRgsTimeRange

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo intervallo di tempo di Response Group. Gli intervalli di tempo vengono utilizzati dall'applicazione Response Group per specificare gli orari di apertura e di chiusura per i giorni lavorativi. Se ad esempio gli agenti del supporto tecnico sono disponibili solo dalle 12.00 alle 17.00 la domenica, sarà necessario creare un intervallo di tempo per la domenica con un orario di apertura fissato alle 12.00 e uno di chiusura fissato alle 17.00. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsRgsTimeRange -CloseTime <TimeSpan> -OpenTime <TimeSpan> [-Name <String>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene mostrato come utilizzare il cmdlet **New-CsRgsTimeRange** per modificare le proprietà di un insieme di orari d'ufficio esistente. In questo esempio viene innanzitutto chiamato **New-CsRgsTimeRange** per creare un nuovo intervallo di tempo denominato "Sunday hours". Questo intervallo di tempo imposta l'orario di apertura alle 8.30 (08:30) e quello di chiusura alle 13.30 (13:30). L'intervallo di tempo creato soltanto in memoria dal comando viene archiviato in una variabile denominata $sundayHours.

Dopo che l'intervallo di tempo è stato configurato, nel secondo comando dell'esempio viene utilizzato il cmdlet **Get-CsRgsHoursOfBusiness** per restituire la raccolta di orari d'ufficio denominata Help Desk Hours (trovata nel servizio ApplicationServer:atl-cs-001.litwareinc.com). La raccolta restituita viene archiviata in una variabile denominata $y.

Dopo che la raccolta è stata recuperata, il terzo comando imposta il valore della proprietà SundayHours1 su $sundayHours, il riferimento oggetto contenente l'intervallo di tempo appena creato. Al termine dell'esecuzione di questo comando, viene quindi utilizzato **Set-CsRgsHoursOfBusiness** per scrivere le modifiche nella raccolta di orari d'ufficio Help Desk Hours. Se **Set-CsRgsHoursOfBusiness** non viene chiamato, l'intervallo di tempo appena creato esisterà solo in memoria e scomparirà non appena si chiuderà Windows PowerShell o si eliminerà la variabile $sundayHours. In tal caso, la raccolta di orari d'ufficio Help Desk Hours non verrà aggiornata.

    $sundayHours = New-CsRgsTimeRange -Name "Sunday hours" -OpenTime "08:30" -CloseTime "13:30"
    $y = Get-CsRgsHoursOfBusiness -Identity Service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk Hours" 
    $y.SundayHours1 = $sundayHours
    Set-CsRgsHoursOfBusiness -Instance $y

## ESEMPIO 2

L'esempio 2 mostra come creare un nuovo intervallo di tempo di Response Group, e quindi utilizzarlo in un nuovo insieme di orari d'ufficio. Nel primo comando dell'esempio viene utilizzato il cmdlet **New-CsRgsTimeRange** per creare un nuovo intervallo di tempo denominato Sunday Hours. L'oggetto OpenTime per l'intervallo viene impostato sulle 8.30 ("08:30") e l'oggetto CloseTime sulle 13.30 ("13:30" utilizzando il formato 24 ore). L'intervallo di tempo viene archiviato in una variabile denominata $sundayHours.

Nel secondo comando viene utilizzato il cmdlet **New-CsRgsBusinessHours** per creare una nuova raccolta di orari d'ufficio denominata Help Desk Hours. In questo comando, la variabile $sundayHours specifica l'intervallo di tempo per la proprietà SundayHours1.

    $sundayHours = New-CsRgsTimeRange -Name "Sunday hours" -OpenTime "08:30" -CloseTime "13:30"
    New-CsRgsHoursOfBusiness -Parent Service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk Hours" -SundayHours1 $sundayHours

## Descrizione dettagliata

Nell'applicazione Response Group vengono utilizzate raccolte di orari d'ufficio per tenere traccia dei giorni della settimana e delle ore del giorno in cui gli agenti sono in genere disponibili per rispondere alle chiamate telefoniche. Si supponga ad esempio che il supporto tecnico sia aperto ogni lunedì dalle 7.00 alle 19.00. In questo caso, sarà necessario eseguire due operazioni, ovvero utilizzare il cmdlet **New-CsRgsHoursOfBusiness** per creare una raccolta di orari d'ufficio per il supporto tecnico e modificare la proprietà MondayTimeRange1 per indicare che il supporto tecnico apre alle 07.00 e chiude alle 19.00.

Per modificare una raccolta di orari d'ufficio esistente, è necessario utilizzare il cmdlet **Set-CsRgsHoursOfBusiness**. Non è tuttavia possibile utilizzare tale cmdlet per modificare direttamente una proprietà relativa a un intervallo di tempo. Ad esempio, per **Set-CsRgsHoursOfBusiness** non sono previsti parametri che corrispondono alla proprietà MondayTimeRange1. Per modificare una raccolta di orari d'ufficio, è invece necessario recuperare la raccolta utilizzando **Get-CsRgsHoursOfBusiness**, apportare le modifiche solo in memoria e quindi utilizzare **Set-CsRgsHoursOfBusiness** per scrivere le modifiche nella raccolta di orari d'ufficio effettiva.

Spesso le modifiche effettuate su una raccolta di orari d'ufficio implica una modifica degli orari di chiusura e apertura relativi a un giorno (o a giorni) specifico. Per modificare gli orari di apertura e di chiusura, è necessario specificare tali orari utilizzando il cmdlet **New-CsRgsTimeRange**. Quando si chiama tale cmdlet, il valore risultante deve essere archiviato in una variabile del riferimento oggetto. Questa variabile verrà quindi utilizzata per impostare gli orari di apertura e chiusura all'interno della raccolta degli orari d'ufficio.

È necessario utilizzare **New-CsRgsTimeRange** anche per specificare gli orari di apertura e di chiusura ogni volta che si crea una nuova raccolta di orari d'ufficio.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsRgsTimeRange** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Poiché tuttavia questo cmdlet crea un oggetto in memoria e da solo non apporta modifiche al sistema, può essere essenzialmente eseguito da chiunque. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsRgsTimeRange"}

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
<td><p><em>CloseTime</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Ora del giorno in cui termina l'orario d'ufficio. Per CloseTime è necessario utilizzare un formato 24 ore. Ad esempio, per indicare che l'orario d'ufficio termina alle nove di sera, utilizzare il seguente formato: -CloseTime &quot;21:00&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>OpenTime</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Ora del giorno in cui comincia l'orario d'ufficio. Per OpenTime è necessario utilizzare un formato 24 ore. Ad esempio, per indicare che l'orario d'ufficio inizia all'una e mezza del pomeriggio, utilizzare il seguente formato: -OpenTime &quot;13:30:00&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Identificatore univoco per l'intervallo di tempo da creare. Il nome ha un limite massimo di 128 caratteri.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. **. New-CsRgsTimeRange** non accetta input da pipeline.

## Tipi restituiti

**New-CsRgsTimeRange** crea nuove istanze dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.TimeRange.

## Vedere anche

#### Ulteriori risorse

[New-CsRgsHoursOfBusiness](new-csrgshoursofbusiness.md)  
[Set-CsRgsHoursOfBusiness](set-csrgshoursofbusiness.md)

