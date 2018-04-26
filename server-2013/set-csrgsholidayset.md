---
title: Set-CsRgsHolidaySet
TOCTitle: Set-CsRgsHolidaySet
ms:assetid: 90848409-25a0-4cc9-a0aa-f3331b5f93e9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398736(v=OCS.15)
ms:contentKeyID: 49301318
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsRgsHolidaySet

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica i valori delle proprietà di un set di festività esistente di Response Group. Un set di festività di Response Group è una raccolta di festività. È ad esempio possibile disporre di un set di festività per una coda per gli Stati Uniti (ovvero un set che può includere la festività del 4 luglio) e un set diverso per una coda per la Francia. Quest'ultima coda può definire una festività per la presa della Bastiglia, ma non per il 4 luglio. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsRgsHolidaySet -Instance <HolidaySet> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

I comandi mostrati nell'esempio 1 illustrano come creare una nuova festività (Christmas Day) e assegnare tale festività a un set di festività esistente. A tale scopo, nel primo comando dell'esempio viene utilizzato il cmdlet **New-CsRgsHoliday** per creare una nuova festività, ovvero una festività "virtuale" che esiste solo in memoria e viene archiviata nella variabile $x. **New-CsRgsHoliday** utilizza tre parametri: StartDate che rappresenta la data di inizio della festività (12/25/2010), EndDate che rappresenta la data di fine della festività (12/26/2010) e Name che rappresenta il nome univoco da assegnare alla festività.

Dopo la creazione della nuova festività, nel secondo comando viene utilizzato **Get-CsRgsHolidaySet** per recuperare il set di festività "2010 Holidays" dal servizio ApplicationServer:atl-cs-001.litwareinc.com. La festività impostata viene archiviata nella variabile $y.

Il comando 3 utilizza il metodo Aggiungi per aggiungere una nuova festività ($x) alla copia virtuale del set di festività ($y). Nel comando finale viene quindi utilizzato **Set-CsRgsHolidaySet** per scrivere tali modifiche e aggiungere la nuova festività al servizio ApplicationServer:atl-cs-001.litwareinc.com.

    $x = New-CsRgsHoliday -StartDate "12/25/2010" -EndDate "12/26/2010" -Name "Christmas Day"
    $y = Get-CsRgsHolidaySet -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "2010 Holidays"
    $y.HolidayList.Add($x)
    Set-CsRgsHolidaySet -Instance $y

## ESEMPIO 2

I comandi nell'esempio 2 rimuovono una festività (in questo caso Christmas Day) da un set di festività esistente. Per eseguire questa attività, nel primo comando dell'esempio viene utilizzato **Get-CsRgsHolidaySet** per recuperare il set di festività 2010 Holidays (-Name "2010 Holidays") dal servizio ApplicationServer:atl-cs-001.litwareinc.com. Il dato recuperato viene archiviato in una variabile denominata $x.

Nel secondo comando la proprietà HolidayList del set di festività recuperato viene inviata tramite pipe al cmdlet **Where-Object**, che seleziona la festività in cui la proprietà Name è uguale a "Christmas Day". La singola festività viene archiviata nella variabile $y.

Dopo che la festività Christmas Day è stata recuperata, il comando 3 utilizza il metodo Rimuovi per rimuovere la festività Christmas Day ($y) dal set di festività ($x). Nel comando finale dell'esempio viene quindi utilizzato **Set-CsRgsHolidaySet** per scrivere tali modifiche (ovvero per rimuovere la festività Christmas Day) nel set di festività 2010 Holidays effettivo in ApplicationServer:atl-cs-001.litwareinc.com.

    $x = Get-CsRgsHolidaySet -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "2010 Holidays"
    $y = $x.HolidayList | Where-Object {$_.Name -eq "Christmas Day"}
    $x.HolidayList.Remove($y)
    Set-CsRgsHolidaySet -Instance $x

## ESEMPIO 3

Il comando mostrato nell'Esempio 3 rimuove tutte le festività dal set di festività 2010 Holidays trovate nel servizio ApplicationServer:atl-cs-001.litwareinc.com. A tale scopo, nel primo comando dell'esempio viene utilizzato **Get-CsRgsHolidaySet** per recuperare il set di festività appropriato da ApplicationServer:atl-cs-001.litwareinc.com. Il set di festività viene quindi archiviato in una variabile denominata $x.

Dopo che il set di festività è stato recuperato, viene utilizzato il metodo Cancella per rimuovere tutti i valori archiviati nella proprietà HolidayList. Dopo che questa proprietà è stata cancellata, nel comando finale dell'esempio viene utilizzato il cmdlet **Set-CsRgsHolidaySet** per scrivere le modifiche nel set di festività 2010 Holidays.

    $x = Get-CsRgsHolidaySet -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "2010 Holidays"
    $x.HolidayList.Clear()
    Set-CsRgsHolidaySet -Instance $x

## Descrizione dettagliata

Allo scopo di garantire ai chiamanti la migliore esperienza di utilizzo possibile, l'applicazione Response Group consente di stabilire chiaramente quando gli agenti di Response Group sono disponibili per rispondere alle chiamate e quando non lo sono. Con l'applicazione Response Group, è infatti possibile definire gli orari d'ufficio, che indicano i giorni della settimana e le ore del giorno in cui gli agenti sono a disposizione per rispondere alle chiamate. Ad esempio, se l'organizzazione è aperta in genere dal lunedì al venerdì dalle 09.00 alle 17.00, sarà possibile configurare gli orari d'ufficio in maniera tale che indichino che gli agenti sono disponibili dal lunedì al venerdì dalle 09.00 alle 17.00 e, di conseguenza, che non sono disponibili il giovedì alle 20.00 o la domenica alle 14.30.

In molte organizzazioni vi sono tuttavia eccezioni alla settimana lavorativa tipica. Negli Stati Uniti, ad esempio, un'organizzazione può essere chiusa a Natale o durante il Giorno del Ringraziamento. Per gestire tali chiusure atipiche, l'applicazione Response Group consente di designare come festività determinati giorni, ovvero giorni in cui l'organizzazione sarebbe in genere aperta ma che, per qualche ragione, in questo caso non lo è. Le singole festività (create utilizzando il cmdlet **New-CsRgsHoliday**) sono raccolte in set di festività. Le festività relative agli Stati Uniti, ad esempio, possono essere raccolte in un set denominato US\_Holidays, mentre le festività relative al Giappone in un set denominato Japanese\_Holidays. Una volta raccolti, i set di festività possono essere assegnati ai flussi di lavoro di Response Group.

Il cmdlet **Set-CsRgsHolidaySet** consente di modificare un set di festività esistente. In linea di massima, ciò significa aggiungere festività o rimuovere festività dall set. **Set-CsRgsHolidaySet** non viene utilizzato direttamente per modificare un set di festività. Viene invece creato un riferimento oggetto a un set di festività esistente utilizzando il cmdlet **Get-CsRgsHolidaySet**. Un riferimento oggetto è una variabile che, in questo caso, fa riferimento a un set di festività esistente. Le modifiche del set vengono apportate in memoria e quindi viene utilizzato **Set-CsRgsHolidaySet** per scrivere tali modifiche nel set di festività effettivo. Se **Set-CsRgsHolidaySet** non viene chiamato, le modifiche apportate esisteranno solo in memoria e scompariranno non appena si chiuderà Windows PowerShell o si eliminerà il riferimento oggetto.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsRgsHolidaySet** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsRgsHolidaySet"}

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
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.HolidaySet</p></td>
<td><p>Riferimento oggetto per il set di festività di Response Group da modificare. Un riferimento oggetto in genere viene recuperato utilizzando il cmdlet <strong>Get-CsRgsHolidaySet</strong> e assegnando il valore restituito a una variabile. Questo comando ad esempio restituisce un riferimento oggetto al set di festività Help Desk e archivia tale riferimento in una variabile denominata $x:</p>
<p>$x = Get-CsRgsHolidaySet -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name &quot;Help Desk&quot;</p>
<p></p></td>
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

Oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.HolidaySet. **Remove-CsRgsHolidaySet** accetta le istanze da pipeline dell'oggetto set di festività di Response Group.

## Tipi restituiti

**Set-CsRgsHolidaySet** non restituisce alcun oggetto o valore. Invece, il cmdlet modifica istanze esistenti dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.HolidaySet.

## Vedere anche

#### Ulteriori risorse

[Get-CsRgsHolidaySet](get-csrgsholidayset.md)  
[New-CsRgsHoliday](new-csrgsholiday.md)  
[New-CsRgsHolidaySet](new-csrgsholidayset.md)  
[Remove-CsRgsHolidaySet](remove-csrgsholidayset.md)

