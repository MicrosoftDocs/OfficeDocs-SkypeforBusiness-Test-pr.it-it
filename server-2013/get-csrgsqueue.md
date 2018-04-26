---
title: Get-CsRgsQueue
TOCTitle: Get-CsRgsQueue
ms:assetid: a2e786b7-5096-4011-8108-2b56ae768c1d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412759(v=OCS.15)
ms:contentKeyID: 49301537
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsRgsQueue

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera informazioni relative alle code di Response Group in uso nell'organizzazione. Con l'applicazione Response Group, le chiamate telefoniche vengono inserite in una coda e lasciate in attesa finché un agente di Response Group non è disponibile per rispondere. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsRgsQueue [-Identity <RgsIdentity>] [-Name <String>] [-Owner <RgsIdentity>] [-ShowAll <SwitchParameter>]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 restituisce le informazioni su tutte le code di Response Group configurate per l'utilizzo nell'organizzazione. Questa operazione viene eseguita chiamando **Get-CsRgsQueue** senza alcun parametro.

    Get-CsRgsQueue

## ESEMPIO 2

Il comando mostrato nell'esempio 2 restituisce informazioni su tutte le code di Response Group trovate nel servizio ApplicationServer:atl-cs-001.litwareinc.com.

    Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com

## ESEMPIO 3

Nell'esempio 3 vengono restituite informazioni per una singola coda di Response Group, ovvero la coda denominata "Help Desk", trovata nel servizio ApplicationServer:atl-cs-001.litwareinc.com.

    Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"

## ESEMPIO 4

Il comando mostrato nell'esempio 4 visualizza informazioni dettagliate sulla proprietà TimeoutAction di ciascuna coda di Response Group trovata nel servizio ApplicationServer:atl-cs-001.litwareinc.com. Per eseguire questa attività, viene innanzitutto utilizzato **Get-CsRgsQueue** per restituire informazioni su tutte le code trovate in ApplicationServer:atl-cs-001.litwareinc.com. Le informazioni vengono quindi passate al cmdlet **Select-Object**, che espande il valore archiviato nella proprietà TimeoutAction. Quando si espande la proprietà TimeoutAction, sono visibili le singole proprietà dell'oggetto incorporato che costituiscono il valore della proprietà, ovvero Prompt; TargetQuestion; Target; TargetQueueID; e TargetUri.

    Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com | Select-Object -ExpandProperty TimeoutAction

## ESEMPIO 5

Nell'esempio 5 vengono restituite informazioni su tutte le code di Response Group in ApplicationServer:atl-cs-001.litwareinc.com la cui proprietà OverflowCandidate è impostata su NewestCall. Per ottenere questo risultato, il comando utilizza innanzitutto **Get-CsRgsQueue** per restituire una raccolta di tutte le code di Response Group trovate nel servizio specificato. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le code la cui proprietà OverflowCandidate è uguale a "NewestCall".

    Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com | Where-Object {$_.OverflowCandidate -eq "NewestCall"}

## Descrizione dettagliata

Quando qualcuno chiama un numero di telefono associato all'applicazione Response Group, in genere avviene quanto segue: la chiamata viene trasferita a una domanda a cui il chiamante deve rispondere per proseguire (ad esempio, "Premere 1 per supporto hardware; premere 2 per supporto software") oppure viene messa in coda finché un agente di Response Group non è disponibile per rispondere.

Invece di avere una singola coda per tutte le chiamate telefoniche, l'applicazione Response Group consente di creare più code che è possibile associare a flussi di lavoro e gruppi di agenti di Response Group diversi. Questo significa che le code possono rispondere diversamente a eventi come ad esempio un determinato numero di chiamate da mettere in coda contemporaneamente o chiamanti lasciati in attesa per un determinato numero di secondi.

Il cmdlet **Get-CsRgsQueue** consente di restituire informazioni sulle code di Response Group configurate per l'utilizzo nell'organizzazione.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsRgsQueue** i membri dei seguenti gruppi: RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsRgsQueue"}

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
<td><p>Rappresenta l'identità del servizio in cui è ospitata la coda di Response Group o l'identità piena della stessa coda. Se si specifica l'identità del servizio (ad esempio, service:ApplicationServer:atl-cs-001.litwareinc.com), verranno restituite tutte le code di Response Group ospitate nel servizio. Se si specifica l'identità della coda, verrà restituita solo la coda di Response Group specificata. L'identità di una coda è costituita dall'identità del servizio seguita da un identificatore univoco globale (GUID), ad esempio service:ApplicationServer:atl-cs-001.litwareinc.com /1987d3c2-4544-489d-bbe3-59f79f530a83.</p>
<p>Un modo alternativo per restituire una singola coda di Response Group consiste nello specificare l'identità del servizio e nell'includere il parametro Name e il nome della coda. Ciò consente di recuperare una coda specifica senza conoscere il GUID assegnato alla coda stessa.</p>
<p>Se chiamato senza alcun parametro, <strong>Get-CsRgsQueue</strong> restituisce tutte le code di Response Group configurate per l'utilizzo nell'organizzazione.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome univoco assegnato alla coda di Response Group nel momento stesso in cui la coda è stata creata.</p></td>
</tr>
<tr class="odd">
<td><p><em>Owner</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>Nome di dominio completo del pool &quot;proprietario&quot; della coda. L'ID del pool proprietario e l'ID del pool di una coda in genere coincidono. Se tuttavia è necessario spostare temporaneamente una coda, ad esempio in una procedura di ripristino di emergenza, l'ID del pool cambia. L'ID del proprietario invece continuerà a puntare al pool originale.</p></td>
</tr>
<tr class="even">
<td><p><em>ShowAll</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se specificato, mostra tutte le code di Response Group, incluse quelle in cui l'ID del pool proprietario e l'ID del pool sono diversi. Per impostazione predefinita, Get-CsRgsQueue restituisce informazioni solo sulle code in cui l'ID del pool proprietario e l'ID del pool sono identici.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Stringa. **Get-CsRgsQueue** accetta un valore stringa che rappresenta l'identità della coda di Response Group.

## Tipi restituiti

**Get-CsRgsQueue** restituisce istanze dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.Queue.

## Vedere anche

#### Ulteriori risorse

[New-CsRgsQueue](new-csrgsqueue.md)  
[Remove-CsRgsQueue](remove-csrgsqueue.md)  
[Set-CsRgsQueue](set-csrgsqueue.md)

