---
title: Remove-CsConferenceDirectory
TOCTitle: Remove-CsConferenceDirectory
ms:assetid: c2c62a14-f3f3-472f-bf91-1fcea9e45425
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412961(v=OCS.15)
ms:contentKeyID: 49301876
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConferenceDirectory

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una directory conferenze esistente. Le directory conferenze vengono utilizzate per consentire agli utenti di conferenze telefoniche con accesso esterno di individuare le informazioni sulle conferenze. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsConferenceDirectory -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 elimina la directory conferenza con valore Identity 2.

    Remove-CsConferenceDirectory -Identity 2

## ESEMPIO 2

Nell'esempio 2 vengono eliminate tutte le directory conferenza rilevate nel servizio UserServer:atl-cs-001.litwareinc.com. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsConferenceDirectory** senza alcun parametro. Quest'ultimo restituisce una raccolta di tutte le directory conferenza attualmente in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le directory ospitate nel servizio UserServer:atl-cs-001.litwareinc.com. A sua volta, la raccolta filtrata viene inviata tramite pipe al cmdlet **Remove-CsConferenceDirectory**, che la elimina.

    Get-CsConferenceDirectory | Where-Object {$_.ServiceID -match "UserServer:atl-cs-001.litwareinc.com"} | Remove-CsConferenceDirectory

## Descrizione dettagliata

Quando si crea un URI (Uniform Resource Identifier) di conferenza telefonica con accesso esterno, a tale URI viene assegnato un indirizzo SIP univoco. Gli indirizzi SIP tuttavia sono difficili da interpretare nei dispositivi che non supportano il protocollo SIP. Un telefono di una rete PSTN (Public Switched Telephone Network) ad esempio non è in grado di interpretare un indirizzo SIP. Per questo motivo, in Lync Server vengono utilizzate le directory conferenza per semplificare l'individuazione e la connessione alle conferenze telefoniche con accesso esterno da parte di tali dispositivi. Per questo scopo si crea una directory conferenze SIP associata a ogni URI di conferenza telefonica con accesso esterno e identificata da un valore intero anziché da un URI SIP. I telefoni PSTN e altri dispositivi possono quindi utilizzare questi numeri (anziché un URI SIP) quando si connettono alle conferenze. Il numero della directory infatti viene incluso nell'ID conferenza PSTN immesso dagli utenti quando si connettono a una conferenza telefonica con accesso esterno.

Le directory conferenza vengono create utilizzando il cmdlet **New-CsConferenceDirectory**. Potrebbe essere necessario a volte eliminare una o più di queste directory, ad esempio rimuovere il pool in cui sono ospitate. Le directory conferenza possono essere rimosse chiamando il cmdlet **Remove-CsConferenceDirectory**. Se si desidera solo spostare una directory da un pool a un altro, è possibile chiamare il cmdlet **Move-CsConferenceDirectory**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsConferenceDirectory** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsConferenceDirectory"}

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
<td><p>Identità numerica della directory conferenza da rimuovere.</p></td>
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
<td><p>Se presente, rimuove la directory conferenza anche se il pool che ospita la directory non è attualmente disponibile. Per impostazione predefinita, il cmdlet <strong>Remove-CsConferenceDirectory</strong> non rimuoverà le directory se non è possibile contattare il pool corrispondente.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.PstnConf.ConferenceDirectories. Il cmdlet **Remove-CsConferenceDirectory** accetta l'input da pipeline di oggetti directory conferenza.

## Tipi restituiti

Nessuno. Il cmdlet **Removes-CsConferenceDirectory** elimina piuttosto le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.PstnConf.ConferenceDirectories.

## Vedere anche

#### Ulteriori risorse

[Get-CsConferenceDirectory](get-csconferencedirectory.md)  
[Move-CsConferenceDirectory](move-csconferencedirectory.md)  
[New-CsConferenceDirectory](new-csconferencedirectory.md)

