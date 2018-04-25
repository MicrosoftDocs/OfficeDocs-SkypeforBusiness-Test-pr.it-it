---
title: Remove-CsPushNotificationConfiguration
TOCTitle: Remove-CsPushNotificationConfiguration
ms:assetid: 77574e30-a75f-4aaa-b2d8-ccbabda31797
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690028(v=OCS.15)
ms:contentKeyID: 49301028
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPushNotificationConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Elimina una raccolta esistente di impostazioni di notifica Push. Il servizio notifica Push (servizio notifica Push Apple e servizio notifica Push Microsoft) consente di inviare notifiche su eventi quali nuovi messaggi istantanei o nuovi messaggi in segreteria telefonica a dispositivi mobili come iPhone e Windows Phone, anche se l'applicazione Lync in tali dispositivi è attualmente sospesa o eseguita in background. Questo cmdlet è stato introdotto nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011.

## Sintassi

    Remove-CsPushNotificationConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando illustrato nell'esempio 1 consente di eliminare la raccolta di impostazioni di notifica Push assegnate al sito Redmond.

    Remove-CsPushNotificationConfiguration -Identity "site:Redmond"

## ESEMPIO 2

Nell'esempio 2 vengono eliminate tutte le impostazioni di notifica Push configurate nell'ambito del sito. A tale scopo, vengono innanzitutto utilizzati il cmdlet **Get-CsPushNotificationConfiguration** e il parametro Filter per restituire una raccolta di tutte le impostazioni configurate nell'ambito del sito. Il valore di filtro "site:\*" limita gli elementi restituiti alle impostazioni con un'identità che inizia con il valore stringa "site:". Le impostazioni nell'ambito del sito vengono quindi inviate tramite pipe al cmdlet **Remove-CsPushNotificationConfiguration**, che le elimina.

    Get-CsPushNotificationConfiguration -Filter "site:*" | Remove-CsPushNotificationConfiguration

## ESEMPIO 3

Nell'esempio 3 viene illustrato come rimuovere tutte le impostazioni di configurazione della notifica Push in cui sono state disabilitate le notifiche del servizio notifica Push Microsoft. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsPushNotificationConfiguration** per restituire una raccolta di tutte le impostazioni di notifica Push attualmente in uso. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà EnableMicrosoftPushNotificationService è uguale a (-eq) False. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsPushNotificationConfiguration**, che a sua volta elimina ogni elemento della raccolta.

    Get-CsPushNotificationConfiguration | Where-Object {$_.EnableMicrosoftPushNotificationService -eq $False} | Remove-CsPushNotificationConfiguration

## Descrizione dettagliata

Il servizio notifica Push Apple e il servizio notifica Push Microsoft consentono agli utenti con telefoni Apple iPhone o Windows Phone in cui è in esecuzione Lync di ricevere notifiche relative agli eventi di Lync anche quando Lync è sospeso o in esecuzione in background. Gli utenti possono ad esempio ricevere notifiche per eventi come i seguenti:

\- Inviti a una nuova sessione di messaggistica istantanea o conferenza

\- Nuovi messaggi istantanei

\- Nuovi messaggi in segreteria telefonica

Senza il servizio notifica Push, gli utenti riceverebbero queste notifiche solo quando Lync è in esecuzione come applicazione attiva e non è in background.

Gli amministratori possono abilitare e disabilitare le notifiche Push per gli utenti con telefoni iPhone e/o Windows Phone. Per impostazione predefinita, le notifiche Push sono disabilitate sia per gli utenti con telefoni iPhone che Windows Phone. Gli amministratori possono quindi abilitare o disabilitare le notifiche Push nell'ambito globale utilizzando il cmdlet **Set-CsPushNotificationConfiguration**. Possono inoltre creare impostazioni di notifica Push personalizzate nell'ambito del sito utilizzando il cmdlet **New-CsPushNotificationConfiguration**.

Tali impostazioni personalizzate possono successivamente essere eliminate utilizzando il cmdlet **Remove-CsPushNotificationConfiguration**. Se si eliminano le impostazioni configurate nell'ambito del sito, gli utenti di tale sito verranno automaticamente gestiti dalle impostazioni di notifica Push globali.

Si noti che è anche possibile eseguire il cmdlet **Remove-CsPushNotificationConfiguration** per le impostazioni globali. In tal caso, le impostazioni globali non verranno però rimosse, ma verranno ripristinati i valori predefiniti delle relative proprietà. In questo caso le notifiche Push verranno disabilitate sia per il servizio notifica Push Apple che per il servizio notifica Push Microsoft.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsPushNotificationConfiguration** i membri dei gruppi seguenti: RTCUniversalServerAdmins.

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
<td><p>Identificatore univoco della raccolta di impostazioni di configurazione di notifica Push. Per rimuovere la raccolta globale, utilizzare la sintassi seguente:</p>
<p>-Identity global</p>
<p>Si noti che non è possibile rimuovere realmente le impostazioni globali, ma solo ripristinare i valori predefiniti delle proprietà.</p>
<p>Per rimuovere la raccolta di un sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity site:Redmond</p>
<p>Non è possibile utilizzare caratteri jolly quando si specifica l'identità di un criterio.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di visualizzare una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non irreversibile che potrebbe verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account del tenant di Skype for Business online per le impostazioni di configurazione della notifica Push da eliminare, ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

Microsoft.Rtc.Management.WriteableConfig.Settings.PushNotificationConfiguration.PushNotificationConfiguration. Il cmdlet **Remove-CsPushNotificationConfiguration** accetta istanze dell'oggetto PushNotificationConfiguration inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsPushNotificationConfiguration** invece elimina le istanze dell'oggetto Microsoft.Rtc.Management.WriteableConfig.Settings.PushNotificationConfiguration.PushNotificationConfiguration.

