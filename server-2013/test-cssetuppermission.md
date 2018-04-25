---
title: Test-CsSetupPermission
TOCTitle: Test-CsSetupPermission
ms:assetid: 604ccb97-278a-4588-9ab8-991aaabae275
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398428(v=OCS.15)
ms:contentKeyID: 49300724
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsSetupPermission

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica che le autorizzazioni necessarie per installare Lync Server o uno dei relativi componenti siano state configurate nel contenitore specificato di Active Directory. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsSetupPermission -ComputerOU <String> [-Domain <Fqdn>] [-DomainController <Fqdn>] [-GlobalCatalog <Fqdn>] [-Report <String>]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 viene verificato se le autorizzazioni di installazione richieste sono state applicate all'unità organizzativa CsServers nel dominio litwareinc.com.

    Test-CsSetupPermission -ComputerOU "ou=CsServers,dc=litwareinc,dc=com"

## Descrizione dettagliata

Con la preparazione del dominio che avviene quando si installa Lync Server, non vengono aggiunte automaticamente le autorizzazioni che consentono ai membri del gruppo RTCUniversalServerAdmins di eseguire il cmdlet **Enable-CsTopology**. Per questo motivo, per impostazione predefinita è necessario essere amministratori del dominio per abilitare una topologia. Per concedere ai membri del gruppo RTCUniversalServerAdmins il diritto di abilitare una topologia, è necessario eseguire il cmdlet **Grant-CsSetupPermissions**. Sarà inoltre necessario eseguire questo cmdlet per ogni contenitore di Active Directory che include computer in cui è in esecuzione Lync Server.

Il cmdlet **Test-CsSetupPermission** consente di determinare se le autorizzazioni richieste sono state aggiunte a un contenitore di Active Directory specificato, ovvero un contenitore che ospita i computer che eseguono Lync Server. Il cmdlet **Test-CsSetupPermission** restituisce True se sono state applicate le autorizzazioni corrette, altrimenti restituisce False. Se il cmdlet restituisce False, sarà necessario eseguire il cmdlet **Grant-CsSetupPermission** per apportare le modifiche necessarie al contenitore di Active Directory.

Utenti che possono eseguire questo cmdlet: Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsSetupPermission"}

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
<td><p>Nome distinto dell'unità organizzativa che contiene gli account per i computer su cui è in esecuzione Lync Server. Ad esempio: &quot;ou=CsServers,dc=litwareinc,dc=com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Domain</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome del dominio in cui è situata l'unità organizzativa da controllare. Se questo parametro non è incluso, il cmdlet <strong>Test-CsSetupPermission</strong> cercherà l'unità organizzativa nel dominio corrente.</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo (FQDN) di un controller di dominio nel dominio. Questo parametro non è obbligatorio se si esegue il cmdlet <strong>Test-CsSetupPermission</strong> in un computer con un account nel dominio.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo di un server di catalogo globale nel dominio. Questo parametro non è obbligatorio se si esegue il cmdlet <strong>Test-CsSetupPermission</strong> in un computer con un account nel dominio.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di segnalare l'attività dettagliata sullo schermo durante l'esecuzione del cmdlet.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsSetupPermission** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Test-CsSetupPermission** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Grant-CsSetupPermission](grant-cssetuppermission.md)  
[Revoke-CsSetupPermission](revoke-cssetuppermission.md)

