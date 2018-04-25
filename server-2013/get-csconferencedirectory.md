---
title: Get-CsConferenceDirectory
TOCTitle: Get-CsConferenceDirectory
ms:assetid: 2b7927ab-c6b3-42ce-9c27-9825cd47fd77
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425771(v=OCS.15)
ms:contentKeyID: 49300025
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConferenceDirectory

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle directory conferenze configurate per l'utilizzo nell'organizzazione. Le directory conferenze vengono utilizzate per consentire agli utenti di conferenze telefoniche con accesso esterno di individuare le informazioni sulle conferenze. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsConferenceDirectory [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsConferenceDirectory [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 restituisce le informazioni su tutte le directory conferenza configurate per l'utilizzo nella propria organizzazione.

    Get-CsConferenceDirectory

## ESEMPIO 2

Nell'Esempio 2 vengono restituite le informazioni sulla directory conferenza con Identity 2. Dal momento che le identità devono essere univoche, questo comando non restituirà mai più di una singola directory conferenza.

    Get-CsConferenceDirectory -Identity 2

## ESEMPIO 3

Nell'esempio 3 vengono restituite tutte le directory conferenze ospitate nel servizio UserServer:atl-cs-001.litwareinc.com. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsConferenceDirectory** senza alcun parametro per restituire una raccolta di tutte le directory conferenze incluse nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le directory in cui ServiceID è uguale al valore stringa "UserServer:atl-cs-001.litwareinc.com".

    Get-CsConferenceDirectory | Where-Object {$_.ServiceID -match "UserServer:atl-cs-001.litwareinc.com"}

## Descrizione dettagliata

Quando si crea un URI di conferenze telefoniche con accesso esterno, all'URI viene assegnato un indirizzo SIP univoco. Gli indirizzi SIP tuttavia sono difficili da convertire per i dispositivi non abilitati per SIP. Un telefono PSTN (Public Switched Telephone Network) ad esempio non è in grado di convertire un indirizzo SIP. Per questo motivo, Lync Server utilizza le directory conferenze per consentire a questi dispositivi di individuare le conferenze telefoniche con accesso esterno e connettersi a esse. Per ottenere questo risultato, viene creata una directory conferenze SIP associata a ogni URI di conferenze telefoniche con accesso esterno che viene identificata come numero intero piuttosto che come un URI SIP. I telefoni e altri dispositivi di tipo PSTN possono utilizzare questi numeri (anziché un URI SIP) quando si connettono alle conferenze. Il numero della directory infatti viene incluso nell'ID conferenza PSTN che gli utenti immettono quando si connettono a una conferenza telefonica con accesso esterno.

Il cmdlet **Get-CsConferenceDirectory** consente di ottenere informazioni su tutte le directory conferenza configurate per l'utilizzo nella propria organizzazione.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsConferenceDirectory** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsConferenceDirectory"}

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare i caratteri jolly per specificare l'identità della directory (o delle directory) conferenza da ottenere. Dal momento che le identità delle directory sono valori numerici, questo parametro potrebbe avere il valore minimo. Tuttavia, questa sintassi restituirà tutte le directory conferenza la cui identità inizia con il numero 3: -Filter &quot;3*&quot;.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificatore numerico (ad esempio, 7) della directory conferenze da restituire. Se questo parametro viene omesso, il cmdlet <strong>Get-CsConferenceDirectory</strong> restituisce informazioni su tutte le directory conferenze in uso nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati la directory conferenza dalla replica locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsConferenceDirectory** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsConferenceDirectory** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.PstnConf.ConferenceDirectories.

## Vedere anche

#### Ulteriori risorse

[Move-CsConferenceDirectory](move-csconferencedirectory.md)  
[New-CsConferenceDirectory](new-csconferencedirectory.md)  
[Remove-CsConferenceDirectory](remove-csconferencedirectory.md)

