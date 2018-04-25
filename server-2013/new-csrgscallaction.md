---
title: New-CsRgsCallAction
TOCTitle: New-CsRgsCallAction
ms:assetid: 07b70bbd-8e2e-426f-8c30-29f74b07b55b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398136(v=OCS.15)
ms:contentKeyID: 49299587
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRgsCallAction

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova azione di chiamata di Response Group. Nell'applicazione Response Group vengono utilizzate azioni di chiamata per determinare quale operazione deve eseguire il sistema quando viene ricevuta una chiamata. Un'azione di chiamata può ad esempio specificare che una chiamata venga trasferita a un'altra coda, che venga posta una domanda specifica di Response Group o che una chiamata venga terminata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsRgsCallAction -Action <Terminate | TransferToQueue | TransferToQuestion | TransferToUri | TransferToVoicemailUri | TransferToPstn> [-Prompt <Prompt>] [-Question <Question>] [-QueueID <RgsIdentity>] [-Uri <String>]

## Esempi

## ESEMPIO 1

I comandi mostrati nell'esempio 1 illustrano come creare una nuova azione di chiamata di Response Group e quindi assegnare tale azione a una coda esistente di Response Group. In questo caso, l'azione di chiamata determina l'operazione da eseguire se si verifica una condizione di overflow della coda. Per eseguire questa attività, viene innanzitutto utilizzato **Get-CsRgsQueue** per recuperare la coda Help Desk Overflow dell'applicazione Response Group da ApplicationServer:atl-cs-001.litwareinc.com. Le informazioni di tale coda vengono archiviate in una variabile denominata $x. Viene quindi utilizzato un comando analogo per recuperare la coda Help Desk. In questo caso, le informazioni vengono archiviate in una variabile denominata $z.

Una volta recuperate le code, viene utilizzato il cmdlet **New-CsRgsPrompt** per creare un prompt di sintesi vocale che accompagni la nuova azione di chiamata. Tale nuova azione viene creata eseguendo il cmdlet **New-CsRgsCallAction**. All'azione di chiamata vengono assegnati tre parametri, ovvero Prompt che rappresenta il prompt utilizzato dall'azione di chiamata, Action che indica che cosa accade se la nuova azione di chiamata viene attivata (il valore TransferToQueue indica che la chiamata verrà trasferita a una coda diversa di Response Group) e QueueID che corrisponde alla coda alternativa a cui sarà trasferita la chiamata ($x.Identity, che rappresenta l'identità della coda Help Desk Overflow). La nuova azione di chiamata viene creata in memoria e archiviata in una variabile denominata $y.

Una volta creata l'azione di chiamata, è possibile assegnare tale nuova azione alla coda Help Desk. Ciò avviene impostando il valore della proprietà OverflowAction su $y, la variabile che contiene l'azione di chiamata appena creata. Se si verifica una condizione di overflow nella coda Help Desk, ovvero se tale coda raggiunge il numero massimo di chiamanti consentiti, le eventuali chiamate successive verranno trasferite automaticamente alla coda Help Desk Overflow.

L'ultimo comando dell'esempio infine chiama **Set-CsRgsQueue** per scrivere le modifiche nell'istanza effettiva della coda Help Desk Overflow in ApplicationServer:atl-cs-001.litwareinc.com.

    $x = Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk Overflow"
    $z = Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk"
    
    $w = New-CsRgsPrompt -TextToSpeechPrompt "Please hold while we transfer your call."
    $y = New-CsRgsCallAction -Prompt $w -Action TransferToQueue -QueueID $x.Identity
    $z.OverflowAction = $y
    Set-CsRgsQueue $z

## ESEMPIO 2

I comandi mostrati nell'esempio 2 sono analoghi a quelli dell'esempio 1. Nell'esempio 2 la nuova azione di chiamata però trasferisce la chiamata a un numero di telefono PSTN. A tale scopo, la proprietà Action della nuova azione di chiamata viene impostata su TransferToPSTN e la proprietà Uri su "sip:+14255551298@litwareinc.com".

    $w = New-CsRgsPrompt -TextToSpeechPrompt "Please hold while we transfer your call."
    $y = New-CsRgsCallAction -Prompt $w -Action TransferToPSTN -Uri "sip:+14255551298@litwareinc.com"
    $z = Get-CsRgsQueue -Identity service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk Queue"
    $z.OverflowAction = $y
    Set-CsRgsQueue $z

## Descrizione dettagliata

Quando viene chiamato un numero di telefono associato all'applicazione Response Group, quest'ultima ricerca il flusso di lavoro corrispondente al numero di telefono chiamato. Dopo che il flusso di lavoro viene trovato, il servizio controlla se la chiamata è stata ricevuta fuori dall'orario di ufficio o durante una festività. In caso affermativo, il servizio esegue l'azione specificata per le chiamate ricevute fuori dall'orario di ufficio o durante le festività. La chiamata può ad esempio essere trasferita direttamente alla segreteria telefonica. Se la chiamata è stata ricevuta durante l'orario di ufficio, l'applicazione Response Group esegue l'azione preconfigurata per le chiamate ricevute durante l'orario di ufficio. Tutte queste azioni vengono determinate in anticipo e create utilizzando il cmdlet **New-CsRgsCallAction**. **New-CsRgsCallAction** consente di inserire le chiamate in una coda di Response Group, di trasferirle alla segreteria telefonica, a un indirizzo SIP o a un numero di telefono PSTN (Public Switched Telephone Network), di trasferirle a una domanda del sistema IVR (Interactive Voice Response) oppure di chiuderle.

Quando si utilizza **New-CsRgsCallAction**, non si modificano direttamente le proprietà di un flusso di lavoro, di una coda o di un altro elemento dell'applicazione Response Group. La nuova azione di chiamata creata esiste inizialmente solo in memoria e deve essere archiviata in una variabile di riferimento oggetto, ad esempio $x. Al momento di apportare una modifica, ad esempio la proprietà DefaultAction di un flusso di lavoro, è quindi necessario assegnare il riferimento oggetto alla proprietà appropriata. Ad esempio,

\-DefaultAction $x

Si noti che le uniche due azioni di chiamata che è possibile assegnare alla proprietà DefaultAction sono TransferToQueue e TransferToQuestion. Tutte le altre azioni di chiamata ad eccezione di queste due sono valide per le operazioni da eseguire nelle festività o al di fuori dall'orario di ufficio. Tutte le azioni di chiamata, tranne TransferToQuestion, possono inoltre essere utilizzate per gli overflow e i timeout delle code.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsRgsCallAction** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Poiché tuttavia questo cmdlet crea un oggetto in memoria e da solo non apporta modifiche al sistema, può essere essenzialmente eseguito da chiunque. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsRgsCallAction"}

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
<td><p><em>Action</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.Action</p></td>
<td><p>Rappresenta l'azione di chiamata da eseguire. Il parametro Action deve essere impostato su uno dei seguenti valori:</p>
<p>Terminate – La chiamata viene terminata.</p>
<p>TransferToQueue – La chiamata viene trasferita alla coda di Response Group.</p>
<p>TransferToQuestion – La chiamata viene trasferita alla domanda di Response Group.</p>
<p>TransferToUri – La chiamata viene trasferita all'URI (Uniform Resource Identifier) SIP specificato.</p>
<p>TransferToVoiceMailUri – La chiamata viene trasferita alla segreteria telefonica.</p>
<p>TransferToPSTN – La chiamata viene trasferita a un telefono tradizionale PSTN (Public Switched Telephone Network).</p>
<p>Il parametro Action deve essere specificato ogni volta che si crea una nuova azione di chiamata. Non è previsto alcun valore predefinito.</p></td>
</tr>
<tr class="even">
<td><p><em>Prompt</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.Prompt</p></td>
<td><p>Prompt da riprodurre prima che si verifichi l'azione di chiamata. (Ad esempio, &quot;Attendere mentre la chiamata viene trasferita.&quot;) È necessario creare i prompt utilizzando il cmdlet <strong>New-CsRgsPrompt</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>Question</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.Question</p></td>
<td><p>Domanda da porre se l'azione è stata impostata su TransferToQuestion. È necessario creare la domanda utilizzando il cmdlet <strong>New-CsRgsQuestion</strong>.</p>
<p>Questo parametro è necessario se Action è impostato su TransferToQuestion.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueID</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>Identità della coda di Response Group a cui deve essere trasferita la chiamata, purché Action sia stato impostato su TransferToQueue. Il valore QueueID viene specificato meglio utilizzando <strong>Get-CsRgsQueue</strong> per recuperare l'identità della coda appropriata.</p>
<p>Tale parametro è obbligatorio se Action è impostato su TransferToQueue.</p></td>
</tr>
<tr class="odd">
<td><p><em>Uri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indirizzo SIP, URI della segreteria telefonica o numero di telefono PSTN a cui deve essere trasferita la chiamata.</p>
<p>Questo parametro è necessario se Action è stato impostato su TransferToUri, TransferToVoiceMailUri, o TransferToPSTN.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. **New-CsRgsCallAction** non accetta l'input da pipeline.

## Tipi restituiti

**New-CsRgsCallAction** crea nuove istanze dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.CallAction.

## Vedere anche

#### Ulteriori risorse

[New-CsRgsQueue](new-csrgsqueue.md)  
[Set-CsRgsQueue](set-csrgsqueue.md)

