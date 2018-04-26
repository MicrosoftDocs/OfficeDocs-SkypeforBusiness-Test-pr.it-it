---
title: Set-CsMcxConfiguration
TOCTitle: Set-CsMcxConfiguration
ms:assetid: eaff70d9-97fa-482c-b9fb-a90263685b29
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690050(v=OCS.15)
ms:contentKeyID: 49302345
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsMcxConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una raccolta esistente di impostazioni di configurazione del servizio per dispositivi mobili di Lync Server. Il servizio per dispositivi mobili consente agli utenti di cellulari, come iPhone e Windows Phone, di eseguire operazioni quali lo scambio di messaggi istantanei e di informazioni sulla presenza, l'archiviazione e il recupero dei messaggi in segreteria telefonica internamente anziché tramite il provider wireless e l'utilizzo di funzionalità di Lync come Chiamata tramite ufficio e le conferenze telefoniche con chiamata esterna. Questo cmdlet è stato introdotto nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011.

## Sintassi

    Set-CsMcxConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsMcxConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-ExposedWebURL <External | Internal>] [-Force <SwitchParameter>] [-PushNotificationProxyUri <String>] [-SessionExpirationInterval <UInt32>] [-SessionShortExpirationInterval <UInt32>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 la proprietà ExposedWebURL delle impostazioni di configurazione del servizio per dispositivi mobili per il sito Redmond viene impostata su External.

    Set-CsMcxConfiguration -Identity site:Redmond -ExposedWebURL External

## ESEMPIO 2

Nell'esempio 2 viene illustrato in che modo tramite un singolo comando è possibile assegnare la stessa proprietà a tutte le impostazioni di configurazione del servizio per dispositivi mobili attualmente in uso nell'organizzazione. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsMcxConfiguration** senza parametri, per restituire una raccolta di tutte le impostazioni di configurazione del servizio per dispositivi mobili esistenti. La raccolta viene quindi inviata tramite pipe a **Set-CsMcxConfiguration**, che imposta la proprietà ExposedWebURL per ogni elemento della raccolta su External.

    Get-CsMcxConfiguration | Set-CsMcxConfiguration -ExposedWebURL External

## ESEMPIO 3

Nell'esempio 3 tutte le impostazioni di configurazione del servizio per dispositivi mobili con un valore di SessionShortExpirationInterval maggiore di 3600 secondi vengono modificate per impostare il valore della proprietà su 3600. In questo modo, 3600 secondi diventa il valore massimo per tutte le impostazioni di configurazione del servizio per dispositivi mobili nell'organizzazione. A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsMcxConfiguration** senza alcun parametro per restituire una raccolta di tutte le impostazioni di configurazione del servizio per dispositivi mobili attualmente in uso. Tale raccolta viene quindi inviata tramite pipe al cmdlet Where-Object che preleva solo le impostazioni in cui la proprietà SessionShortExpirationInterval è maggiore di (-gt) 3600. Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsMcxConfiguration** che imposta il valore della proprietà SessionShortExpirationInterval per ogni elemento nella raccolta su 3600.

    Get-CsMcxConfiguration | Where-Object {$_.SessionShortExpirationInterval -gt 3600} | Set-CsMcxConfiguration -SessionShortExpirationInterval 3600

## Descrizione dettagliata

Il servizio per dispositivi mobili Lync Server estende numerose funzionalità di Lync a dispositivi mobili come Apple iPhone, Windows Phone, telefoni Android e telefoni Nokia. Gli utenti possono tra l'altro utilizzare questi telefoni per scambiare messaggi istantanei e informazioni sulla presenza e per ricevere notifiche di nuovi messaggi in segreteria telefonica. Grazie al servizio notifica Push (servizio notifica Push Apple e servizio notifica Push Microsoft), gli utenti con telefoni iPhone o Windows Phone possono ricevere queste notifiche anche se Lync Server è in esecuzione in background. Il servizio per dispositivi mobili consente inoltre alle organizzazioni di abilitare la caratteristica Chiamata tramite ufficio. Con questa caratteristica, gli utenti possono effettuare una chiamata dal proprio cellulare e fare in modo che risulti provenire dal telefono dell'ufficio. Ad esempio, tramite i sistemi ID chiamante verrà visualizzato il numero dell'ufficio dell'utente anziché il numero del relativo cellulare.

Il servizio per dispositivi mobili viene gestito utilizzando le impostazioni di configurazione del servizio per dispositivi mobili che possono essere applicate all'ambito globale, del sito o del servizio (solo per il servizio del server Web). Queste impostazioni controllano aspetti come la durata massima di una sessione del servizio per dispositivi mobili, la disponibilità del servizio di individuazione automatica di Lync Server (che indirizza gli utenti del servizio per dispositivi mobili al pool di registrazione appropriato) per gli utenti che eseguono l'accesso al di fuori del firewall dell'organizzazione e la posizione del provider del servizio notifica Push.

Il cmdlet **Set-CsMcxConfiguration** consente agli amministratori di modificare qualsiasi impostazione di configurazione del servizio per dispositivi mobili esistente.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsMcxConfiguration** in locale: RTCUniversalServerAdmins.

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
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>ExposedWebURL</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.McxConfiguration.ExposedWebURL</p></td>
<td><p>Indica se gli utenti possono accedere all'URL utilizzato dal servizio di individuazione automatica sia dall'interno che dall'esterno del firewall dell'organizzazione (External) oppure solo dall'interno del firewall (Internal).</p>
<p>I valori consentiti sono: Internal o External. Il valore predefinito è External.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Impedisce la visualizzazione di eventuali messaggi di errore non irreversibili che potrebbero verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Rappresenta l'identificatore univoco della raccolta di impostazioni di configurazione del servizio per dispositivi mobili da modificare. Per modificare le impostazioni globali, utilizzare la sintassi seguente:</p>
<p>-Identity global</p>
<p>Per modificare le impostazioni nell'ambito del sito, utilizzare il prefisso &quot;site:&quot; seguito dal nome del sito. Ad esempio:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>Per modificare le impostazioni configurate nell'ambito del servizio, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity service:WebServer:atl-cs-001.litwareinc.com</p>
<p>Se questo parametro non viene specificato, il cmdlet <strong>Set-CsMcxConfiguration</strong> modifica le impostazioni globali.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto MCXConfiguration</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>PushNotificationProxyUri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URI di un provider di servizi che può inoltrare le richieste di notifiche Push al servizio notifica Push Apple e al servizio notifica Push Microsoft. PushNotificationProxyUri deve avere il formato di un indirizzo SIP, ad esempio:</p>
<p>-PushNotificationProxyUri &quot;sip:push@push.lync.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>SessionExpirationInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Durata, in secondi, di una sessione mobile per utenti di iPhone o Windows Phone. Se Lync è in esecuzione in background su questi telefoni, gli utenti riceveranno le notifiche Push finché l'intervallo di durata della sessione non scade.</p>
<p>Il dispositivo portatile deve inviare un avviso per il server che indica che il dispositivo è ancora attivo prima del raggiungimento del timeout della sessione. Se non esiste, il dispositivo verrà elencato come inattivo e l'utente dovrà accedere al sistema.</p>
<p>Questa proprietà può essere impostata su qualsiasi valore intero compreso tra 120 e 4294967295, inclusi. Il valore predefinito è 259200 secondi (3 giorni). Si noti che il valore della proprietà SessionExpirationInterval deve essere maggiore di quello della proprietà SessionShortExpirationInterval.</p></td>
</tr>
<tr class="even">
<td><p><em>SessionShortExpirationInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Durata, in secondi, di una sessione mobile per utenti di telefoni Android o Nokia.</p>
<p>Il dispositivo portatile deve inviare un avviso per il server che indica che il dispositivo è ancora attivo prima del raggiungimento del timeout della sessione. Se non esiste, il dispositivo verrà elencato come inattivo e l'utente dovrà accedere al sistema.</p>
<p>Questa proprietà può essere impostata su qualsiasi valore intero compreso tra 120 e 4294967295, inclusi. Il valore predefinito è 3600 secondi (1 ora). Si noti che il valore della proprietà SessionExpirationInterval deve essere maggiore di quello della proprietà SessionShortExpirationInterval.</p></td>
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

Oggetto Microsoft.Rtc.Management.WriteableConfig.Settings.McxConfiguration.McxConfiguration. Il cmdlet **Set-CsMcxConfiguration** accetta istanze dell'oggetto McxConfiguration inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsMcxConfiguration** modifica invece le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WriteableConfig.Settings.McxConfiguration.McxConfiguration.

