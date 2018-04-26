---
title: New-CsPushNotificationConfiguration
TOCTitle: New-CsPushNotificationConfiguration
ms:assetid: 8bf61c72-7902-4075-9388-47a7dd4e649c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690027(v=OCS.15)
ms:contentKeyID: 49301264
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPushNotificationConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta di impostazioni di configurazione delle notifiche Push nell'ambito del sito. Il servizio notifica Push (servizio notifica Push Apple e servizio notifica Push Microsoft) consente di inviare notifiche su eventi quali nuovi messaggi istantanei o nuovi messaggi in segreteria telefonica a dispositivi mobili come iPhone e Windows Phone, anche se l'applicazione Lync in tali dispositivi è attualmente sospesa o eseguita in background. Questo cmdlet è stato introdotto nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011.

## Sintassi

    New-CsPushNotificationConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-EnableApplePushNotificationService <$true | $false>] [-EnableMicrosoftPushNotificationService <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 crea una nuova raccolta di impostazioni di notifica Push per il sito Redmond e abilita le notifiche push sia per il servizio notifica Push Apple che per il servizio notifica Push Microsoft. Quest'ultima operazione viene eseguita impostando entrambe le proprietà EnableApplePushNotificationService e EnableMicrosoftPushNotificationService su True.

    New-CsPushNotificationConfiguration -Identity "site:Redmond" -EnableApplePushNotificationService $True -EnableMicrosoftPushNotificationService -$True

## ESEMPIO 2

Nell'esempio 2 viene illustrato come creare un insieme di impostazioni di configurazione di notifica Push per ognuno dei siti di Lync Server. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsSite** per restituire una raccolta di tutti i siti di Lync Server. La raccolta viene quindi inviata tramite pipe al cmdlet **ForEach-Object**, che seleziona ogni sito della raccolta, chiama il cmdlet **New-CsPushNotificationConfiguration** e crea un nuovo insieme di impostazioni di configurazione di notifica Push per il sito. Si noti che questo comando avrà esito negativo per qualsiasi sito che ospita già una raccolta di impostazioni di configurazione di notifica Push.

    Get-CsSite | ForEach-Object {New-CsPushConfigurationNotification -Identity $_.Identity}

## ESEMPIO 3

Nell'esempio 3 viene illustrato l'utilizzo del parametro InMemory per creare una raccolta di impostazioni di configurazione della notifica Push inizialmente presenti solo in memoria. A tale scopo, nell'esempio viene creata una nuova raccolta di impostazioni (con identità site:Redmond) che viene archiviata in una variabile denominata $x. Si noti che, dopo l'esecuzione del primo comando, la raccolta è presente solo in memoria. Se si esegue il cmdlet **Get-CsPushNotificationConfiguration**, non sarà possibile visualizzare alcuna voce per site:Redmond.

Nei due comandi successivi entrambe le proprietà EnableApplePushNotificationService ed EnableMicrosoftPushNotificationService per tale raccolta virtuale di impostazioni vengono impostate su True per abilitare le notifiche Push sia del servizio notifica Push Apple che del servizio notifica Push Microsoft. Nell'ultimo comando viene infine utilizzato il cmdlet **Set-CsPushNotificationConfiguration** per trasformare le impostazioni di notifica Push virtuali in una raccolta effettiva di impostazioni applicate al sito Redmond. Se non si chiama il cmdlet **Set-CsPushNotificationConfiguration**, le impostazioni rimangono solo in memoria e vengono eliminate al termine della sessione di Windows PowerShell o quando viene eliminata la variabile $x.

    $x = New-CsPushNotificationConfiguration -Identity "site:Redmond" -InMemory
    $x.EnableApplePushNotificationService = $True 
    $x.EnableMicrosoftPushNotificationService = $True
    Set-CsPushNotificationConfiguration -Instance $x

## Descrizione dettagliata

Il servizio notifica Push Apple e il servizio notifica Push Microsoft consentono agli utenti con telefoni Apple iPhone o Windows Phone in cui è in esecuzione Lync di ricevere notifiche relative agli eventi di Lync, anche quando Lync è sospeso o in esecuzione in background. Gli utenti possono ad esempio ricevere notifiche per eventi come i seguenti:

\- Inviti a una nuova sessione di messaggistica istantanea o conferenza

\- Nuovi messaggi istantanei

\- Nuovi messaggi in segreteria telefonica

Senza il servizio notifica Push, gli utenti riceverebbero queste notifiche solo quando Lync è in esecuzione come applicazione attiva e non è in background.

Gli amministratori possono abilitare e disabilitare le notifiche Push per gli utenti con telefoni iPhone e/o Windows Phone. Per impostazione predefinita, le notifiche Push sono disabilitate sia per gli utenti con telefoni iPhone che Windows Phone. Gli amministratori possono quindi abilitare o disabilitare le notifiche Push nell'ambito globale utilizzando il cmdlet **Set-CsPushNotificationConfiguration**. Possono inoltre creare impostazioni di notifica Push personalizzate nell'ambito del sito utilizzando il cmdlet **New-CsPushNotificationConfiguration**. In questo modo, gli amministratori possono fornire notifiche Push agli utenti in alcuni siti (ad esempio Redmond) limitando nel contempo l'utilizzo di tali notifiche in altri siti.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsPushNotificationConfiguration** i membri dei gruppi seguenti: RTCUniversalServerAdmins.

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
<td><p>Le impostazioni di notifica Push possono essere create solo nell'ambito del sito. Per specificare una nuova raccolta di impostazioni per un sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>Si noti che questo comando avrà esito negativo se il sito Redmond ospita già una raccolta di impostazioni di notifica Push.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di visualizzare una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableApplePushNotificationService</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Quando questo parametro è impostato su True, gli utenti con telefoni iPhone ricevono notifiche Push dal servizio notifica Push Apple. Quando è impostato su False, gli utenti con telefoni iPhone non ricevono tali notifiche.</p>
<p>Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableMicrosoftPushNotificationService</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Quando questo parametro è impostato su True, gli utenti con telefoni Windows Phone ricevono notifiche push dal servizio notifica Push Microsoft. Quando è impostato su False, gli utenti con telefoni Windows Phone non ricevono tali notifiche.</p>
<p>Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non irreversibile che potrebbe verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output di un comando chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account del tenant di Skype for Business online per cui vengono create nuove impostazioni di configurazione delle notifiche Push, ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID tenant per ciascun tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

Nessuno. Il cmdlet **New-CsPushNotificationConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **New-CsPushNotificationConfiguration** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WriteableConfig.Settings.PushNotificationConfiguration.PushNotificationConfiguration.

