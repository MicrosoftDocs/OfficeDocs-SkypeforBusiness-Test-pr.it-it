---
title: Grant-CsOUPermission
TOCTitle: Grant-CsOUPermission
ms:assetid: 26d8bdbf-abf0-4ca3-b9ab-fbb355fbcca1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425739(v=OCS.15)
ms:contentKeyID: 49299971
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsOUPermission

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Concede i diritti di gestione di Lync Server per un'unità organizzativa di Active Directory. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Grant-CsOUPermission -ObjectType <User | Computer | InetOrgPerson | Contact | AppContact | Device> -OU <String> [-Confirm [<SwitchParameter>]] [-Domain <Fqdn>] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando illustrato nell'esempio 1 consente di concedere i diritti di gestione utente (-ObjectType "user") nell'unità organizzativa Redmond nel dominio litwareinc.com.

    Grant-CsOUPermission -OU "ou=Redmond,dc=litwareinc,dc=com" -ObjectType "user"

## ESEMPIO 2

Nell'esempio 2 i diritti di gestione vengono concessi per tre oggetti diversi (user, contact, inetOrgPerson) per l'unità organizzativa Redmond nel dominio litwareinc.com.

    Grant-CsOUPermission -OU "ou=Redmond,dc=litwareinc,dc=com" -ObjectType "user","contact","inetOrgPerson"

## ESEMPIO 3

Nell'esempio 3 i diritti di gestione utente vengono concessi contemporaneamente a tre unità organizzative diverse: Redmond, Dublin e Tokyo. Per ottenere questo risultato, il primo comando nell'esempio crea una variabile di matrice denominata $x. Questa variabile include i nomi distinti delle tre unità organizzative di Active Directory in cui verranno concessi i diritti. Il secondo comando crea un ciclo foreach che seleziona ogni unità organizzativa archiviata nella matrice ed esegue il cmdlet **Grant-CsOUPermission** per tale unità organizzativa. Il comando a sua volta concede i diritti di gestione utente per ogni unità organizzativa della matrice.

    $x = "ou=Redmond,dc=litwareinc,dc=com", "ou=Dublin,dc=litwareinc,dc=com", "ou=Tokyo,dc=litwareinc,dc=com"
    
    foreach ($i in $x) {Grant-CsOUPermission -OU $i -ObjectType "user"}

## Descrizione dettagliata

Se il dominio Active Directory in uso è stato bloccato (disabilitando l'ereditarietà delle autorizzazioni), la preparazione del dominio che viene effettuata durante l'installazione di Lync Server non sarà in grado di aggiungere i diritti necessari per gestire utenti, computer, contatti, contatti dell'applicazione e persone InetOrg. Gli amministratori di dominio saranno comunque in grado di gestire questi oggetti, ma nessun altro, neanche i membri del gruppo RTCUniversalUserAdmins, disporrà di diritti di gestione. In questo caso, sarà necessario utilizzare il cmdlet **Grant-CsOUPermission** per concedere ai gruppi di sicurezza necessari i diritti appropriati. Questa operazione deve essere eseguita per ogni contenitore.

Si noti che questo cmdlet consente di concedere i diritti solo a un insieme predefinito di gruppi di sicurezza e non può essere utilizzato per concedere diritti a gruppi di sicurezza arbitrari o a singoli utenti.

I diritti concessi utilizzando il cmdlet **Grant-CsOUPermission** possono essere successivamente rimossi utilizzando il cmdlet **Revoke-CsOUPermission**. Se si esegue tale cmdlet, i gruppi a cui inizialmente erano stati concessi i diritti per l'unità organizzativa non disporranno più di quei diritti di gestione di Lync Server per il contenitore di Active Directory specificato. In questo caso, è necessario essere un amministratore dell'organizzazione o del dominio per gestire Lync Server o uno dei relativi componenti.

Utenti autorizzati a utilizzare questo cmdlet: È necessario essere amministratori di dominio per poter utilizzare localmente il cmdlet **Grant-CsOUPermission**. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsOUPermission"}

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
<td><p>Tipo di oggetto che dispone dei diritti. I valori validi sono:</p>
<p>User</p>
<p>Computer</p>
<p>Contact</p>
<p>AppContact</p>
<p>InetOrgPerson</p>
<p>Device (obbligatorio per la creazione di telefoni delle aree comuni)</p>
<p>Per assegnare più tipi di oggetto nello stesso comando, separare i tipi di oggetto utilizzando le virgole: -ObjectType &quot;user&quot;,&quot;computer&quot;,&quot;contact&quot;. È tuttavia possibile specificare solo un massimo di tre tripi di oggetto per ogni comando.</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome distinto dell'unità organizzativa in cui è necessario concedere i diritti. Ad esempio: -OU &quot;ou=Redmond,dc=litwareinc,dc=com&quot;. Si noti che è possibile concedere i diritti solo a un'unica unità organizzativa per comando.</p></td>
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
<td><p>Nome del dominio in cui si trova l'unità organizzativa. Se questo parametro non viene incluso, il cmdlet <strong>Grant-CsOUPermission</strong> cercherà l'unità organizzativa nel dominio corrente.</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente agli amministratori di specificare il nome di dominio completo del controller di dominio da utilizzare quando si esegue il cmdlet <strong>Grant-CsOUPermission</strong>. Se questo parametro non viene specificato, il cmdlet utilizzerà il primo controller di dominio disponibile.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>FQDN del server di catalogo globale nel dominio. Questo parametro non è obbligatorio se si esegue il cmdlet <strong>Grant-CsOUPermission</strong> in un computer con un account nel dominio.</p></td>
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

Nessuno. Il cmdlet **Grant-CsOUPermission** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Grant-CsOUPermission** non restituisce oggetti o valori.

## Vedere anche

#### Ulteriori risorse

[Revoke-CsOUPermission](revoke-csoupermission.md)  
[Test-CsOUPermission](test-csoupermission.md)

