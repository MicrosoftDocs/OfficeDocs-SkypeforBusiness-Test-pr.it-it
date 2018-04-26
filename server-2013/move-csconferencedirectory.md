---
title: Move-CsConferenceDirectory
TOCTitle: Move-CsConferenceDirectory
ms:assetid: c43207fa-06dd-4360-ae32-b2f17f7100d2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412968(v=OCS.15)
ms:contentKeyID: 49301918
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Move-CsConferenceDirectory

 

_**Ultima modifica dell'argomento:** 2015-05-28_

Sposta una directory conferenze esistente da un pool all'altro. Le directory conferenze vengono utilizzate per consentire agli utenti di conferenze telefoniche con accesso esterno di individuare le informazioni sulle conferenze. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Move-CsConferenceDirectory -Identity <XdsGlobalRelativeIdentity> -TargetPool <String> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 si sposta la directory conferenze con identità 3 nel pool atl-cs-002.litwareinc.com.

    Move-CsConferenceDirectory -Identity 3 -TargetPool atl-cs-002.litwareinc.com

## ESEMPIO 2

Il comando riportato nell'esempio 2 è una variante di quello mostrato nell'esempio 1. In questo caso è tuttavia incluso il parametro Force per garantire che lo spostamento venga eseguito anche se il pool di destinazione non è attualmente disponibile.

    Move-CsConferenceDirectory -Identity 3 -TargetPool atl-cs-002.litwareinc.com -Force

## ESEMPIO 3

Nell'esempio 3 vengono spostate tutte le directory conferenze esistenti nel pool di destinazione atl-cs-002.litwareinc.com. Per eseguire questa attività, nel comando viene utilizzato innanzitutto il cmdlet **Get-CsConferenceDirectory** per restituire una raccolta di tutte le directory conferenza attualmente in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Move-CsConferenceDirectory**, che sposta ogni directory della raccolta nel pool di destinazione.

    Get-CsConferenceDirectory | Move-CsConferenceDirectory -TargetPool atl-cs-002.litwareinc.com 

## Descrizione dettagliata

Quando si crea un URI (Uniform Resource Identifier) di conferenza telefonica con accesso esterno, a tale URI viene assegnato un indirizzo SIP univoco. Gli indirizzi SIP tuttavia sono difficili da interpretare nei dispositivi che non supportano il protocollo SIP. Un telefono di una rete PSTN (Public Switched Telephone Network) ad esempio non è in grado di interpretare un indirizzo SIP. Per questo motivo, in Lync Server vengono utilizzate le directory conferenza per semplificare l'individuazione e la connessione alle conferenze telefoniche con accesso esterno da parte di tali dispositivi. Per questo scopo si crea una directory conferenze SIP associata a ogni URI di conferenza telefonica con accesso esterno e identificata da un valore intero anziché da un URI SIP. I telefoni PSTN e altri dispositivi possono quindi utilizzare questi numeri anziché un URI SIP quando si connettono alle conferenze. Il numero della directory infatti viene incluso nell'ID conferenza PSTN immesso dagli utenti quando si connettono a una conferenza telefonica con accesso esterno.

A volte può essere necessario spostare una directory conferenza da un pool all'altro. Se ad esempio si rimuove un pool, potrebbe essere necessario spostare tutte le directory conferenza esistenti in un'altra posizione. Il cmdlet **Move-CsConferenceDirectory** consente di spostare le directory conferenza in un altro pool.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Move-CsConferenceDirectory** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Move-CsConferenceDirectory"}

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
<td><p>Identità numerica della directory conferenze da spostare.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetPool</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo (FQDN) del pool in cui deve essere spostata la directory conferenza. Ad esempio: -Identity atl-cs-002.litwareinc.com.</p></td>
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
<td><p>Se specificato, questo parametro consente di spostare la directory conferenza anche se il pool di destinazione non è attualmente disponibile. Per impostazione predefinita, il cmdlet <strong>Move-CsConferenceDirectory</strong> non sposta le directory se non è possibile contattare il pool di destinazione.</p>
<p>Prima di eseguire il cmdlet <strong>Move-CsConferenceDirectory</strong> con il parametro Force, è consigliabile utilizzare Dbimpexp.exe per esportare manualmente i dati legacy e quindi importarli nel pool di registrazione di destinazione. Dbimpexp.exe è disponibile nella directory radice del supporto di installazione di Lync Server.</p></td>
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

Nessuno. Il cmdlet **Move-CsConferenceDirectory** non accetta input da pipeline.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Get-CsConferenceDirectory](get-csconferencedirectory.md)  
[New-CsConferenceDirectory](new-csconferencedirectory.md)  
[Remove-CsConferenceDirectory](remove-csconferencedirectory.md)

