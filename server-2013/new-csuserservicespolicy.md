---
title: New-CsUserServicesPolicy
TOCTitle: New-CsUserServicesPolicy
ms:assetid: 8d7b7f79-f72e-4057-a0d1-188a87af5023
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205072(v=OCS.15)
ms:contentKeyID: 49301272
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsUserServicesPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo criterio servizi utente. I criteri servizi utente determinano se i contatti di un utente vengono o meno archiviati in Lync Server 2013 o nell'archivio contatti unificato. L'archivio contatti unificato consente agli utenti di gestire un unico insieme di contatti accessibili tramite Lync 2013, Microsoft Outlook e/o Microsoft Outlook Web Access. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    New-CsUserServicesPolicy -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Tenant <Guid>] [-UcsAllowed <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 crea un nuovo criterio servizi utente per il sito Redmond. Per gli utenti gestiti da tale criterio i contatti non verranno spostati nell'archivio contatti unificato, in quanto il parametro UcsAllowed è stato impostato su False ($False).

    New-CsUserServicesPolicy -Identity "site:Redmond" -UcsAllowed $False

## Descrizione dettagliata

L'archivio contatti unificato, introdotto in Lync Server 2013, consente agli amministratori di archiviare i contatti di un utente in Microsoft Exchange Server 2013 anziché in Lync Server. In questo modo l'utente può accedere allo stesso insieme di contatti in Microsoft Outlook e Outlook Web Access e in Lync 2013. In alternativa, è possibile continuare ad archiviare i contatti in Lync Server 2013. In tal caso gli utenti dovranno gestire due insiemi separati di contatti: uno da utilizzare con Outlook e Outlook Web Access e un altro da utilizzare con Lync 2013.

Per usufruire dell'archivio contatti unificato, è inoltre necessario assegnare all'utente un criterio servizi utente che consenta l'utilizzo dell'archivio contatti unificato. I criteri servizi utente, che possono essere configurati nell'ambito globale, del sito o per utente, includono solo una proprietà: UcsAllowed. Se questa proprietà è impostata su True e vengono soddisfatti tutti gli altri prerequisiti, al successivo accesso di un utente a Lync Server 2013 viene eseguita automaticamente la migrazione dei relativi contatti nell'archivio contatti unificato.

Se questa proprietà è impostata su False, la migrazione automatica non viene eseguita. La sola impostazione di UcsAllowed tuttavia non determina lo spostamento dei contatti di un utente dall'archivio contatti unificato in Lync Server. Per ottenere questo risultato, è necessario innanzitutto assegnare all'utente un criterio servizi utente che non consenta l'utilizzo dell'archivio contatti unificato. Utilizzare quindi il cmdlet **Invoke-UcsRollback** per eseguire "manualmente" la migrazione dei contatti dall'archivio contatti unificato in Lync Server.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsUserServicesPolicy"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **New-CsUserServicesPolicy** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Identificatore univoco del criterio da creare. Per creare un criterio nell'ambito del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>Per creare un criterio nell'ambito del servizio, utilizzare una sintassi simile alla seguente: -Identity &quot;UserServer:atl-cs-001.litwareinc.com&quot;</p>
<p>Si noti che il servizio Server utenti è l'unico servizio che può ospitare un criterio servizi utente.</p>
<p>I criteri possono essere creati anche nell'ambito del singolo utente. Per creare un criterio per utente, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;RedmondUserServicesPolicy&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Impedisce la visualizzazione di eventuali messaggi di errore non irreversibili che potrebbero verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account del tenant di Skype for Business online per cui vengono creati i nuovi criteri servizi utente, ad esempio:</p>
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

Nessuno. Il cmdlet **New-CsUserServicesPolicy** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **New-CsUserServicesPolicy** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.UserServices.UserServicesPolicy.

## Vedere anche

#### Ulteriori risorse

[Get-CsUserServicesPolicy](get-csuserservicespolicy.md)  
[Grant-CsUserServicesPolicy](grant-csuserservicespolicy.md)  
[Remove-CsUserServicesPolicy](remove-csuserservicespolicy.md)  
[Set-CsUserServicesPolicy](set-csuserservicespolicy.md)

