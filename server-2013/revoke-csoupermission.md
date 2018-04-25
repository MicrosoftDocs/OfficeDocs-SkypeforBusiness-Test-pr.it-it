---
title: Revoke-CsOUPermission
TOCTitle: Revoke-CsOUPermission
ms:assetid: de0542c9-6d11-4038-9b4a-757338d61fae
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398977(v=OCS.15)
ms:contentKeyID: 49302211
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Revoke-CsOUPermission

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Revoca le autorizzazioni di gestione di Lync Server che sono state concesse per un'unità organizzativa Active Directory. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Revoke-CsOUPermission -ObjectType <User | Computer | InetOrgPerson | Contact | AppContact | Device> -OU <String> [-Confirm [<SwitchParameter>]] [-Domain <Fqdn>] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 revoca le autorizzazioni per la gestione degli utenti (-ObjectType "user") per l'unità organizzativa Redmond nel dominio litwareinc.com.

    Revoke-CsOUPermission -OU "ou=Redmond,dc=litwareinc,dc=com" -ObjectType "user"

## ESEMPIO 2

Nell'esempio 2 vengono rimosse tre diverse autorizzazioni di gestione (oggetti utente, contatto e inetOrgPerson) dall'unità organizzativa Redmond nel dominio litwareinc.com.

    Revoke-CsOUPermission -OU "ou=Redmond,dc=litwareinc,dc=com" -ObjectType "user","contact","inetOrgPerson"

## Descrizione dettagliata

Se il dominio Active Directory in uso è stato bloccato disabilitando l'ereditarietà delle autorizzazioni, la preparazione del dominio che avviene durante l'installazione di Lync Server non sarà in grado di aggiungere le autorizzazioni necessarie per gestire utenti, computer, contatti, contatti dell'applicazione e persone InetOrg. Gli amministratori dell'organizzazione e gli amministratori di dominio potranno comunque gestire tali oggetti, ma nessun altro, inclusi i membri del gruppo RTCUniversalServerAdmins, disporrà delle autorizzazioni di gestione. In tal caso, sarà necessario utilizzare il cmdlet **Grant-CsOUPermission** per concedere ai gruppi di sicurezza appropriati le autorizzazioni richieste. Questa operazione deve essere eseguita per ogni singolo contenitore Active Directory con account utente di Lync Server.

Le autorizzazioni concesse utilizzando il cmdlet **Grant-CsOUPermission** possono essere successivamente rimosse utilizzando il cmdlet **Revoke-CsOUPermission**. Se si esegue il cmdlet **Revoke-CsOUPermission** per un'unità organizzativa, sarà necessario essere amministratori dell'organizzazione o amministratori di dominio per poter gestire gli utenti di Lync Server in tale unità organizzativa.

Utenti autorizzati a eseguire il cmdlet: per poter eseguire localmente il cmdlet **Revoke-CsOUPermission**, è necessario essere amministratori di dominio. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Revoke-CsOUPermission"}

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
<td><p>Tipo di oggetto coperto da queste autorizzazioni. I valori validi sono:</p>
<p>User</p>
<p>Computer</p>
<p>Contact</p>
<p>AppContact</p>
<p>InetOrgPerson</p>
<p>Per revocare le autorizzazioni per più tipi di oggetti nello stesso comando, separare i tipi di oggetto utilizzando virgole: -ObjectType &quot;user&quot;,&quot;computer&quot;,&quot;contact&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome distinto dell'unità organizzativa in cui rimuovere le autorizzazioni. Ad esempio: -OU &quot;ou=Redmond,dc=litwareinc,dc=com&quot;. Con un singolo comando è possibile rimuovere autorizzazioni da una sola unità organizzativa.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Domain</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome del dominio in cui si trova l'unità organizzativa. Se questo parametro non è incluso, il cmdlet <strong>Revoke-CsOUPermission</strong> cercherà l'unità organizzativa nel dominio corrente.</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente agli amministratori di specificare il nome di dominio completo (FQDN) del controller di dominio da utilizzare quando si esegue il cmdlet <strong>Revoke-CsOUPermission</strong>. Se non viene specificato, il cmdlet utilizzerà il primo controller di dominio disponibile.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Il nome di dominio completo di un server di catalogo globale nel dominio in uso. Questo parametro non è necessario se si esegue il cmdlet <strong>Revoke-CsOUPermission</strong> in un computer con un account nel dominio.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\OUPermissions.html&quot;</p></td>
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

Nessuno. Il cmdlet **Revoke-CsOUPermission** non accetta input inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **Revoke-CsOUPermission** non restituisce alcun oggetto o valore.

## Vedere anche

#### Ulteriori risorse

[Grant-CsOUPermission](grant-csoupermission.md)  
[Test-CsOUPermission](test-csoupermission.md)

