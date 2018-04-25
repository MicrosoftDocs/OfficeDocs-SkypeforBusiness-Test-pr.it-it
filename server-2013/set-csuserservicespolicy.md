---
title: Set-CsUserServicesPolicy
TOCTitle: Set-CsUserServicesPolicy
ms:assetid: fbe18ddf-5094-4d8b-ad27-75b73173b8c4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205414(v=OCS.15)
ms:contentKeyID: 49302559
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUserServicesPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un criterio servizi utente esistente. I criteri servizi utente determinano se i contatti di un utente vengono o meno archiviati in Lync Server 2013 o nell'archivio contatti unificato. L'archivio contatti unificato consente agli utenti di gestire un unico insieme di contatti accessibili tramite Lync 2013, Outlook e/o Outlook Web Access. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsUserServicesPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsUserServicesPolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-UcsAllowed <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 disabilita l'uso dell'archivio contatti unificato per i criteri Servizi utente RedmondUserServicesPolicy per utente. Ciò significa che i contatti degli utenti gestiti con questi criteri non vengono archiviati nell'archivio contatti unificato.

    Set-CsUserServicesPolicy -Identity "RedmondUserServicesPolicy" -UcsAllowed $False

## Esempio 2

Nell'esempio 2 tutti i criteri Servizi utente configurati nell'ambito del sito vengono modificati per disabilitare l'uso dell'archivio contatti unificato. A tale scopo, nel comando vengono innanzitutto chiamati il cmdlet **Get-CsUserServicesPolicy** e il parametro Filter per restituire una raccolta di tutti i criteri configurati nell'ambito del sito. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsUserServicesPolicy**, che raccoglie tutti i criteri nella raccolta e imposta la proprietà UcsAllowed su ($False).

    Get-CsUserServicesPolicy -Filter "site:*" | Set-CsUserServicesPolicy -UcsAllowed $False

## Descrizione dettagliata

L'archivio contatti unificato, introdotto in Lync Server 2013, consente agli amministratori di archiviare i contatti di un utente in Microsoft Exchange Server 2013 anziché in Lync Server. In questo modo l'utente può accedere allo stesso insieme di contatti in Outlook e Outlook Web Access e in Lync 2013. In alternativa, è possibile continuare ad archiviare i contatti in Lync Server 2013. In tal caso gli utenti dovranno gestire due insiemi separati di contatti: uno da utilizzare con Outlook e Outlook Web Access e un altro da utilizzare con Lync 2013.

Per usufruire dell'archivio contatti unificato, è inoltre necessario assegnare all'utente un criterio servizi utente che consenta l'utilizzo dell'archivio contatti unificato. I criteri servizi utente, che possono essere configurati nell'ambito globale, del sito o per utente, includono solo una proprietà: UcsAllowed. Se questa proprietà è impostata su True e vengono soddisfatti tutti gli altri prerequisiti, al successivo accesso di un utente a Lync Server 2013 viene eseguita automaticamente la migrazione dei relativi contatti nell'archivio contatti unificato.

Se questa proprietà è impostata su False, la migrazione automatica non viene eseguita. La sola impostazione di UcsAllowed tuttavia non determina lo spostamento dei contatti di un utente dall'archivio contatti unificato in Lync Server. Per ottenere questo risultato, è necessario innanzitutto assegnare all'utente un criterio servizi utente che non consenta l'utilizzo dell'archivio contatti unificato. Utilizzare quindi il cmdlet **Invoke-CsUcsRollback** per eseguire "manualmente" la migrazione dei contatti dall'archivio contatti unificato in Lync Server.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsUserServicesPolicy"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Set-CsUserServicesPolicy** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima dell'esecuzione del comando. Impedisce la visualizzazione di eventuali messaggi di errore non irreversibili che potrebbero verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Impedisce la visualizzazione di eventuali messaggi di errore non irreversibili che potrebbero verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per i criteri da modificare. Per modificare i criteri globali, utilizzare la sintassi seguente:</p>
<p>-Identity &quot;global&quot;</p>
<p>Per modificare criteri configurati con ambito di sito, utilizzare una sintassi analoga alla seguente:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>Per modificare criteri configurati con ambito di servizio, utilizzare una sintassi analoga alla seguente:</p>
<p>-Identity &quot;UserServer:atl-cs-001.litwareinc.com&quot;</p>
<p>Notare che il servizio UserServer è l'unico servizio che può ospitare criteri di servizi utente.</p>
<p>Se questo parametro non è incluso, il cmdlet <strong>Set-CsUserServicesPolicy</strong> modificherà automaticamente i criteri globali.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant Skype for Business online di cui è necessario modificare i criteri dei servizi utente. Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="even">
<td><p><em>UcsAllowed</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Quando è impostato su True (valore predefinito) viene automaticamente eseguita la migrazione degli utenti interessati dai criteri nell'archivio contatti unificato (presupponendo che tali utenti abbiano un account in Microsoft Exchange Server 2013 e che accedano utilizzando Lync 2013). Quando è impostato su False, è possibile rimuovere gli utenti dall'archivio contatti unificato, ma solo se vengono rimossi &quot;manualmente&quot; dal cmdlet <strong>Invoke-CsUcsRollback</strong>.</p></td>
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

Il cmdlet **Set-CsUserServicesPolicy** accetta istanze da pipeline dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.UserServices.UserServicesPolicy.

## Tipi restituiti

Nessuno. Viceversa, il cmdlet **Set-CsUserServicesPolicy** modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.UserServices.UserServicesPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsUserServicesPolicy](get-csuserservicespolicy.md)  
[Grant-CsUserServicesPolicy](grant-csuserservicespolicy.md)  
[New-CsUserServicesPolicy](new-csuserservicespolicy.md)  
[Remove-CsUserServicesPolicy](remove-csuserservicespolicy.md)

