---
title: New-CsRgsHolidaySet
TOCTitle: New-CsRgsHolidaySet
ms:assetid: 5c110dcf-f596-44ae-8d40-bfafc6701550
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398403(v=OCS.15)
ms:contentKeyID: 49300670
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRgsHolidaySet

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo set di festività di Response Group. Un set di festività di Response Group è una raccolta di festività. È ad esempio possibile disporre di un set di festività per una coda per gli Stati Uniti (ovvero un set che può includere la festività del 4 luglio) e un set diverso per una coda per la Francia. Quest'ultima coda può definire una festività per la presa della Bastiglia, ma non per il 4 luglio. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsRgsHolidaySet -HolidayList <Collection> -Name <String> -Parent <RgsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

I comandi mostrati nell'esempio 1 creano un nuovo set di festività denominato 2013 Holidays (per le festività del 2013) e quindi assegnano a tale set una nuova festività (New Year's Day, ovvero Capodanno). A tale scopo, nel primo comando viene utilizzato **New-CsRgsHoliday** per creare una festività relativa a Capodanno (New Year's Day). **New-CsRgsHoliday** accetta tre parametri: StartDate che indica la data di inizio della festività (1/1/2013 12:00 AM), EndDate che rappresenta la data di fine della festività (1/2/2013 12:00 AM) e Name che viene utilizzato per archiviare il nome assegnato alla festività. L'oggetto festività risultante viene archiviato nella variabile $j.

Dopo che la nuova festività è stata creata in memoria, viene utilizzato **New-CsRgsHolidaySet** per creare un nuovo set di festività nel servizio ApplicationServer:atl-cs-001.litwareinc.com. Al set di festività viene conferito il nome 2013 Holidays (-Name "2013 Holidays") e viene assegnata la festività archiviata nella variabile $x: -HolidayList ($x). Se si desidera assegnare più festività al set di festività, è necessario creare nuove festività e assegnare ognuna di queste a una variabile univoca. È quindi possibile includere tutti questi i nomi di variabili come valore del parametro passato a HolidayList:

\-HolidayList($x, $y, $z)

    $x = New-CsRgsHoliday -StartDate "1/1/2013 12:00 AM" -EndDate "1/2/2013 12:00 AM" -Name "New Year's Day"
    New-CsRgsHolidaySet -Parent "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "2013 Holidays" -HolidayList($x)

## Descrizione dettagliata

Allo scopo di garantire ai chiamanti la migliore esperienza di utilizzo possibile, l'applicazione Response Group consente di stabilire chiaramente quando gli agenti di Response Group sono disponibili per rispondere alle chiamate e quando non lo sono. Con l'applicazione Response Group, è infatti possibile definire gli orari d'ufficio, che indicano i giorni della settimana e le ore del giorno in cui gli agenti sono a disposizione per rispondere alle chiamate. Ad esempio, se l'organizzazione è aperta in genere dal lunedì al venerdì dalle 09.00 alle 17.00, sarà possibile configurare gli orari d'ufficio in maniera tale che indichino che gli agenti sono disponibili dal lunedì al venerdì dalle 09.00 alle 17.00 e, di conseguenza, che non sono disponibili il giovedì alle 20.00 o la domenica alle 14.30.

In molte organizzazioni vi sono tuttavia eccezioni alla settimana lavorativa tipica. Negli Stati Uniti ad esempio un'organizzazione può essere chiusa a Natale o durante il Giorno del Ringraziamento. Per gestire chiusure atipiche, l'applicazione Response Group consente di designare come festività determinati giorni, ovvero giorni in cui l'organizzazione è di solito aperta ma, per qualche ragione, in questo caso non lo è. Le singole festività (create utilizzando il cmdlet **New-CsRgsHoliday**) sono raccolte in set di festività. Le festività relative agli Stati Uniti ad esempio possono essere raccolte in un set denominato US\_Holidays, mentre le festività relative al Giappone in un set denominato Japanese\_Holidays. Dopo essere state raccolte, le festività e i set corrispondenti possono quindi essere assegnati ai flussi di lavoro di Response Group.

Il cmdlet **New-CsRgsHolidaySet** consente di configurare nuovi set di festività da utilizzare nell'organizzazione. Quando si crea un nuovo set di festività, è necessario includere almeno una festività. Tali singole festività devono essere create utilizzando il cmdlet **New-CsRgsHoliday**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsRgsHolidaySet** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsRgsHolidaySet"}

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
<td><p><em>HolidayList</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Collections.ObjectModel.Collection</p></td>
<td><p>Una o più festività da aggiungere al set di festività. Le festività devono essere create utilizzando il cmdlet <strong>New-CsRgsHoliday</strong> e quindi archiviate in un riferimento oggetto. Questi riferimenti oggetto vengono quindi passati al parametro Holidays per aggiungere le festività al relativo set. Ad esempio, questo comando crea una festività denominata New Year's Day e quindi memorizza il valore risultante in un riferimento oggetto denominato $x:</p>
<p>$x = New-CsRgsHoliday -StartDate &quot;1/1/2013 12:00 AM&quot; -EndDate &quot;1/2/2013 12:00 AM&quot; -Name &quot;New Year's Day&quot;</p>
<p>Si noti che il formato utilizzato per specificare le date e le ore dipenderà dalle impostazioni internazionali e della lingua in uso. Per gli esempi mostrati in questo argomento viene utilizzato il formato dell'inglese americano.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome univoco da assegnare al set di festività. La combinazione della proprietà Parent e della proprietà Name consente di identificare in modo univoco i set di festività senza dover fare riferimento al relativo identificatore univoco globale (GUID).</p></td>
</tr>
<tr class="odd">
<td><p><em>Parent</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>Il servizio in cui sarà ospitato il nuovo set di festività. Ad esempio: -Parent &quot;service:ApplicationServer:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
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

Nessuno. **New-CsRgsHolidaySet** non accetta l'input da pipeline.

## Tipi restituiti

**New-CsRgsHolidaySet** crea nuove istanze dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.HolidaySet.

## Vedere anche

#### Ulteriori risorse

[Get-CsRgsHolidaySet](get-csrgsholidayset.md)  
[New-CsRgsHoliday](new-csrgsholiday.md)  
[Remove-CsRgsHolidaySet](remove-csrgsholidayset.md)  
[Set-CsRgsHolidaySet](set-csrgsholidayset.md)

