---
title: Remove-CsMcxConfiguration
TOCTitle: Remove-CsMcxConfiguration
ms:assetid: 71904a62-a1f1-4466-9921-0a175909e117
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690026(v=OCS.15)
ms:contentKeyID: 49300941
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsMcxConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove la raccolta specificata di impostazioni di configurazione del servizio per dispositivi mobili di Lync Server 2013. Il servizio per dispositivi mobili consente agli utenti di cellulari, come iPhone e Windows Phone, di eseguire operazioni quali lo scambio di messaggi istantanei e di informazioni sulla presenza, l'archiviazione e il recupero dei messaggi in segreteria telefonica internamente anziché tramite il provider wireless e l'utilizzo di funzionalità di Lync Server come Chiamata tramite ufficio e le conferenze telefoniche con chiamata in uscita. Questo cmdlet è stato introdotto nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011.

## Sintassi

    Remove-CsMcxConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando illustrato nell'esempio 1 consente di eliminare la raccolta di impostazioni di configurazione del servizio per dispositivi mobili assegnate al sito Redmond.

    Remove-CsMcxConfiguration -Identity "site:Redmond"

## ESEMPIO 2

Nell'esempio 2 tutte le impostazioni di configurazione del servizio per dispositivi mobili assegnate all'ambito del servizio vengono rimosse. A tale scopo, viene utilizzato il cmdlet **Get-CsMcxConfiguration** insieme al parametro Filter. Il valore di filtro "service:\*" garantisce che vengano restituite solo le impostazioni con un parametro Identity che inizia con il valore stringa "service:". Tale raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsMcxConfiguration**, che provvede alla sua eliminazione.

    Get-CsMcxConfiguration -Filter "service:*" | Remove-CsMcxConfiguration

## ESEMPIO 3

Nell'esempio 3 vengono eliminate tutte le impostazioni di configurazione del servizio per dispositivi mobili in cui la proprietà ExposedWebURL è stata configurata su Internal. A tale scopo, nel comando viene innanzitutto chiamato il cmdlet **Get-CsMcxConfiguration** senza alcun parametro. In questo modo viene restituita una raccolta di tutte le impostazioni di configurazione del servizio per dispositivi mobili attualmente in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui ExposedWebURL è uguale a (-eq) Internal. La raccolta filtrata viene a sua volta inviata tramite pipe al cmdlet **Remove-CsMcxConfiguration**, che elimina ogni elemento di tale raccolta.

    Get-CsMcxConfiguration | Where-Object {$_.ExposedWebURL -eq "Internal"} | Remove-CsMcxConfiguration

## ESEMPIO 4

Nell'esempio 4 tutte le impostazioni di configurazione del servizio per dispositivi mobili a cui non è assegnato un URI proxy di notifica Push vengono rimosse da Lync Server. A tale scopo, nel comando viene utilizzato innanzitutto il cmdlet **Get-CsMcxConfiguration** senza alcun parametro per restituire una raccolta di tutte le impostazioni di configurazione del servizio per dispositivi mobili attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona le impostazioni la cui proprietà PushNotificationProxyUri è uguale a (-eq) un valore Null. La impostazioni che soddisfano questo criterio vengono quindi inviate tramite pipe al cmdlet **Remove-CsMcxConfiguration**, che le elimina.

    Get-CsMcxConfiguration | Where-Object {$_.PushNotificationProxyUri -eq $Null} | Remove-CsMcxConfiguration

## Descrizione dettagliata

Il servizio per dispositivi mobili estende numerose funzionalità di Lync Server a dispositivi mobili come Apple iPhone, Windows Phone, telefoni Android e telefoni Nokia. Gli utenti possono tra l'altro utilizzare questi telefoni per scambiare messaggi istantanei e informazioni sulla presenza e per ricevere notifiche di nuovi messaggi in segreteria telefonica. Grazie al servizio di notifica push (servizio di notifica push Apple e servizio di notifica push Microsoft), gli utenti con telefoni iPhone o Windows Phone possono ricevere queste notifiche anche se Lync è in esecuzione in background. Il servizio per dispositivi mobili consente inoltre alle organizzazioni di abilitare la funzionalità Chiamata tramite ufficio. Grazie a questa funzionalità, gli utenti possono effettuare una chiamata dal proprio cellulare e fare in modo che risulti provenire dal telefono dell'ufficio. Ad esempio, i sistemi con ID chiamante visualizzeranno il numero dell'ufficio dell'utente anziché il numero del relativo cellulare.

Il servizio per dispositivi mobili viene gestito utilizzando le relative impostazioni di configurazione che possono essere applicate all'ambito globale, del sito o del servizio (solo per il servizio del server Web). Queste impostazioni controllano aspetti come la durata massima di una sessione del servizio per dispositivi mobili, la disponibilità del servizio di individuazione automatica (che indirizza gli utenti del servizio per dispositivi mobili al pool di registrazione appropriato) per gli utenti che eseguono l'accesso al di fuori del firewall dell'organizzazione e la posizione del provider del servizio di notifica push.

Quando si installa Lync Server, viene creata una singola raccolta di impostazioni di configurazione del servizio per dispositivi mobili nell'ambito globale. Gli amministratori possono tuttavia creare impostazioni di configurazione personalizzate nell'ambito del sito o del servizio. Queste impostazioni personalizzate possono successivamente essere rimosse utilizzando il cmdlet **Remove-CsMcxConfiguration**. Se si rimuovono le impostazioni del servizio, i server del servizio per dispositivi mobili precedentemente gestiti da tali impostazioni verranno gestiti dalle impostazioni del sito, se disponibili, oppure dalle impostazioni globali. Se si rimuovono le impostazioni del sito, i server verranno gestiti dalle impostazioni globali.

Si noti che è anche possibile eseguire il cmdlet **Remove-CsMcxConfiguration** sulle impostazioni globali. In tal caso, tuttavia, le impostazioni globali non verranno rimosse, ma verranno semplicemente ripristinati i valori predefiniti delle proprietà incluse nella raccolta globale.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsMcxConfiguration** i membri dei gruppi seguenti: RTCUniversalServerAdmins.

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
<td><p>Identificatore univoco delle impostazioni di configurazione del servizio per dispositivi mobili da rimuovere. Per &quot;rimuovere&quot; le impostazioni globali, utilizzare la sintassi seguente:</p>
<p>-Identity global</p>
<p>Si noti che non è possibile rimuovere realmente le impostazioni globali, ma solo ripristinare i valori predefiniti delle proprietà.</p>
<p>Per rimuovere le impostazioni dall'ambito del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity site:Redmond</p>
<p>Per rimuovere le impostazioni configurate nell'ambito del servizio, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity service:WebServer:atl-cs-001.litwareinc.com</p>
<p>Non è possibile utilizzare caratteri jolly per specificare il parametro Identity.</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WriteableConfig.Settings.McxConfiguration.McxConfiguration. Il cmdlet **Remove-CsMcxConfiguration** accetta input inviato tramite pipeline di oggetti McxConfiguration.

## Tipi restituiti

Nessuno. Il cmdlet elimina istanze dell'oggetto Microsoft.Rtc.Management.WriteableConfig.Settings.McxConfiguration.McxConfiguration.

