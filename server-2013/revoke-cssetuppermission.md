---
title: Revoke-CsSetupPermission
TOCTitle: Revoke-CsSetupPermission
ms:assetid: 3486d164-b1a2-4d4c-9150-cef802674682
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425834(v=OCS.15)
ms:contentKeyID: 49300135
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Revoke-CsSetupPermission

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Revoca i diritti di installazione di Lync Server concessi per un'unità organizzativa di Active Directory. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Revoke-CsSetupPermission -ComputerOU <String> [-Confirm [<SwitchParameter>]] [-Domain <Fqdn>] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando illustrato nell'esempio 1 consente di revocare i diritti di installazione applicati all'unità organizzativa CsServers nel dominio litwareinc.com.

    Revoke-CsSetupPermission -ComputerOU "ou=CsServers,dc=litwareinc,dc=com"

## Descrizione dettagliata

Con la preparazione del dominio eseguita quando si installa Lync Server non vengono aggiunti automaticamente i diritti che consentono ai membri del gruppo RTCUniversalServerAdmins di eseguire il cmdlet **Enable-CsTopology**. Per questo motivo, per impostazione predefinita è necessario essere amministratori di dominio per abilitare una topologia. Per concedere ai membri del gruppo RTCUniversalServerAdmins il diritto di abilitare una topologia, è necessario eseguire il cmdlet **Grant-CsSetupPermissions**. È inoltre necessario eseguire questo cmdlet in ogni contenitore di Active Directory che ospita computer in cui è in esecuzione Lync Server.

I diritti concessi utilizzando il cmdlet **Grant-CsSetupPermission** possono essere successivamente rimossi utilizzando il cmdlet **Revoke-CsSetupPermission**. Se si esegue tale cmdlet, il gruppo RTCUniversalServerAdmins non disporrà più dei diritti di installazione di Lync Server per il contenitore di Active Directory specificato. In questo caso, è necessario essere un amministratore dell'organizzazione o del dominio per abilitare una topologia di Lync Server.

Utenti che possono eseguire questo cmdlet: il cmdlet **Revoke-CsSetupPermission** può essere eseguito in locale solo dagli amministratori del dominio. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Revoke-CsSetupPermission"}

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
<td><p>Nome distinto dell'unità organizzativa che contiene gli account per i computer in cui sarà installato (o è stato installato) Lync Server. Ad esempio: -ComputerOU &quot;ou=CsServers,dc=litwareinc,dc=com&quot;.</p>
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
<td><p>Nome del dominio in cui si trova l'unità organizzativa. Se questo parametro non viene incluso, il cmdlet <strong>Revoke-CsSetupPermission</strong> cercherà l'unità organizzativa nel dominio corrente.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome completo del controller di dominio da contattare durante l'assegnazione dei criteri. Ad esempio: -DomainController atl-dc-001.litwareinc.com.</p>
<p>Se questo parametro non viene specificato, il cmdlet <strong>Revoke-CsSetupPermission</strong> contatterà il controller di dominio disponibile più vicino durante l'assegnazione del criterio.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome completo del server di catalogo globale da contattare durante l'assegnazione dei criteri. Ad esempio: -GlobalCatalog atl-dc-001.litwareinc.com.</p>
<p>Se questo parametro non viene specificato, il cmdlet <strong>Revoke-CsSetupPermission</strong> contatterà il server di catalogo globale disponibile più vicino durante l'assegnazione del criterio.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\OUPermissions.html&quot;</p></td>
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

Nessuno. Il cmdlet **Revoke-CsSetupPermission** non accetta input da pipeline.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Grant-CsSetupPermission](grant-cssetuppermission.md)  
[Test-CsSetupPermission](test-cssetuppermission.md)

