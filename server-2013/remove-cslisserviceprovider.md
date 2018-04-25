---
title: Remove-CsLisServiceProvider
TOCTitle: Remove-CsLisServiceProvider
ms:assetid: d26302bf-7794-4125-af80-ba7c92096b6d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398904(v=OCS.15)
ms:contentKeyID: 49302051
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsLisServiceProvider

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un oggetto contenente le informazioni sul servizio Web fornito dal provider del routing di rete Enhanced 9-1-1 (E9-1-1) per la verifica delle località. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsLisServiceProvider [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio il servizio Web del provider di servizi viene rimosso dall'implementazione del servizio di chiamate di emergenza. Ci sarà, al massimo, un solo provider di servizi definito, il quale verrà rimosso da questo cmdlet.

    Remove-CsLisServiceProvider

## Descrizione dettagliata

In un'implementazione VoIP aziendale con il servizio di chiamate di emergenza le chiamate di emergenza devono essere instradate innanzitutto attraverso un provider di routing di rete del servizio chiamate di emergenza per poter essere instradate al PSAP (Public Safety Answering Point) appropriato. Il centro PSAP è un centro che indirizza le chiamate ai servizi di emergenza più vicini: ad esempio, polizia, vigili del fuoco, servizio ambulanze. Perché ciò sia possibile, il provider deve disporre di un elenco delle posizioni fornito dall'organizzazione da poter confrontare con uno stradario informatico per assicurarsi che tutte le posizioni siano corrette. Questo cmdlet rimuove una voce relativa a un provider; dopo aver eseguito questo cmdlet, non vi sarà alcun accesso al servizio Web fornito dal provider.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsLisServiceProvider** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsLisServiceProvider"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
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

Accetta l'input da pipeline di un oggetto provider di servizi LIS (Location Information Server).

## Tipi restituiti

Questo cmdlet non restituisce alcun oggetto o valore. Rimuove un oggetto di tipo System.Management.Automation.PSCustomObject.

## Vedere anche

#### Ulteriori risorse

[Set-CsLisServiceProvider](set-cslisserviceprovider.md)  
[Get-CsLisServiceProvider](get-cslisserviceprovider.md)

