---
title: Get-CsAdminRoleAssignment
TOCTitle: Get-CsAdminRoleAssignment
ms:assetid: 61374f9b-e85a-4866-91f2-037a862ba0d6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398434(v=OCS.15)
ms:contentKeyID: 49300740
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAdminRoleAssignment

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce i ruoli di controllo di accesso basato sui ruoli (RBAC, Role-Based Access Control) assegnati a un utente. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsAdminRoleAssignment -Identity <String> [-Force <SwitchParameter>] [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 vengono restituiti tutti i ruoli RBAC assegnati all'utente kenmyer.

    Get-CsAdminRoleAssignment -Identity "kenmyer"

## ESEMPIO 2

Nell'esempio 2 vengono restituiti i ruoli RBAC per tutti gli utenti abilitati per Lync Server. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsUser** senza alcun parametro. In questo modo viene restituita una raccolta di tutti gli utenti dell'organizzazione abilitati per Lync Server o per Office Communications Server. Questi dati vengono inviati tramite pipe al cmdlet **ForEach-Object**, che esegue un ciclo tra ogni account utente della raccolta ed effettua le operazioni seguenti: 1) riporta il nome visualizzato dell'utente sullo schermo e 2) utilizza il cmdlet **Get-CsAdminRoleAssignment** per restituire i ruoli RBAC dell'utente. Le informazioni sull'account utente devono essere inviate tramite pipe al cmdlet **ForEach-Object** perché il cmdlet **Get-CsAdminRoleAssignment** non accetta direttamente i dati inviati tramite pipeline.

    Get-CsUser | ForEach-Object {$_.DisplayName; Get-CsAdminRoleAssignment -Identity $_.SamAccountName}

## Descrizione dettagliata

Il controllo di accesso basato sui ruoli (RBAC) consente agli amministratori di delegare il controllo di attività di gestione specifiche per Lync Server. Ad esempio, invece di concedere al personale dell'Help Desk dell'organizzazione privilegi completi di amministratore, è possibile concedere loro diritti molto specifici: il diritto di gestire esclusivamente gli account utente, il diritto di gestire esclusivamente i componenti di VoIP aziendale e il diritto di gestire esclusivamente l'archiviazione e il server di archiviazione. Tali diritti inoltre possono essere limitati nell'ambito: a un utente potrebbe essere conferito il diritto di gestire VoIP aziendale, ma solo nel sito Redmond, mentre un altro potrebbe ricevere il diritto di gestire gli account utente, ma solo se tali account appartengono all'unità organizzativa Finance.

Il cmdlet **Get-CsAdminRoleAssignment** offre un modo per recuperare i ruoli RBAC assegnati a un utente.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Get-CsAdminRoleAssignment** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAdminRoleAssignment"}

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
<td><p>System.String</p></td>
<td><p>SamAccountName dell'utente per cui restituire i ruoli RBAC. È possibile recuperare il SamAccountName per un utente utilizzando un comando simile al seguente:</p>
<p>Get-CsUser &quot;Ken Myer&quot; | Select-Object SamAccountName</p>
<p>È necessario utilizzare il SamAccountName per specificare l'identità dell'utente. Altri valori comuni utilizzati per specificare le identità (ad esempio il nome visualizzato di Active Directory o l'indirizzo SIP dell'utente) non funzionano con <strong>Get-CsAdminRoleAssignment</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati delle assegnazioni di ruoli RBAC dalla replica locale del archivio di gestione centrale anziché dal archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Stringa. Il cmdlet **Get-CsAdminRoleAssignment** accetta l'input un valore stringa inviato tramite pipeline che rappresenta il nome di account SAM (SamAccountName) di un utente.

## Tipi restituiti

Il cmdlet **Get-CsAdminRoleAssignment** restituisce valori stringa che rappresentano i ruoli RBAC assegnati all'utente specificato.

## Vedere anche

#### Ulteriori risorse

[Get-CsAdminRole](get-csadminrole.md)

