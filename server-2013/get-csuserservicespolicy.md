---
title: Get-CsUserServicesPolicy
TOCTitle: Get-CsUserServicesPolicy
ms:assetid: 424cd3ca-6df4-4715-97f1-95d2da3b6d90
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204838(v=OCS.15)
ms:contentKeyID: 49300340
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsUserServicesPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui criteri servizi utente configurati per l'utilizzo nell'organizzazione. I criteri di questo tipo determinano se i contatti di un utente vengono o meno archiviati in Lync Server 2013 o nell'archivio contatti unificato. Tale archivio consente agli utenti di gestire un unico insieme di contatti accessibili tramite Lync 2013, Outlook e/o Outlook Web Access. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsUserServicesPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsUserServicesPolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Tenant <Guid>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce informazioni su tutti i criteri servizi utente attualmente in uso nell'organizzazione.

    Get-CsUserServicesPolicy

## Esempio 2

Nell'esempio 2 vengono restituite informazioni su un singolo criterio servizi utente, ovvero il criterio configurato per il sito Redmond.

    Get-CsUserServicesPolicy -Identity "site:Redmond"

## Esempio 3

Nell'esempio 3 vengono restituite informazioni su tutti i criteri servizi utente configurati nell'ambito del sito. Per ottenere questo risultato, viene incluso il parametro Filter con valore "site:\*".

    Get-CsUserServicesPolicy -Filter "site:*"

## Esempio 4

Il comando riportato nell'esempio 4 restituisce informazioni sui criteri servizi utente in cui è stato disabilitato l'utilizzo dell'archivio contatti unificato. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsUserServicesPolicy** senza parametri per restituire una raccolta di tutti i criteri servizi utente configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i criteri in cui la proprietà UcsAllowed è stata impostata su False ($False).

    Get-CsUserServicesPolicy | Where-Object {$_.UcsAllowed -eq $False}

## Descrizione dettagliata

L'archivio contatti unificato, introdotto in Lync Server 2013, consente agli amministratori di archiviare i contatti di un utente in Microsoft Exchange Server 2013 anziché in Lync Server. In questo modo l'utente può accedere allo stesso insieme di contatti in Outlook e Outlook Web Access e in Lync 2013. In alternativa, è possibile continuare ad archiviare i contatti in Lync Server 2013. In tal caso, gli utenti dovranno gestire due insiemi separati di contatti: uno da utilizzare con Outlook e Outlook Web Access e un altro da utilizzare con Lync 2013.

Per usufruire dell'archivio contatti unificato, è inoltre necessario assegnare all'utente un criterio servizi utente che consenta l'utilizzo dell'archivio contatti unificato. I criteri servizi utente, che possono essere configurati nell'ambito globale, del sito o per utente, includono solo una proprietà: UcsAllowed. Se questa proprietà è impostata su True e vengono soddisfatti tutti gli altri prerequisiti, al successivo accesso di un utente a Lync Server 2013 viene eseguita automaticamente la migrazione dei relativi contatti nell'archivio contatti unificato.

Se questa proprietà è impostata su False, la migrazione automatica non viene eseguita. La sola impostazione di UcsAllowed tuttavia non determina lo spostamento dei contatti di un utente dall'archivio contatti unificato a Lync Server. A tale scopo, è necessario innanzitutto assegnare all'utente un criterio servizi utente che non consenta l'utilizzo dell'archivio contatti unificato. Utilizzare quindi il cmdlet **Invoke-UcsRollback** per eseguire "manualmente" la migrazione dei contatti dall'archivio contatti unificato a Lync Server.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsUserServicesPolicy"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsUserServicesPolicy** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare i caratteri jolly quando si specificano i criteri da recuperare. La sintassi seguente ad esempio restituisce tutti i criteri configurati nell'ambito del sito:</p>
<p>-Filter &quot;site:*&quot;</p>
<p>La sintassi seguente restituisce tutti i criteri configurati nell'ambito per utente:</p>
<p>-Filter &quot;tag:*&quot;</p>
<p>Non è possibile utilizzare i parametri Filter e Identity nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco del criterio da restituire. Per restituire il criterio globale, utilizzare la sintassi seguente:</p>
<p>-Identity global</p>
<p>Per restituire un criterio configurato nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity &quot;site:Redmond&quot;.</p>
<p>Per restituire un criterio configurato nell'ambito del servizio, utilizzare una sintassi simile alla seguente: -Identity &quot;UserServer:atl-cs-001.litwareinc.com&quot;</p>
<p></p>
<p>Si noti che il servizio UserServer è l'unico in grado di ospitare un criterio servizi utente.</p>
<p></p>
<p>I criteri possono essere configurati anche nell'ambito per utente. Per restituire uno di questi criteri, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;RedmondUserServicesPolicy&quot;</p>
<p>Se questo parametro non viene incluso, verranno restituiti tutti i criteri servizi utente configurati per l'utilizzo nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati del criterio servizi utente dalla replica locale dell'archivio di gestione centrale anziché direttamente dall'archivio di gestione centrale.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Se utilizzato, questo parametro recupera il criterio servizi utente per il tenant di Skype for Business online specificato. Ad esempio:</p>
<p>-Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>Non utilizzare i parametri Tenant e Identity nello stesso comando.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsUserServicesPolicy** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsUserServicesPolicy** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.UsersServices.UserServicesPolicy.

## Vedere anche

#### Ulteriori risorse

[Grant-CsUserServicesPolicy](grant-csuserservicespolicy.md)  
[New-CsUserServicesPolicy](new-csuserservicespolicy.md)  
[Remove-CsUserServicesPolicy](remove-csuserservicespolicy.md)  
[Set-CsUserServicesPolicy](set-csuserservicespolicy.md)

