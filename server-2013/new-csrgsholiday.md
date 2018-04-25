---
title: New-CsRgsHoliday
TOCTitle: New-CsRgsHoliday
ms:assetid: 021c6286-207d-4924-b477-15c9a98d6fda
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398075(v=OCS.15)
ms:contentKeyID: 49299494
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRgsHoliday

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova festività di Response Group. Nell'applicazione Response Group una festività rappresenta un giorno in cui gli agenti assegnati a una coda, che in genere dovrebbero lavorare in quella data, non lavorano e non sono quindi disponibili per rispondere alle chiamate. Se ad esempio ai dipendenti che operano negli Stati Uniti viene concessa come festività il Giorno del ringraziamento, sarà necessario configurare una festività per il 22 novembre 2013. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsRgsHoliday -EndDate <DateTime> -StartDate <DateTime> [-Name <String>]

## Esempi

## ESEMPIO 1

Con i comandi mostrati nell'esempio 1 viene illustrato come creare una nuova festività (Christmas Day) e assegnare tale festività a un set di festività esistenti. A tale scopo, nel primo comando dell'esempio viene utilizzato il cmdlet **New-CsRgsHoliday** per creare una nuova festività, ovvero una festività "virtuale" che esiste solo in memoria e viene archiviata nella variabile $christmasDay. **New-CsRgsHoliday** utilizza tre parametri, ovvero StartDate che rappresenta la data di inizio della festività (25/12/2013, ore 00.00), EndDate che rappresenta la data di fine della festività (26/12/2013, ore 00.00) e Name che rappresenta il nome univoco da assegnare alla festività.

Dopo la creazione della nuova festività, nel secondo comando viene utilizzato **Get-CsRgsHolidaySet** per recuperare il set di festività "2013 Holidays" dal servizio ApplicationServer:atl-cs-001.litwareinc.com. La festività impostata viene archiviata nella variabile $y.

Il comando 3 utilizza il metodo Aggiungi per aggiungere una nuova festività ($christmasDay) alla copia virtuale del set di festività ($y). Il comando finale quindi chiama **Set-CsRgsHolidaySet** per scrivere le modifiche, ovvero per aggiungere la nuova festività, nel servizio ApplicationServer:atl-cs-001.litwareinc.com.

    $christmasDay = New-CsRgsHoliday -StartDate "12/25/2013 12:00 AM" -EndDate "12/26/2013 12:00 AM" -Name "Christmas Day"
    $y = Get-CsRgsHolidaySet -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com"  -Name "2013 Holidays"
    $y.HolidayList.Add($christmasDay)
    Set-CsRgsHolidaySet -Instance $y

## Descrizione dettagliata

Nell'applicazione Response Group vengono utilizzate raccolte di orari d'ufficio per indicare i giorni della settimana e le ore del giorno in cui gli agenti sono in genere disponibili per rispondere alle chiamate telefoniche. Si supponga ad esempio che il supporto tecnico di solito disponga di personale ogni lunedì dalle 07.00 alle 19.00. In tal caso, sarebbe necessario creare una raccolta di orari d'ufficio per il supporto tecnico e configurare le 07.00 come orario di apertura e le 19.00 come orario di chiusura per il lunedì tipico.

Possono tuttavia esservi eccezioni alla regola che prevede che il supporto tecnico disponga di personale dalle 07.00 alle 19.00 di tutti i lunedì. Ad esempio, il 4 luglio è una festività nazionale negli USA, pertanto il personale del supporto tecnico potrebbe non essere disponibile in quella data. Per evidenziare il fatto che il supporto tecnico non sarà in funzione giovedì 4 luglio 2013, sarà necessario creare una festività per quella data e aggiungerla al set di festività del supporto tecnico.

Per creare una festività, è necessario utilizzare il cmdlet **New-CsRgsHoliday**. La "festività" non deve comprendere necessariamente una celebrazione o un festeggiamento; è semplicemente un giorno in cui gli agenti non saranno disponibili per rispondere al telefono. **New-CsRgsHoliday** non aggiunge direttamente una festività a un set di festività. Piuttosto, il cmdlet crea una nuova festività che esiste soltanto in memoria. È pertanto necessario creare un riferimento oggetto (come $x) che punti a tale istanza in memoria. Dopo che la festività è stata creata in memoria, è necessario utilizzare il cmdlet **Get-CsRgsHolidaySet** per recuperare il set di festività appropriato e il cmdlet **Set-CsRgsHolidaySet** per aggiungere la nuova festività a tale set.

Anche se un set di festività può contenere (e in genere contiene) molte festività, queste festività devono essere aggiunte al set una alla volta.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsRgsHoliday** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Poiché tuttavia questo cmdlet crea un oggetto in memoria e da solo non apporta modifiche al sistema, può essere essenzialmente eseguito da chiunque. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsRgsHoliday\\b"}

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
<td><p><em>EndDate</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.DateTime</p></td>
<td><p>Data di fine della festività. Il formato relativo alla data di fine dipende dalle impostazioni internazionali e della lingua in uso. Ad esempio, negli USA una data di fine corrispondente al 4 luglio 2013 avrà il formato -EndDate &quot;7/5/2013 12:00 AM&quot;, che indica che la festività finisce alle 00.00 del 5 luglio 2013.</p></td>
</tr>
<tr class="even">
<td><p><em>StartDate</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.DateTime</p></td>
<td><p>Data di inizio della festività. Il formato relativo alla data di inizio dipende dalle impostazioni internazionali e della lingua in uso. Ad esempio, negli USA una data di inizio corrispondente al 4 luglio 2013 avrà il formato -StartDate &quot;7/4/2013 12:00 AM&quot;, che indica che la festività inizia alle 00.00 del 4 luglio 2013.</p></td>
</tr>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome univoco utilizzato per differenziare la festività dalle altre festività.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. **New-CsRgsHoliday** non accetta l'input da pipeline.

## Tipi restituiti

**New-CsRgsHoliday** crea nuove istanze dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.Holiday.

## Vedere anche

#### Ulteriori risorse

[New-CsRgsHolidaySet](new-csrgsholidayset.md)  
[Set-CsRgsHolidaySet](set-csrgsholidayset.md)

