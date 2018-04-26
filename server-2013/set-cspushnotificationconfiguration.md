---
title: Set-CsPushNotificationConfiguration
TOCTitle: Set-CsPushNotificationConfiguration
ms:assetid: 3aacdb2b-b6dd-4615-a3f9-68360f3ae483
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690013(v=OCS.15)
ms:contentKeyID: 49300242
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPushNotificationConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una raccolta esistente di impostazioni di configurazione delle notifiche Push. Il servizio notifica Push (servizio notifica Push Apple e servizio notifica Push Microsoft) consente di inviare notifiche su eventi quali nuovi messaggi istantanei o nuovi messaggi in segreteria telefonica a dispositivi mobili come iPhone e Windows Phone, anche se l'applicazione Lync in tali dispositivi è attualmente sospesa o eseguita in background. Questo cmdlet è stato introdotto nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011.

## Sintassi

    Set-CsPushNotificationConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsPushNotificationConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EnableApplePushNotificationService <$true | $false>] [-EnableMicrosoftPushNotificationService <$true | $false>] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando illustrato nell'esempio 1 consente di disabilitare le notifiche Push del servizio notifica Push Apple per il sito Redmond.

    Set-CsPushNotificationConfiguration -Identity "site:Redmond" -EnableApplePushNotificationService $False

## ESEMPIO 2

Nell'esempio 2 vengono disabilitate le notifiche push del servizio notifica Push Apple per tutti i siti che attualmente ospitano impostazioni di notifica Push. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsPushNotificationConfiguration** e il parametro Filter per restituire tutte le impostazioni di notifica Push configurate nell'ambito del sito. Il valore di filtro "site:\*" restituisce solo le impostazioni con il parametro Identity che inizia con il valore stringa "site:". La raccolta di impostazioni viene quindi inviata tramite pipe al cmdlet **Set-CsPushNotificationConfiguration**, che seleziona ogni elemento della raccolta e imposta la proprietà EnableApplePushNotificationService su False.

    Get-CsPushNotificationConfiguration -Filter "site:*" | Set-CsPushNotificationService -EnableApplePushNotificationService $False

## ESEMPIO 3

Nell'esempio 3 viene illustrato come individuare tutte le impostazioni di notifica Push in cui le notifiche push del servizio notifica Push Microsoft sono disabilitate e quindi disabilitare anche le notifiche Push del servizio notifica Push Apple per ognuna di tali impostazioni. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsPushNotificationConfiguration** per restituire una raccolta di tutte le impostazioni di notifica Push attualmente in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà EnableMicrosoftPushNotificationService è uguale a (-eq) False. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsPushNotificationConfiguration**, che seleziona ogni elemento di tale raccolta e imposta la proprietà EnableApplePushNotificationService su False.

    Get-CsPushNotificationConfiguration | Where-Object {$_.EnableMicrosoftPushNotificationService -eq $False} | Set-CsPushNotificationConfiguration -EnableApplePushNotificationService $False

## Descrizione dettagliata

Il servizio notifica Push Apple e il servizio notifica Push Microsoft consentono agli utenti con telefoni Apple iPhone o Windows Phone in cui è in esecuzione Lync di ricevere notifiche relative agli eventi di Lync quando Lync è sospeso o in esecuzione in background. Gli utenti possono ad esempio ricevere notifiche per eventi come i seguenti:

\- Inviti a una nuova sessione di messaggistica istantanea o conferenza

\- Nuovi messaggi istantanei

\- Nuovi messaggi in segreteria telefonica

Senza il servizio notifica Push, gli utenti riceverebbero queste notifiche solo quando Lync è in esecuzione come applicazione attiva e non è in background.

Gli amministratori possono abilitare e disabilitare le notifiche Push per gli utenti con telefoni iPhone e/o Windows Phone. Per impostazione predefinita, le notifiche Push sono disabilitate sia per gli utenti con telefoni iPhone che Windows Phone. Gli amministratori possono quindi abilitare o disabilitare le notifiche Push nell'ambito globale utilizzando il cmdlet **Set-CsPushNotificationConfiguration**. Possono inoltre creare impostazioni di notifica Push personalizzate nell'ambito del sito utilizzando il cmdlet **New-CsPushNotificationConfiguration**. Tali impostazioni personalizzate possono inoltre essere modificate utilizzando il cmdlet **Set-CsPushNotificationConfiguration**.

Per le impostazioni di configurazione di notifica Push, gli amministratori devono gestire due soli valori di proprietà: EnableApplePushNotificationService, che determina se le notifiche Push vengono inviate agli utenti con telefoni iPhone, e EnableMicrosoftPushNotificationService, che determina se le notifiche Push vengono inviate agli utenti con telefoni Windows Phone. Si noti che queste proprietà non devono necessariamente essere impostate sullo stesso valore. È ad esempio possibile abilitare le notifiche Push per gli utenti con telefoni Windows Phone, impostando EnableMicrosoftPushNotificationService su True, e, nello stesso tempo, disabilitare le notifiche per gli utenti con telefoni iPhone, impostando EnableApplePushNotificationService su False.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsPushNotificationConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins.

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
<td><p>Richiede la conferma prima dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableApplePushNotificationService</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Quando questo parametro è impostato su True, gli utenti con telefoni iPhone ricevono notifiche Push dal servizio notifica Push Apple. Quando è impostato su False, gli utenti con telefoni iPhone non ricevono tali notifiche.</p>
<p>Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableMicrosoftPushNotificationService</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Quando questo parametro è impostato su True, gli utenti con telefoni Windows Phone ricevono notifiche push dal servizio notifica Push Microsoft. Quando è impostato su False, gli utenti con telefoni Windows Phone non ricevono tali notifiche.</p>
<p>Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Indica l'identità delle impostazioni di configurazione di notifica Push da modificare. Per fare riferimento alle impostazioni globali, utilizzare la sintassi seguente:</p>
<p>-Identity global</p>
<p>Per fare riferimento alle impostazioni del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity site:Redmond</p>
<p>Si noti che non è possibile utilizzare caratteri jolly quando si specifica un parametro Identity.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto configurazione Push</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di Skype for Business online per le impostazioni di notifica Push da modificare. Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Se si usa una sessione remota di Windows PowerShell e si è connessi solo a Skype for Business online non è necessario includere il parametro Tenant. L'ID del tenant verrà infatti compilato automaticamente in base alle informazioni di connessione. Il parametro Tenant è destinato principalmente all'uso in ambienti ibridi.</p></td>
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

Microsoft.Rtc.Management.WriteableConfig.Settings.PushNotificationConfiguration.PushNotificationConfiguration. Il cmdlet **Set-CsPushNotificationConfiguration** accetta istanze dell'oggetto PushNotificationConfiguration inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsPushNotificationConfiguration** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WriteableConfig.Settings.PushNotificationConfiguration.PushNotificationConfiguration.

