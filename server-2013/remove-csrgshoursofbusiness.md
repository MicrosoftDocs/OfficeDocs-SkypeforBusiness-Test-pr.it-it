---
title: Remove-CsRgsHoursOfBusiness
TOCTitle: Remove-CsRgsHoursOfBusiness
ms:assetid: 753b2cd7-709b-455b-85a3-8b80ea35d4e0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398568(v=OCS.15)
ms:contentKeyID: 49301002
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsRgsHoursOfBusiness

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un insieme esistente di orari di ufficio di Response Group. Gli orari di ufficio sono utilizzati per indicare i giorni della settimana e le ore del giorno in cui gli agenti di Response Group sono in genere disponibili per rispondere alle chiamate telefoniche. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsRgsHoursOfBusiness -Instance <BusinessHours> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 rimuove tutti gli insiemi di orari di ufficio trovati nel servizio ApplicationServer:atl-cs-001.litwareinc.com. A tale scopo, nel comando viene innanzitutto chiamato **Get-CsRgsHoursOfBusiness** per restituire tutti gli insiemi di orari di ufficio trovati nel servizio ApplicationServer:atl-cs-001.litwareinc.com. Questi insiemi vengono quindi inviati tramite pipe al cmdlet **Remove-CsRgsHoursOfBusiness**, che elimina ogni insieme di orari di ufficio che gli viene passato.

    Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" | Remove-CsRgsHoursOfBusiness

## ESEMPIO 2

Nell'esempio 2, un singolo insieme di orari di ufficio viene rimosso da ApplicationServer:atl-cs-001.litwareinc.com: la raccolta denominata Help Desk Business Hours.

    Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -Name "Help Desk Business Hours" | Remove-CsRgsHoursOfBusiness

## ESEMPIO 3

Nell'esempio 3 vengono eliminati tutti gli insiemi di orari di ufficio in cui è configurata la domenica. A tale scopo, nel comando viene innanzitutto chiamato **Get-CsRgsHoursOfBusiness** per restituire tutti gli insiemi di orari di ufficio trovati in ApplicationServer:atl-cs-001.litwareinc.com. Questi insiemi vengono quindi inviati tramite pipe al cmdlet **Where-Object**, che seleziona solo gli elementi per cui si verifica una delle condizioni seguenti: la proprietà SundayTimeRange1 non è uguale a un valore Null o la proprietà SundayTimeRange2 non è uguale a un valore Null. Se una proprietà relativa a un intervallo di tempo non è Null, significa che per tale intervallo di tempo sono stati configurati orari di ufficio. Tutti gli insiemi che soddisfano almeno uno di questi criteri vengono quindi inviati tramite pipe al cmdlet **Remove-CsRgsHoursOfBusiness**, che li rimuove.

    Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" | Where-Object {$_.SundayTimeRange1 -ne $Null -or $_.SundayTimeRange2 -ne $Null} | Remove-CsRgsHoursOfBusiness

## ESEMPIO 4

Il comando mostrato nell'esempio 4 elimina tutti gli insiemi di orari di ufficio personalizzati, ovvero gli insiemi che non possono essere condivisi tra flussi di lavoro. Per eseguire questa attività, nel comando viene innanzitutto utilizzato **Get-CsRgsHoursOfBusiness** per restituire tutti gli insiemi di orari di ufficio trovati in ApplicationServer:atl-cs-001.litwareinc.com. Questi dati vengono quindi inviati tramite pipe al cmdlet **Where-Object**, che seleziona solo gli insiemi in cui la proprietà Custom è uguale a True. Questi insiemi vengono quindi inviati tramite pipe a **Remove-CsRgsHoursOfBusiness**, che li elimina.

    Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" | Where-Object {$_.Custom -eq $True} | Remove-CsRgsHoursOfBusiness -Force

## Descrizione dettagliata

Allo scopo di garantire ai chiamanti la migliore esperienza di utilizzo possibile, l'applicazione Response Group consente di stabilire chiaramente quando gli agenti di Response Group sono disponibili per rispondere alle chiamate e quando non lo sono. Con l'applicazione Response Group, è infatti possibile definire gli orari di ufficio, che indicano i giorni della settimana e le ore del giorno di disponibilità degli agenti. Se ad esempio l'organizzazione è operativa in genere dal lunedì al venerdì dalle 09.00 alle 17.00, sarà possibile configurare gli orari di ufficio in modo da indicare che gli agenti sono disponibili dal lunedì al venerdì dalle 09.00 alle 17.00 e, di conseguenza, che non lo sono il giovedì alle 20.00 o la domenica alle 14.30.

È possibile creare nuovi insiemi di orari di ufficio utilizzando il cmdlet **New-CsRgsHoursOfBusiness**. Tali insiemi possono successivamente essere rimossi utilizzando il cmdlet **Remove-CsRgsHoursOfBusiness**. Si noti che, quando si chiama **Remove-CsRgsHoursOfBusiness**, viene rimosso l'intero insieme di orari, che non è più disponibile per l'utilizzo. Se si desidera semplicemente rimuovere gli orari di ufficio per un determinato giorno, ad esempio perché il supporto tecnico non è più disponibile la domenica, utilizzare **Set-CsRgsHoursOfBusiness** per rimuovere da una raccolta solo i valori applicabili.

Per impostazione predefinita, **Remove-CsRgsHoursOfBusiness** visualizza un prompt se si tenta di eliminare un insieme di orari di ufficio attualmente utilizzato da un flusso di lavoro attivo. Verrà richiesto di confermare se si desidera rimuovere la raccolta e non verrà eseguita alcuna azione finché non si risponde. Per non visualizzare il prompt ed eliminare direttamente gli insiemi di orari di ufficio anche se al momento sono assegnati a un flusso di lavoro attivo, aggiungere il parametro Force. Ad esempio:

Get-CsRgsHoursOfBusiness –Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" | Remove-CsRgsHoursOfBusiness –Force

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, il cmdlet **Remove-CsRgsHoursOfBusiness** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsRgsHoursOfBusiness"}

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
<td><p>Riferimento all'oggetto che punta all'insieme di orari di ufficio da rimuovere. Quando gli oggetti flusso di lavoro vengono inviati tramite pipe a <strong>Remove-CsRgsHoursOfBusiness</strong>, è possibile omettere il parametro Instance.</p>
<p>Per utilizzare il parametro Instance, sono necessari comandi analoghi al seguente:</p>
<p>$x = Get-CsRgsHoursOfBusiness –Identity ApplicationServer:atl-cs-001.litwareinc.com /1987d3c2-4544-489d-bbe3-59f79f530a83</p>
<p>Remove-CsRgsHoursOfBusiness –Instance $x</p>
<p>Si noti che è possibile rimuovere un solo insieme di orari di ufficio alla volta quando si utilizza il parametro Instance. Ciò significa che il riferimento all'oggetto ($x) non può contenere più oggetti orario di ufficio.</p></td>
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
<td><p>Forza l'eliminazione di un insieme di orari di ufficio. Se questo parametro è presente, il set di festività sarà eliminato senza avviso, anche se è utilizzato attualmente da un flusso di lavoro attivo. Se questo parametro non è presente, verrà richiesto di confermare l'eliminazione di ogni insieme di orari di ufficio attualmente assegnati a un flusso di lavoro attivo.</p></td>
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

Oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.BusinessHours. **Remove-CsRgsHoursOfBusiness** accetta le istanze da pipeline dell'oggetto orari di ufficio di Response Group.

## Tipi restituiti

Elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.BusinessHours.

## Vedere anche

#### Ulteriori risorse

[Get-CsRgsHoursOfBusiness](get-csrgshoursofbusiness.md)  
[New-CsRgsHoursOfBusiness](new-csrgshoursofbusiness.md)  
[Set-CsRgsHoursOfBusiness](set-csrgshoursofbusiness.md)

