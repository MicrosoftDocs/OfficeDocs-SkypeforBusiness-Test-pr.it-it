---
title: Remove-CsTrustedApplicationPool
TOCTitle: Remove-CsTrustedApplicationPool
ms:assetid: 93aa3381-e3fc-45df-840e-3d6d61a52fb3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398750(v=OCS.15)
ms:contentKeyID: 49301348
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsTrustedApplicationPool

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un pool contenente i computer che ospitano applicazioni attendibili. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsTrustedApplicationPool -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con questo esempio viene rimosso il pool con FQDN TrustPool.litwareinc.com. Viene utilizzato il parametro Identity per specificare il nome di dominio completo del pool da rimuovere. Poiché le identità sono univoche, con questo comando viene rimosso al massimo un pool.

    Remove-CsTrustedApplicationPool -Identity TrustPool.litwareinc.com

## ESEMPIO 2

In questo esempio vengono rimossi tutti i pool attendibili il cui nome di dominio completo inizia con la stringa "trust". La prima parte del comando è una chiamata al cmdlet **Get-CsTrustedApplicationPool**, che recupera una raccolta di tutti i pool di applicazioni attendibili nell'infrastruttura di Lync Server. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** verifica ogni elemento della raccolta per vedere se PoolFqdn corrisponde alla stringa con caratteri jolly trust\*. Il risultato è una raccolta di tutti i pool di applicazioni attendibili con un PoolFqdn che inizia con la stringa trust seguita da uno o più caratteri qualsiasi. Questa raccolta viene infine inviata tramite pipe al cmdlet **Remove-CsTrustedApplicationPool**, che rimuove ogni elemento della raccolta.

    Get-CsTrustedApplicationPool | Where-Object {$_.PoolFqdn -match "trust*"} | Remove-CsTrustedApplicationPool

## Descrizione dettagliata

È consigliabile che i computer che eseguono applicazioni attendibili all'interno di una distribuzione Lync Server vengano aggiunti a un pool distinto, destinato unicamente a questo tipo di applicazioni. È comunque possibile aggiungere i computer con applicazioni attendibili a un pool esistente, utilizzato anche per altri scopi. Questo cmdlet rimuove un pool di applicazioni attendibili esistente. Non è tuttavia possibile rimuovere un pool di applicazioni attendibili che non dispone di un valore per la funzione di registrazione. Se al pool di applicazioni attendibili non è stata assegnata una funzione di registrazione, è necessario aggiungere un valore a essa relativo con il cmdlet **Set-CsTrustedApplicationPool** e quindi rimuovere il pool.

Occorre ricordare che rimuovendo il pool vengono rimossi anche tutti i computer, le applicazioni e gli endpoint applicazione associati al pool.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Remove-CsTrustedApplicationPool** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsTrustedApplicationPool"}

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
<td><p>Il nome di dominio completo (FQDN) o l'ID del servizio del pool da rimuovere.</p></td>
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

Oggetto Microsoft.Rtc.Management.Xds.DisplayExternalServer. Consente di accettare l'input da pipeline di oggetti pool di applicazioni attendibili.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Rimuove un oggetto di tipo Microsoft.Rtc.Management.Xds.DisplayExternalServer.

## Vedere anche

#### Ulteriori risorse

[New-CsTrustedApplicationPool](new-cstrustedapplicationpool.md)  
[Set-CsTrustedApplicationPool](set-cstrustedapplicationpool.md)  
[Get-CsTrustedApplicationPool](get-cstrustedapplicationpool.md)

