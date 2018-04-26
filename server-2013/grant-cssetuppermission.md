---
title: Grant-CsSetupPermission
TOCTitle: Grant-CsSetupPermission
ms:assetid: 753bccc1-edb4-48c9-bd0a-2db5d86f8c5e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398569(v=OCS.15)
ms:contentKeyID: 49300999
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsSetupPermission

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Concede le autorizzazioni di installazione di Lync Server per un'unità organizzativa di Active Directory. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Grant-CsSetupPermission -ComputerOU <String> [-Confirm [<SwitchParameter>]] [-Domain <Fqdn>] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 vengono concesse le autorizzazioni di installazione per l'unità organizzativa CsServers nel dominio litwareinc.com.

    Grant-CsSetupPermission -ComputerOU "ou=CsServers,dc=litwareinc,dc=com"

## Descrizione dettagliata

Con la preparazione del dominio che avviene quando si installa Lync Server, non vengono aggiunte automaticamente le autorizzazioni che consentono ai membri del gruppo RTCUniversalServerAdmins di eseguire il cmdlet **Enable-CsTopology**. Per questo motivo, per impostazione predefinita è necessario essere amministratori del dominio per abilitare una topologia. Per concedere ai membri del gruppo RTCUniversalServerAdmins il diritto di abilitare una topologia, è necessario eseguire il cmdlet **Grant-CsSetupPermissions**. Sarà inoltre necessario eseguire questo cmdlet per ogni contenitore di Active Directory che include computer in cui è in esecuzione Lync Server.

Questo cmdlet concede esclusivamente le autorizzazioni al gruppo RTCUniversalServerAdmins; non può essere utilizzato per concedere le autorizzazioni ad altri gruppi di sicurezza o a singoli utenti.

Utenti che possono eseguire questo cmdlet: il cmdlet **Grant-CsSetupPermission** può essere eseguito in locale solo dagli amministratori del dominio. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsSetupPermission"}

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
<td><p><em>ComputerOU</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il nome distinto dell'unità organizzativa che contiene gli account per i computer in cui sarà installato (o è stato installato) Lync Server. Ad esempio: &quot;ou=CsServers,dc=litwareinc,dc=com&quot;.</p>
<p>Se si preferisce è possibile tralasciare la parte del dominio dal nome distinto quando si specifica l'unità organizzativa. Ad esempio:</p>
<p>-ComputerOU &quot;ou=CsServers&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Domain</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome del dominio in cui è situata l'unità organizzativa. Se questo parametro non è incluso, il cmdlet <strong>Grant-CsSetupPermission</strong> cercherà l'unità organizzativa nel dominio corrente.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome completo del controller di dominio da contattare durante l'assegnazione dei criteri. Ad esempio: -DomainController atl-dc-001.litwareinc.com.</p>
<p>Se non viene specificato, il cmdlet <strong>Grant-CsSetupPermission</strong> contatterà il controller di dominio disponibile più vicino durante l'assegnazione del criterio.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di ignorare la visualizzazione di messaggi di errore non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome completo del server di catalogo globale da contattare durante l'assegnazione dei criteri. Ad esempio: -GlobalCatalog atl-dc-001.litwareinc.com.</p>
<p>Se non viene specificato, il cmdlet <strong>Grant-CsSetupPermission</strong> contatterà il server di catalogo globale disponibile più vicino durante l'assegnazione del criterio.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\SetupPermissions.html&quot;</p></td>
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

Nessuno. Il cmdlet **Grant-CsSetupPermission** non accetta input tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Grant-CsSetupPermission** non restituisce alcun oggetto o valore.

## Vedere anche

#### Ulteriori risorse

[Revoke-CsSetupPermission](revoke-cssetuppermission.md)  
[Test-CsSetupPermission](test-cssetuppermission.md)

