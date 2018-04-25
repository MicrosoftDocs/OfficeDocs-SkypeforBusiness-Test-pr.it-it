---
title: New-CsMcxConfiguration
TOCTitle: New-CsMcxConfiguration
ms:assetid: 9eebea4a-64a3-424c-9b05-0579c4e8111e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690035(v=OCS.15)
ms:contentKeyID: 49301484
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsMcxConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta di impostazioni di configurazione del servizio per dispositivi mobili di Lync Server 2013 nell'ambito del sito o del servizio. Il servizio per dispositivi mobili consente agli utenti di cellulari, come iPhone e Windows Phone, di eseguire operazioni quali lo scambio di messaggi istantanei e di informazioni sulla presenza, l'archiviazione e il recupero dei messaggi in segreteria telefonica internamente anziché tramite il provider wireless e l'utilizzo di funzionalità di Lync Server come Chiamata tramite ufficio e le conferenze telefoniche con chiamata in uscita. Questo cmdlet è stato introdotto nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011.

## Sintassi

    New-CsMcxConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-ExposedWebURL <External | Internal>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-PushNotificationProxyUri <String>] [-SessionExpirationInterval <UInt32>] [-SessionShortExpirationInterval <UInt32>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene creata una nuova raccolta di impostazioni di configurazione del servizio per dispositivi mobili per il sito Redmond e la raccolta viene automaticamente assegnata a tale sito. In questo esempio vengono apportate due modifiche alle impostazioni di configurazione predefinite del servizio per dispositivi mobili: la proprietà ExposedWebURL viene impostata su Internal e la proprietà SessionShortExpirationInterval viene impostata su 7200 secondi.

    New-CsMcxConfiguration -Identity "site:Redmond" -ExposedWebURL Internal -SessionShortExpirationInterval 7200

## ESEMPIO 2

Nell'esempio 2 viene creato un insieme identico di impostazioni di configurazione del servizio per dispositivi mobili per ogni server Web attualmente in uso in un'organizzazione. A tale scopo, viene utilizzato il cmdlet **Get-CsService** insieme al parametro WebServer, per restituire una raccolta di tutti i server Web esistenti. La raccolta viene quindi inviata tramite pipe al cmdlet **For-Each**-Object. A sua volta, il cmdlet **ForEach-Object** seleziona ogni server della raccolta ed esegue il cmdlet **New-CsMcxConfiguration** per creare nuove impostazioni di configurazione del servizio per dispositivi mobili in tale server.

    Get-CsService -WebServer | ForEach-Object {New-CsMcxConfiguration -Identity $_.Identity -ExposedWebURL Internal -SessionShortExpirationInterval 7200}

## ESEMPIO 3

Nell'esempio 3 viene illustrato in che modo il parametro InMemory consente di creare una nuova raccolta di impostazioni di configurazione del servizio per dispositivi mobili in memoria, modificare i valori delle proprietà di tale raccolta e quindi salvare la raccolta in Lync Server. A tale scopo, tramite il primo comando viene creata una nuova raccolta di impostazioni di configurazione del servizio per dispositivi mobili con l'identità site:Redmond. Anziché venire create e assegnate automaticamente al sito Redmond, queste impostazioni vengono create solo in memoria (a causa del parametro InMemory) e quindi archiviate in una variabile denominata $x.

I comandi 2 e 3 nell'esempio illustrano come modificare i valori delle proprietà di questa raccolta di configurazioni virtuali del servizio per dispositivi mobili. Dopo aver apportato le modifiche desiderate ai valori delle proprietà, è possibile utilizzare il cmdlet **Set-CsMcxConfiguration** e il parametro Instance per trasformare le impostazioni virtuali in una raccolta effettiva di impostazioni di configurazione del servizio per dispositivi mobili assegnate al sito Redmond. Si noti che se non si chiama il cmdlet **Set-CsMcxConfiguration**, al sito Redmond non verranno assegnate impostazioni e la raccolta virtuale verrà eliminata non appena si termina la sessione di Windows PowerShell o si elimina la variabile $x.

    $x = New-CsMcxConfiguration -Identity "site:Redmond" -InMemory
    $x.ExposedWebURL = "Internal"
    $x.SessionShortExpirationInterval = 7200
    Set-CsMcxConfiguration -Instance $x

## Descrizione dettagliata

Il servizio per dispositivi mobili estende numerose funzionalità di Lync Server a dispositivi mobili come Apple iPhone, Windows Phone, telefoni Android e telefoni Nokia. Gli utenti possono tra l'altro utilizzare questi telefoni per scambiare messaggi istantanei e informazioni sulla presenza e per ricevere notifiche di nuovi messaggi in segreteria telefonica. Grazie al servizio notifica Push (servizio notifica Push Apple e servizio notifica Push Microsoft), gli utenti con telefoni iPhone o Windows Phone possono ricevere queste notifiche anche se Lync è in esecuzione in background. Il servizio per dispositivi mobili consente inoltre alle organizzazioni di abilitare la funzionalità Chiamata tramite ufficio. Grazie a questa funzionalità, gli utenti possono effettuare una chiamata dal proprio cellulare e fare in modo che risulti provenire dal telefono dell'ufficio. Ad esempio, i sistemi con ID chiamante visualizzeranno il numero dell'ufficio dell'utente anziché il numero del relativo cellulare.

Il servizio per dispositivi mobili viene gestito utilizzando le relative impostazioni di configurazione che possono essere applicate all'ambito globale, del sito o del servizio (solo per il servizio del server Web). Queste impostazioni controllano aspetti come la durata massima di una sessione del servizio per dispositivi mobili, la disponibilità del servizio di individuazione automatica di Lync Server (che indirizza gli utenti del servizio per dispositivi mobili al pool di registrazione appropriato) per gli utenti che eseguono l'accesso al di fuori del firewall dell'organizzazione e la posizione del provider del servizio notifica Push.

Quando si installa Lync Server, viene creata una singola raccolta di impostazioni di configurazione del servizio per dispositivi mobili nell'ambito globale. Gli amministratori possono tuttavia utilizzare il cmdlet **New-CsMcxConfiguration** per creare impostazioni di configurazione personalizzate nell'ambito del sito o del servizio.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsMcxConfiguration** i membri dei gruppi seguenti: RTCUniversalServerAdmins.

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
<td><p>Identificatore univoco della raccolta di impostazioni di configurazione del servizio per dispositivi mobili da creare. Per creare le impostazioni nell'ambito del sito, utilizzare il prefisso &quot;site:&quot; seguito dal nome del sito. Ad esempio:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>Per creare le impostazioni configurate nell'ambito del servizio, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity service:WebServer:atl-cs-001.litwareinc.com</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di visualizzare una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExposedWebURL</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.McxConfiguration.ExposedWebURL</p></td>
<td><p>Indica se gli utenti possono accedere all'URL utilizzato dal servizio di individuazione automatica sia dall'interno che dall'esterno del firewall dell'organizzazione (External) oppure solo dall'interno del firewall (Internal).</p>
<p>I valori consentiti sono: Internal o External. Il valore predefinito è External.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non irreversibile che potrebbe verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output di un comando chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>PushNotificationProxyUri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URI di un provider di servizi che può inoltrare le richieste di notifica push al servizio notifica Push Apple e al servizio notifica Push Microsoft. PushNotificationProxyUri deve avere il formato di un indirizzo SIP, ad esempio:</p>
<p>-PushNotificationProxyUri &quot;sip:push@push.lync.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>SessionExpirationInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Durata, in secondi, di una sessione per dispositivi mobili per utenti di iPhone o Windows Phone. Se Lync è in esecuzione in background in questi telefoni, gli utenti riceveranno notifiche push per tutta la durata dell'intervallo di scadenza della sessione.</p>
<p>Il dispositivo mobile deve inviare un avviso al server per indicare che il dispositivo è ancora attivo prima del raggiungimento del timeout della sessione. In caso contrario, il dispositivo viene contrassegnato come non attivo e l'utente deve eseguire di nuovo l'accesso al sistema.</p>
<p>Questa proprietà può essere impostata su qualsiasi valore intero compreso tra 120 e 4294967295, inclusi. Il valore predefinito è 259200 secondi (3 giorni). Si noti che il valore della proprietà SessionExpirationInterval deve essere maggiore di quello della proprietà SessionShortExpirationInterval.</p></td>
</tr>
<tr class="even">
<td><p><em>SessionShortExpirationInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Durata, in secondi, di una sessione per dispositivi mobili per utenti di telefoni Android o Nokia.</p>
<p>Prima che venga raggiunto il timeout della sessione, il dispositivo mobile deve inviare al server un avviso per indicare di essere ancora attivo. In caso contrario, il dispositivo viene contrassegnato come non attivo e l'utente deve eseguire di nuovo l'accesso al sistema.</p>
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

Nessuno. Il cmdlet **New-CsMcxConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Crea una nuova istanza dell'oggetto Microsoft.Rtc.Management.WriteableConfig.Settings.McxConfiguration.McxConfiguration.

