---
title: Get-CsPushNotificationConfiguration
TOCTitle: Get-CsPushNotificationConfiguration
ms:assetid: ec2c17e5-ac4d-4d21-995a-642c5cf5c7bc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690049(v=OCS.15)
ms:contentKeyID: 49302359
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPushNotificationConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera informazioni sulle impostazioni di configurazione delle notifiche Push attualmente in uso nell'organizzazione. Il servizio notifica Push (servizio notifica Push Apple e servizio notifica Push Microsoft) consente di inviare notifiche su eventi quali nuovi messaggi istantanei o nuovi messaggi in segreteria telefonica a dispositivi mobili come iPhone e Windows Phone, anche se l'applicazione Lync in tali dispositivi è attualmente sospesa o eseguita in background. Questo cmdlet è stato introdotto nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011.

## Sintassi

    Get-CsPushNotificationConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsPushNotificationConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Tenant <Guid>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono restituite informazioni su tutte le impostazioni di notifica Push configurate per l'utilizzo nell'organizzazione.

    Get-CsPushNotificationConfiguration

## ESEMPIO 2

Il comando illustrato nell'esempio 2 restituisce informazioni su una singola raccolta di impostazioni di notifica Push, ovvero le impostazioni configurate per il sito Redmond.

    Get-CsPushNotificationConfiguration -Identity "site:Redmond"

## ESEMPIO 3

Nell'esempio 3 il comando restituisce tutte le impostazioni di notifica Push assegnate all'ambito del sito. A tale scopo, nel comando vengono utilizzati il parametro Filter e il valore di filtro "site:\*". Tale filtro consente di restituire solo le impostazioni con un valore di Identity che inizia con il valore stringa "site:".

    Get-CsPushNotificationConfiguration -Filter "site:*"

## ESEMPIO 4

Nell'esempio 4 vengono restituite tutte le impostazioni di notifica Push in cui le notifiche Push per telefoni iPhone sono state disabilitate. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsPushNotificationConfiguration** per restituire una raccolta di tutte le impostazioni di notifica Push attualmente in uso nell'organizzazione. La raccolta viene quindi inoltrata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà EnableApplePushNotificationService è uguale a (-eq) False.

    Get-CsPushNotificationConfiguration | Where-Object {$_.EnableApplePushNotificationService -eq $False}

## ESEMPIO 5

Nell'esempio 5 vengono restituite le informazioni per tutte le impostazioni di notifica Push in cui il servizio notifica Push Apple e/o il servizio notifica Push Microsoft sono stati disabilitati. A tale scopo, nel comando viene utilizzato innanzitutto il cmdlet **Get-CsPushNotificationConfiguration** per restituire una raccolta di tutte le impostazioni di notifica Push attualmente in uso. Questa raccolta viene quindi inoltrata tramite pipe al cmdlet Where-Object, che seleziona solo le impostazioni che soddisfano uno dei criteri seguenti o entrambi i criteri: 1) la proprietà EnableApplePushNotificationService è uguale a (-eq) False, 2) la proprietà EnableMicrosoftPushNotificationService è uguale a False. L'operatore –or indica a Where-Object di cercare le impostazioni che soddisfano uno dei due criteri. Per limitare i dati restituiti alle impostazioni in cui entrambi i servizi sono stati disabilitati, usare l'operatore –and:

Get-CsPushNotificationConfiguration | Where-Object {$\_.EnableApplePushNotificationService –eq $False –and $\_.EnableMicrosoftPushNotificationService –eq $False}

    Get-CsPushNotificationConfiguration | Where-Object {$_.EnableApplePushNotificationService -eq $False -or $_.EnableMicrosoftPushNotificationService -eq $False}

## Descrizione dettagliata

Il servizio notifica Push Apple e il servizio notifica Push Microsoft consentono agli utenti con telefoni Apple iPhone o Windows Phone in cui è in esecuzione Lync di ricevere notifiche relative agli eventi di Lync quando Lync è sospeso o in esecuzione in background. Gli utenti possono ad esempio ricevere notifiche per eventi come i seguenti:

\- Inviti a una nuova sessione di messaggistica istantanea o conferenza

\- Nuovi messaggi istantanei

\- Nuovi messaggi in segreteria telefonica

Senza il servizio notifica Push, gli utenti riceverebbero queste notifiche solo se Lync fosse in esecuzione come applicazione attiva e non in background.

Gli amministratori possono abilitare e disabilitare le notifiche Push per gli utenti con telefoni iPhone e/o Windows Phone. Per impostazione predefinita, le notifiche Push sono disabilitate sia per gli utenti con telefoni iPhone che Windows Phone. Gli amministratori possono quindi abilitare o disabilitare le notifiche Push nell'ambito globale utilizzando il cmdlet **Set-CsPushNotificationConfiguration**. Possono inoltre creare impostazioni di notifica Push personalizzate nell'ambito del sito utilizzando il cmdlet **New-CsPushNotificationConfiguration**.

Il cmdlet **Get-CsPushNotificationConfiguration** consente di restituire le informazioni sulle impostazioni di configurazione di notifica Push attualmente in uso nell'organizzazione.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsPushNotificationConfiguration** i membri dei gruppi seguenti: RTCUniversalServerAdmins.

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
<td><p>Consente di utilizzare i caratteri jolly per restituire una o più raccolte di impostazioni di configurazione di notifica Push. Per restituire una raccolta di tutte le impostazioni configurate nell'ambito del sito, utilizzare la sintassi seguente:</p>
<p>-Filter site:*</p>
<p>Per restituire una raccolta di tutte le impostazioni con valore stringa &quot;Canada&quot; nella relativa proprietà Identity (l'unica proprietà alla quale è possibile applicare un filtro), utilizzare la sintassi seguente:</p>
<p>-Filter &quot;*Canada*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Indica l'identificatore univoco della raccolta di impostazioni di notifica Push da restituire. Per fare riferimento alle impostazioni globali, utilizzare la sintassi seguente:</p>
<p>-Identity global</p>
<p>Per fare riferimento a una raccolta configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity site:Redmond</p>
<p>Si noti che non è possibile utilizzare caratteri jolly quando si specifica un parametro Identity. Se tuttavia è necessario utilizzare caratteri jolly, includere il parametro Filter.</p>
<p>Se questo parametro non è specificato, il cmdlet <strong>Get-CsPushNotificationConfiguration</strong> restituisce una raccolta di tutte le impostazioni di configurazione di notifica Push in uso nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione delle notifiche Push dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant Office 365 di cui è necessario modificare le impostazioni di configurazione di notifica Push. Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Se si usa una sessione remota di Windows PowerShell e si è connessi solo a Skype for Business online, non è necessario includere il parametro Tenant. L'ID del tenant verrà infatti compilato automaticamente in base alle informazioni di connessione. Il parametro Tenant è destinato principalmente all'uso in distribuzioni ibride.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Get-CsPushNotificationConfiguration** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsPushNotificationConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WriteableConfig.Settings.PushNotificationConfiguration.PushNotificationConfiguration.

