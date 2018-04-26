---
title: Remove-CsUserServicesPolicy
TOCTitle: Remove-CsUserServicesPolicy
ms:assetid: 025f9a94-ff44-4e06-8b14-721f8fd9924f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204629(v=OCS.15)
ms:contentKeyID: 49299500
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsUserServicesPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Elimina un criterio servizi utente esistente. I criteri servizi utente determinano se i contatti di un utente vengono o meno archiviati in Lync Server 2013 o nell'archivio contatti unificato. Quest'ultimo consente agli utenti di gestire un unico insieme di contatti accessibili tramite Lync 2013, Microsoft Outlook e/o Microsoft Outlook Web Access. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Remove-CsUserServicesPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 elimina il criterio servizi utente per utente RedmondUserServicesPolicy.

    Remove-CsUserServicesPolicy -Identity "RedmondUserServicesPolicy"

## Esempio 2

Nell'esempio 2 vengono eliminati tutti i criteri servizi utente configurati nell'ambito sito. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsUserServicesPolicy** e il valore Filter per restituire una raccolta di tutti i criteri configurati nell'ambito sito. Questa operazione viene eseguita utilizzando il valore di filtro "site:\*". La raccolta risultante viene quindi inviata tramite pipe al cmdlet **Remove-CsUserServicesPolicy**, che elimina ogni criterio della raccolta.

    Get-CsUserServicesPolicy -Filter "site:*" | Remove-CsUserServicesPolicy

## Esempio 3

Nell'esempio 3 vengono eliminati tutti i criteri servizi utente che consentono di utilizzare l'archivio contatti unificato. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsUserServicesPolicy** senza parametri per restituire una raccolta di tutti i criteri servizi utente configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i criteri in cui la proprietà UcsAllowed è uguale a (-eq) True ($True). Questi criteri vengono quindi inviati tramite pipe al cmdlet **Remove-CsUserServicesPolicy**, che li rimuove.

    Get-CsUserServicesPolicy | Where-Object {$_.UcsAllowed -eq $True} | Remove-CsUserServicesPolicy

## Descrizione dettagliata

L'archivio contatti unificato, introdotto in Lync Server 2013, consente agli amministratori di archiviare i contatti di un utente in Microsoft Exchange Server 2013 anziché in Lync Server. In questo modo l'utente può accedere allo stesso insieme di contatti in Outlook e Outlook Web Access e in Lync 2013. In alternativa, è possibile continuare ad archiviare i contatti in Lync Server 2013. In tal caso gli utenti dovranno gestire due insiemi separati di contatti: uno da utilizzare con Outlook e Outlook Web Access e un altro da utilizzare con Lync 2013.

Per usufruire dell'archivio contatti unificato, è inoltre necessario assegnare all'utente un criterio servizi utente che consenta l'utilizzo dell'archivio contatti unificato. I criteri servizi utente, che possono essere configurati nell'ambito globale, del sito o per utente, includono solo una proprietà: UcsAllowed. Se questa proprietà è impostata su True e vengono soddisfatti tutti gli altri prerequisiti, al successivo accesso di un utente a Lync Server 2013 viene eseguita automaticamente la migrazione dei relativi contatti nell'archivio contatti unificato.

Se questa proprietà è impostata su False, la migrazione automatica non viene eseguita. La sola impostazione di UcsAllowed tuttavia non determina lo spostamento dei contatti di un utente dall'archivio contatti unificato a Lync Server. A tale scopo, è necessario innanzitutto assegnare all'utente un criterio servizi utente che non consenta l'utilizzo dell'archivio contatti unificato. Utilizzare quindi il cmdlet **Invoke-UcsRollback** per eseguire "manualmente" la migrazione dei contatti dall'archivio contatti unificato a Lync Server.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsUserServicesPolicy"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Remove-CsUserServicesPolicy** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco del criterio da eliminare. Per rimuovere un criterio configurato nell'ambito sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>Per rimuovere un criterio configurato nell'ambito del servizio, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;UserServer:atl-cs-001.litwareinc.com&quot;</p>
<p>Il servizio Server utenti è l'unico in grado di ospitare un criterio servizi utente.</p>
<p>I criteri possono essere rimossi anche nell'ambito per utente. Per rimuovere criteri per utente, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;RedmondUserServicesPolicy&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Rimuove il criterio servizi utente assegnato al tenant di Skype for Business online specificato. Quando si rimuove un criterio assegnato a un tenant, è inoltre necessario includere il parametro Identity con valore &quot;global&quot;:</p>
<p>-Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot; –Identity &quot;global&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Remove-CsUserServicesPolicy** accetta le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.UserServices.UserServicesPolicy inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsUserServicesPolicy** invece elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.UserServices.UserServicesPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsUserServicesPolicy](get-csuserservicespolicy.md)  
[Grant-CsUserServicesPolicy](grant-csuserservicespolicy.md)  
[New-CsUserServicesPolicy](new-csuserservicespolicy.md)  
[Set-CsUserServicesPolicy](set-csuserservicespolicy.md)

