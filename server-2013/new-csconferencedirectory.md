---
title: New-CsConferenceDirectory
TOCTitle: New-CsConferenceDirectory
ms:assetid: fd5a4369-10cd-4337-94df-51bcaee4fde9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413080(v=OCS.15)
ms:contentKeyID: 49302573
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsConferenceDirectory

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova directory conferenze da utilizzare nell'organizzazione. Le directory conferenze vengono utilizzate per consentire agli utenti di conferenze telefoniche con accesso esterno di individuare le informazioni sulle conferenze. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsConferenceDirectory -HomePool <String> -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Viene creata una nuova directory conferenze con identità 42. Tale directory verrà ospitata nel pool atl-cs-001.litwareinc.com.

    New-CsConferenceDirectory -Identity 42 -HomePool "atl-cs-001.litwareinc.com"

## Descrizione dettagliata

Quando si crea un URI (Uniform Resource Identifier) di conferenza telefonica con accesso esterno, a tale URI vengono assegnati indirizzi SIP univoci. Tuttavia, gli indirizzi SIP sono difficili da convertire nei dispositivi che non supportano SIP. Ad esempio, un indirizzo SIP non può essere compreso da un telefono PSTN (Public Switched Telephone Network). Per questo motivo, Lync Server utilizza le directory conferenze allo scopo di semplificare l'individuazione e la connessione alle conferenze telefoniche con accesso esterno da parte di tali dispositivi. Per questo scopo si crea una directory conferenze SIP associata a ogni URI di conferenza telefonica con accesso esterno e identificata da un valore intero anziché da un URI SIP. I telefoni PSTN e altri dispositivi possono utilizzare questi numeri (piuttosto che un URI SIP) quando si connettono alle conferenze; infatti, il numero della directory viene incluso nell'ID conferenza PSTN che gli utenti immettono quando si connettono ad una conferenza con accesso esterno.

È possibile creare nuove directory conferenze chiamando il cmdlet **New-CsConferenceDirectory**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **New-CsConferenceDirectory** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsConferenceDirectory"}

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
<td><p><em>HomePool</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo del pool di registrazione in cui verrà ospitata la nuova directory conferenze. Ad esempio: -Identity atl-cs-001.litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificatore numerico univoco per la nuova directory conferenze. Le identità possono essere rappresentate da qualsiasi valore intero compreso tra 0 e 9999 inclusi. Tuttavia, le identità devono essere univoche. As esempio, non è possibile avere due directory con l'identità 575. Non è necessario seguire un ordine numerico quando si creano nuove directory. Ad esempio, è possibile creare una directory con l'identità 999 seguita da una directory con identità 2, seguita ancora da una directory con identità 438 e così via.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsConferenceDirectory** non accetta input inviato tramite pipe.

## Tipi restituiti

Crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.PstnConf.ConferenceDirectories.

## Vedere anche

#### Ulteriori risorse

[Get-CsConferenceDirectory](get-csconferencedirectory.md)  
[Move-CsConferenceDirectory](move-csconferencedirectory.md)  
[Remove-CsConferenceDirectory](remove-csconferencedirectory.md)

