---
title: Get-CsMeetingConfiguration
TOCTitle: Get-CsMeetingConfiguration
ms:assetid: 3aa2d905-0ce0-4675-8543-c7bb9b4a3d1a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425875(v=OCS.15)
ms:contentKeyID: 49300241
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsMeetingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il cmdlet **Get-CsMeetingConfiguration** consente di restituire informazioni sulle impostazioni di configurazione delle riunioni attualmente in uso nell'organizzazione. Tali impostazioni consentono di stabilire il tipo di riunioni (denominate anche "conferenze") che possono essere create dagli utenti e di definire come (o anche se) possono partecipare a tali riunioni utenti anonimi e utenti che utilizzano conferenze telefoniche con accesso esterno. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsMeetingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsMeetingConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Tenant <Guid>]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 restituisce una raccolta di tutte le impostazioni di configurazione delle riunioni attualmente in uso nella propria organizzazione.

    Get-CsMeetingConfiguration

## ESEMPIO 2

Nell'Esempio 2, viene restituita solo una raccolta di impostazioni di configurazione delle riunioni: le impostazioni con Identity site:Redmond.

    Get-CsMeetingConfiguration -Identity site:Redmond

## ESEMPIO 3

Nell'esempio 3 vengono restituite tutte le impostazioni di configurazione delle riunioni configurate nell'ambito del servizio. Per ottenere questo risultato, viene incluso il parametro Filter con valore "service:\*" che restituisce solo i dati relativi alle impostazioni la cui proprietà Identity inizia con i caratteri "service:".

    Get-CsMeetingConfiguration -Filter "service:*"

## ESEMPIO 4

Nell'esempio 4 vengono restituite informazioni su tutte le impostazioni di configurazione delle riunioni a cui gli utenti anonimi sono autorizzati ad accedere per impostazione predefinita. A tale scopo, il comando innanzitutto utilizza il cmdlet **Get-CsMeetingConfiguration** senza alcun parametro per restituire una raccolta di tutte le impostazioni di configurazione delle riunioni attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà AdmitAnonymousByDefault è uguale a True.

    Get-CsMeetingConfiguration | Where-Object {$_.AdmitAnonymousUsersByDefault -eq $True}

## Descrizione dettagliata

Le riunioni (denominate anche "conferenze") sono parte integrante di Lync Server. I cmdlet **CsMeetingConfiguration** consentono agli amministratori di controllare il tipo di riunioni che possono essere create dagli utenti e di stabilire la modalità di partecipazione alle riunioni da parte di utenti anonimi e utenti che utilizzano conferenze telefoniche con accesso esterno. È ad esempio possibile configurare le riunioni in modo che chiunque acceda tramite PSTN (Public Switched Telephone Network) venga automaticamente ammesso alla riunione. In alternativa, è possibile configurare le riunioni in modo che gli utenti che utilizzano conferenze telefoniche con accesso esterno non siano automaticamente ammessi alla riunione, ma vengano instradati alla sala di attesa. Questi utenti restano in attesa finché un relatore non concede loro l'accesso alla riunione.

Il cmdlet **Get-CsMeetingConfiguration** consente di restituire informazioni sulle raccolte di impostazioni di configurazione delle riunioni attualmente in uso nell'organizzazione.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsMeetingConfiguration** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsMeetingConfiguration"}

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
<td><p>Consente di utilizzare i caratteri jolly per ottenere una o più raccolte di impostazioni di configurazione delle riunioni. Ad esempio, per ottenere una raccolta di tutte le impostazioni configurate nell'ambito del sito, utilizzare la seguente sintassi: -Filter site:*. Per ottenere una raccolta di tutte le impostazioni che hanno il termine &quot;EMEA&quot; nella loro identità (Identity, l'unica proprietà che è possibile filtrare), utilizzare la seguente sintassi: -Filter *EMEA*.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Indica l'identificatore univoco della raccolta di impostazioni di configurazione delle riunioni che si desidera ottenere. Per ottenere le impostazioni globali, utilizzare la seguente sintassi: -Identity global. Per fare riferimento a una raccolta configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Per ottenere le impostazioni configurate nell'ambito del servizio, utilizzare una sintassi simile alla seguente: -Identity service:UserServer:atl-cs-001.litwareinc.com.</p>
<p>Se questo parametro non viene specificato, il cmdlet <strong>Get-CsMeetingConfiguration</strong> restituirà una raccolta di tutte le impostazioni delle riunioni in uso nell'organizzazione.</p>
<p>Si noti che non è possibile utilizzare caratteri jolly quando si specifica un parametro Identity. Se tuttavia è necessario utilizzare caratteri jolly, includere il parametro Filter.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati di configurazione della riunione dalla replica locale di archivio di gestione centrale invece che direttamente da archivio di gestione centrale.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di Office 365 di cui devono essere recuperate le impostazioni di configurazione delle riunioni.</p>
<p>Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Se si usa una sessione remota di Windows PowerShell e si è connessi solo a Skype for Business online non è necessario includere il parametro Tenant. L'ID del tenant verrà infatti compilato automaticamente in base alle informazioni di connessione. Il parametro Tenant è destinato principalmente all'uso in ambienti ibridi.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsMeetingConfiguration** non accetta dati inviati tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsMeetingConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.MeetingConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsMeetingConfiguration](new-csmeetingconfiguration.md)  
[Remove-CsMeetingConfiguration](remove-csmeetingconfiguration.md)  
[Set-CsMeetingConfiguration](set-csmeetingconfiguration.md)

