---
title: Remove-CsTrustedApplicationComputer
TOCTitle: Remove-CsTrustedApplicationComputer
ms:assetid: c9c0604b-a94e-42b9-9db3-bc3dbe686e41
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398838(v=OCS.15)
ms:contentKeyID: 49301976
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsTrustedApplicationComputer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove il computer di un'applicazione attendibile. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsTrustedApplicationComputer -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Questo esempio mostra la rimozione del computer con nome di dominio completo (FQDN) Trust1.litwareinc.com.

    Remove-CsTrustedApplicationComputer -Identity Trust1.litwareinc.com

## ESEMPIO 2

In questo esempio vengono rimossi tutti i computer attendibili i cui nomi di dominio completi (FQDN) iniziano con la stringa Trust. Nella parte iniziale dell'esempio viene chiamato il cmdlet **Get-CsTrustedApplicationComputer** e viene passato il valore Trust\* al parametro Filter. Questa operazione consentirà di recuperare tutti i computer delle applicazioni attendibili con un nome dominio completo (FQDN) che inizia con Trust e che termina con un set qualunque di caratteri. La raccolta di computer viene quindi inviata tramite pipe al cmdlet **Remove-CsTrustedApplicationComputer**, che rimuove ogni elemento (ovvero ogni computer) della raccolta. Tenere presente che il cmdlet non rimuoverà i computer da un pool se la rimozione producesse come risultato un pool vuoto.

    Get-CsTrustedApplicationComputer -Filter Trust* | Remove-CsTrustedApplicationComputer

## Descrizione dettagliata

È consigliabile che i computer che eseguono applicazioni attendibili in una distribuzione di Lync Server vengano aggiunti a un pool distinto, destinato unicamente a questo tipo di applicazioni. È tuttavia possibile aggiungere i computer con applicazioni attendibili a un pool esistente utilizzato anche per altri scopi. Utilizzare questo cmdlet per rimuovere il computer di un'applicazione attendibile.

Quando si utilizza questo cmdlet per rimuovere il computer di un'applicazione attendibile, quest'ultimo verrà rimosso non solo dall'elenco dei computer delle applicazioni attendibili, ma anche dall'elenco dei computer disponibili in Lync Server. In altre parole, se si chiama il cmdlet **Get-CsTrustedApplicationComputer** o il cmdlet **Get-CsComputer**, il computer non comparirà più nell'elenco. Non è possibile rimuovere il computer di un'applicazione attendibile se è il solo computer del pool. Se si desidera rimuovere l'unico computer di un pool, è necessario rimuovere l'intero pool. A tale scopo, chiamare il cmdlet **Remove-CsTrustedApplicationPool**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsTrustedApplicationComputer** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsTrustedApplicationComputer"}

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
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nome di dominio completo (FQDN) del computer da rimuovere.</p></td>
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
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
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

Oggetto Microsoft.Rtc.Management.Xds.DisplayComputer. Accetta l'input da pipeline di oggetti computer con applicazioni attendibili.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Rimuove un oggetto di tipo Microsoft.Rtc.Management.Xds.DisplayComputer.

## Vedere anche

#### Ulteriori risorse

[New-CsTrustedApplicationComputer](new-cstrustedapplicationcomputer.md)  
[Get-CsTrustedApplicationComputer](get-cstrustedapplicationcomputer.md)  
[Remove-CsTrustedApplicationPool](remove-cstrustedapplicationpool.md)  
[Get-CsTrustedApplicationPool](get-cstrustedapplicationpool.md)

