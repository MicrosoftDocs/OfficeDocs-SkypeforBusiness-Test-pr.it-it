---
title: Test-CsOUPermission
TOCTitle: Test-CsOUPermission
ms:assetid: 9908eac9-765e-4406-bb6b-0e4dd07f85f8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398787(v=OCS.15)
ms:contentKeyID: 49301434
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsOUPermission

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica che le autorizzazioni necessarie per gestire utenti, computer e altri oggetti siano state impostate nel contenitore di Active Directory specificato. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsOUPermission -ObjectType <User | Computer | InetOrgPerson | Contact | AppContact | Device> -OU <String> [-Domain <Fqdn>] [-DomainController <Fqdn>] [-GlobalCatalog <Fqdn>] [-Report <String>]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 viene verificata l'impostazione delle autorizzazioni utente impostate sull'unità organizzativa Redmond nel dominio litwareinc.com.

    Test-CsOUPermission -OU "ou=Redmond,dc=litwareinc,dc=com" -ObjectType "user"

## Descrizione dettagliata

Se il dominio di Active Directory in uso è stato bloccato (disabilitando l'ereditarietà delle autorizzazioni), la preparazione del dominio che avviene durante l'installazione di Lync Server non sarà in grado di aggiungere le autorizzazioni necessarie per gestire utenti, computer, contatti, contatti dell'applicazione e persone InetOrg. Gli amministratori di dominio potranno ancora gestire questi oggetti, ma nessun altro, compresi i membri del gruppo RTCUniversalServerAdmins, disporrà delle autorizzazioni di gestione. In tal caso, è necessario utilizzare il cmdlet [Grant-CsOUPermission](grant-csoupermission.md) per concedere le autorizzazioni appropriate al gruppo RTCUniversalServerAdmins. Sarà inoltre necessario eseguire questa operazione contenitore per contenitore.

Il cmdlet **Test-CsOUPermission** consente di determinare se le autorizzazioni necessarie sono state aggiunte o meno a un contenitore di Active Directory specificato. Il cmdlet **Test-CsOUPermission** restituisce True se sono state applicate le autorizzazioni corrette, altrimenti restituisce False. Se il cmdlet restituisce False, sarà necessario eseguire il cmdlet [Grant-CsOUPermission](grant-csoupermission.md) per apportare le modifiche necessarie.

Utenti che possono eseguire questo cmdlet: Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsOUPermission"}

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
<td><p><em>ObjectType</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.ObjectType</p></td>
<td><p>Tipo di oggetti da controllare. I valori validi sono:</p>
<p>User</p>
<p>Computer</p>
<p>Contact</p>
<p>AppContact</p>
<p>InetOrgPerson</p>
<p>Per controllare più oggetti dello stesso tipo, separarli utilizzando una virgola: -ObjectType &quot;user&quot;,&quot;computer&quot;,&quot;contact&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome distinto dell'unità organizzativa da controllare. Ad esempio: -OU &quot;ou=Redmond,dc=litwareinc,dc=com&quot;.</p>
<p>È possibile controllare una sola unità organizzativa per comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Domain</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome del dominio in cui è situata l'unità organizzativa da controllare. Se questo parametro non è incluso, il cmdlet <strong>Test-CsOUPermission</strong> cercherà l'unità organizzativa nel dominio corrente.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo (FQDN) di un controller di dominio nel dominio. Questo parametro non è obbligatorio se si esegue il cmdlet <strong>Test-CsOUPermission</strong> in un computer con un account nel dominio.</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo di un server di catalogo globale nel dominio. Questo parametro non è obbligatorio se si esegue il cmdlet <strong>Test-CsOUPermission</strong> in un computer con un account nel dominio.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\OUPermissions.html&quot;. Se il file esiste, viene sovrascritto durante l'esecuzione del cmdlet.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsOUPermission** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Test-CsOUPermission** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Grant-CsOUPermission](grant-csoupermission.md)  
[Revoke-CsOUPermission](revoke-csoupermission.md)

