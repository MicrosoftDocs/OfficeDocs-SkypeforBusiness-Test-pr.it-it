---
title: Set-CsMeetingConfiguration
TOCTitle: Set-CsMeetingConfiguration
ms:assetid: 80c3529e-d009-48c5-835a-3740f02b6dd4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398648(v=OCS.15)
ms:contentKeyID: 49301144
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsMeetingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

**Set-CsMeetingConfiguration** consente di modificare le impostazioni di configurazione delle riunioni attualmente in uso nell'organizzazione. Tali impostazioni consentono di stabilire il tipo di riunioni (note anche come "conferenze") che gli utenti possono creare, nonché di controllare come (o persino se) utenti anonimi e utenti di conferenze telefoniche con accesso esterno possono partecipare a tali riunioni. Si noti che queste impostazioni hanno effetto solo sulle riunioni pianificate e non sulle riunioni ad hoc create facendo clic sull'opzione Riunione immediata in Lync. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsMeetingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsMeetingConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AdmitAnonymousUsersByDefault <$true | $false>] [-AssignedConferenceTypeByDefault <$true | $false>] [-Confirm [<SwitchParameter>]] [-CustomFooterText <String>] [-DesignateAsPresenter <None | Company | Everyone>] [-EnableAssignedConferenceType <$true | $false>] [-Force <SwitchParameter>] [-HelpURL <String>] [-LegalURL <String>] [-LogoURL <String>] [-PstnCallersBypassLobby <$true | $false>] [-RequireRoomSystemsAuthorization <$true | $false>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 vengono modificate le di impostazioni di configurazione delle riunioni assegnate al sito Redmond (Identity site:Redmond). In questo caso, il valore della proprietà DesignateAsPresenter è impostato su Everyone.

    Set-CsMeetingConfiguration -Identity site:Redmond -DesignateAsPresenter Everyone

## ESEMPIO 2

Il comando mostrato nell'esempio 2 è una variante del comando mostrato nell'esempio 1. Questa volta tuttavia il valore della proprietà DesignateAsPresenter viene modificato per tutte le impostazioni di configurazione delle riunioni in uso nell'organizzazione. A tale scopo, viene chiamato il cmdlet **Get-CsMeetingConfiguration** senza alcun parametro per restituire una raccolta di tutte le impostazioni di configurazione delle riunioni attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsMeetingConfiguration**, che modifica la proprietà DesignateAsPresenter per tutti gli elementi nella raccolta.

    Get-CsMeetingConfiguration | Set-CsMeetingConfiguration -DesignateAsPresenter Everyone

## ESEMPIO 3

Con l'esempio 3 vengono modificate tutte le impostazioni di configurazione delle riunioni che non consentono l'ammissione predefinita degli utenti anonimi. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsMeetingConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione delle riunioni attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà AdmitAnonymousUsersByDefault è uguale a False. A sua volta, la raccolta filtrata viene inviata tramite pipe al cmdlet **Set-CsMeetingConfiguration**, che imposta la proprietà PstnCallersBypassLobby su True per ogni elemento nella raccolta.

    Get-CsMeetingConfiguration | Where-Object {$_.AdmitAnonymousUsersByDefault -eq $False} | Set-CsMeetingConfiguration -PstnCallersBypassLobby $True

## Descrizione dettagliata

Le riunioni, o conferenze, sono parte integrante di Lync Server. I cmdlet CsMeetingConfiguration consentono agli amministratori di controllare il tipo di riunioni che gli utenti possono creare e di determinare come le riunioni devono gestire gli utenti anonimi e gli utenti di conferenze telefoniche con accesso esterno. Ad esempio, è possibile configurare le riunioni in modo che chiunque acceda esternamente attraverso la rete PSTN (Public Switched Telephone Network) venga automaticamente ammesso alla riunione. In alternativa, è possibile configurare le riunioni in modo che gli utenti con accesso esterno non vengano automaticamente ammessi alla riunione, ma vengano invece indirizzati alla relativa sala di attesa. Questi utenti con accesso esterno rimangono in attesa in tale sala finché un relatore non li ammette alla riunione.

Come specificato in precedenza, queste impostazioni hanno effetto solo sulle riunioni pianificate e non sulle riunioni ad hoc create facendo clic sull'opzione Riunione immediata in Microsoft Lync. Quando si crea una riunione facendo clic su Riunione immediata, l'accesso come partecipante viene automaticamente consentito a tutti e gli utenti anonimi possono partecipare alla riunione senza dover attendere nella sala di attesa. Questo si verifica indipendentemente dalla configurazione delle impostazioni della riunione tramite i cmdlet CsMeetingConfiguration.

Il cmdlet **Set-CsMeetingConfiguration** consente di modificare qualsiasi impostazione di configurazione delle riunioni attualmente in uso nell'organizzazione.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsMeetingConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsMeetingConfiguration"}

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
<td><p><em>AdmitAnonymousUsersByDefault</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Consente di determinare se, per impostazione predefinita, le riunioni consentono la partecipazione degli utenti anonimi (vale a dire degli utenti non autenticati). Impostare questo valore su True se si desidera che, per impostazione predefinita, le nuove riunioni consentano la partecipazione degli utenti anonimi. Impostare questo valore su False se si preferisce che, per impostazione predefinita, le nuove riunioni non consentano la partecipazione degli utenti anonimi. Il valore predefinito è True.</p></td>
</tr>
<tr class="even">
<td><p><em>AssignedConferenceTypeByDefault</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Consente di determinare se le nuove riunioni saranno configurate, per impostazione predefinita, come riunioni pubbliche. Impostare questo valore su True per utilizzare le riunioni pubbliche come impostazione predefinita; impostare questo valore su False per utilizzare le riunioni private come impostazione predefinita. Il valore predefinito è True.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>CustomFooterText</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Testo da utilizzare negli inviti alle riunioni personalizzati.</p></td>
</tr>
<tr class="odd">
<td><p><em>DesignateAsPresenter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.DesignateAsPresenter</p></td>
<td><p>Indica quali utenti (oltre all'organizzatore della riunione) possono essere automaticamente designati come presentatori quando accedono a una riunione. Le scelte valide sono None, Company ed Everyone. Per impostazione predefinita, DesignateAsPresenter è impostato su Company, pertanto tutti i membri dell'organizzazione otterranno i diritti di presentatore nel momento in cui accedono a una riunione.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableAssignedConferenceType</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se gli utenti possono pianificare riunioni pubbliche. Nel caso di una riunione pubblica, l'ID della conferenza e il collegamento alla riunione rimangono gli stessi ogni volta che si tiene una riunione. Nel caso di una riunione privata, l'ID della conferenza e il collegamento alla riunione cambiano da una riunione all'altra. Il valore predefinito è True.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>HelpURL</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL di un sito Web in cui gli utenti possono ottenere assistenza per partecipare alla riunione.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Indica l'identificatore univoco per la raccolta di impostazioni di configurazione delle riunioni da modificare. Per fare riferimento alle impostazioni globali, utilizzare la sintassi seguente: -Identity global. Per far riferimento a una raccolta configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity &quot;site:Redmond&quot;. Le impostazioni configurate nell'ambito del servizio possono essere referenziate con una sintassi simile alla seguente: -Identity &quot;service:UserServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>Se questo parametro non viene specificato, il cmdlet <strong>Set-CsMeetingConfiguration</strong> modifica le impostazioni globali.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto MeetingConfiguration</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>LegalURL</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL di un sito Web contenente informazioni legati e dichiarazioni di non responsabilità per le riunioni.</p></td>
</tr>
<tr class="even">
<td><p><em>LogoURL</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL dell'immagine da utilizzare negli inviti alle riunioni personalizzati.</p></td>
</tr>
<tr class="odd">
<td><p><em>PstnCallersBypassLobby</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se gli utenti che accedono esternamente attraverso una linea telefonica PSTN (Public Switched Telephone Network) devono essere automaticamente ammessi a una riunione. Se l'impostazione è True ($True), i chiamanti PSTN saranno automaticamente ammessi alla riunione. Se l'impostazione è False ($False), i chiamanti PSTN saranno inizialmente instradati alla sala di attesa conferenza. Dovranno quindi attendere che un presentatore della conferenza conceda loro l'accesso alla riunione. Il valore predefinito è True.</p></td>
</tr>
<tr class="even">
<td><p><em>RequireRoomSystemsAuthorization</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se questo parametro è impostato su True ($True), tutti gli utenti dovranno essere autenticati prima di poter partecipare a una riunione utilizzando il sistema delle sale di Lync. Il valore predefinito è False ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di Office 365 per cui modificare le impostazioni di configurazione delle riunioni.</p>
<p>Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Se si usa una sessione remota di Windows PowerShell e si è connessi solo a Skype for Business online, non è necessario includere il parametro Tenant. L'ID del tenant verrà infatti compilato automaticamente in base alle informazioni di connessione. Il parametro Tenant è destinato principalmente all'uso in distribuzioni ibride.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.MeetingConfiguration. Il cmdlet Set-CsMeetingConfiguration accetta istanze dell'oggetto configurazione riunioni inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CsMeetingConfiguration** non restituisce alcun oggetto o valore. Modifica invece le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.UserServices.MeetingConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsMeetingConfiguration](get-csmeetingconfiguration.md)  
[New-CsMeetingConfiguration](new-csmeetingconfiguration.md)  
[Remove-CsMeetingConfiguration](remove-csmeetingconfiguration.md)

