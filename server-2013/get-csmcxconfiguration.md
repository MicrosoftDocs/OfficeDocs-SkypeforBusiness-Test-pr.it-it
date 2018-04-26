---
title: Get-CsMcxConfiguration
TOCTitle: Get-CsMcxConfiguration
ms:assetid: a09c0d49-5377-4a22-89e6-2751030ccf20
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690031(v=OCS.15)
ms:contentKeyID: 49301502
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsMcxConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera le informazioni sulle impostazioni di configurazione del servizio per dispositivi mobili di Lync Server attualmente in uso nell'organizzazione. Il servizio per dispositivi mobili consente agli utenti di cellulari, come iPhone e Windows Phone, di eseguire operazioni quali lo scambio di messaggi istantanei e di informazioni sulla presenza, l'archiviazione e il recupero dei messaggi in segreteria telefonica internamente anziché tramite il provider wireless e l'utilizzo di funzionalità di Lync Server come Chiamata tramite ufficio e le conferenze telefoniche con chiamata esterna. Questo cmdlet è stato introdotto nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011.

## Sintassi

    Get-CsMcxConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsMcxConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Il comando illustrato nell'esempio 1 restituisce le informazioni su tutte le impostazioni di configurazione del servizio per dispositivi mobili attualmente in uso nell'organizzazione.

    Get-CsMcxConfiguration

## ESEMPIO 2

Nell'esempio 2 vengono restituite informazioni solo per la raccolta globale di impostazioni di configurazione del servizio per dispositivi mobili.

    Get-CsMcxConfiguration -Identity "global"

## ESEMPIO 3

Nell'esempio 3 vengono restituite informazioni su tutte le impostazioni di configurazione del servizio per dispositivi mobili assegnate all'ambito del servizio. A tale scopo, viene incluso il parametro Filter insieme al valore stringa "service:\*". Tale valore di filtro restituisce tutte le impostazioni di configurazione del servizio per dispositivi mobili il cui parametro Identity inizia con il valore stringa "service:".

    Get-CsMcxConfiguration -Filter "service:*"

## ESEMPIO 4

Nell'esempio 4 vengono restituite solo le impostazioni di configurazione del servizio per dispositivi mobili in cui la proprietà ExposedWebURL è uguale a External. A tale scopo, nel comando viene innanzitutto chiamato il cmdlet **Get-CsMcxConfiguration** senza parametri per restituire una raccolta di tutte le impostazioni di configurazione del servizio per dispositivi mobili in uso nell'organizzazione. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà ExposedWebURL è uguale a (-eq) External.

    Get-CsMcxConfiguration | Where-Object {$_.ExposedWebURL -eq "External"}

## ESEMPIO 5

Nell'esempio 5 vengono restituite tutte le eventuali impostazioni di configurazione del servizio per dispositivi mobili in cui la proprietà SessionExpirationInterval è impostata su un valore minore del valore predefinito di 259200 secondi (72 ore). A tale scopo, viene innanzitutto utilizzato il cmdlet **Get-CsMcxConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione del servizio per dispositivi mobili esistenti. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object** che, a sua volta, seleziona solo le impostazioni in cui il valore della proprietà SessionExpirationInterval è minore di 259200.

    Get-CsMcxConfiguration | Where-Object {$_.SessionExpirationInterval -lt 259200}

## Descrizione dettagliata

Il servizio per dispositivi mobili di Lync Server estende numerose funzionalità di Lync Server a dispositivi mobili come Apple iPhone, Windows Phone, telefoni Android e telefoni Nokia. Gli utenti possono tra l'altro utilizzare questi telefoni per scambiare messaggi istantanei e informazioni sulla presenza e per ricevere notifiche di nuovi messaggi in segreteria telefonica. Grazie al servizio notifica Push (servizio notifica Push Apple e servizio notifica Push Microsoft), gli utenti con telefoni iPhone o Windows Phone possono ricevere queste notifiche anche se Lync è in esecuzione in background. Il servizio per dispositivi mobili consente inoltre alle organizzazioni di abilitare la funzionalità Chiamata tramite ufficio. Grazie a questa funzionalità, gli utenti possono effettuare una chiamata dal proprio cellulare e fare in modo che risulti provenire dal telefono dell'ufficio. Ad esempio, nei sistemi con ID chiamante verrà visualizzato il numero dell'ufficio dell'utente anziché il numero del relativo cellulare.

Il servizio per dispositivi mobili viene gestito mediante le relative impostazioni di configurazione che possono essere applicate all'ambito globale, del sito o del servizio (solo per il servizio del server Web). Queste impostazioni controllano aspetti come la durata massima di una sessione del servizio per dispositivi mobili, la disponibilità del servizio di individuazione automatica di Lync Server (che indirizza gli utenti del servizio per dispositivi mobili al pool di registrazione appropriato) per gli utenti che eseguono l'accesso al di fuori del firewall dell'organizzazione e la posizione del provider del servizio notifica Push. Il cmdlet **Get-CsMcxConfiguration** consente agli amministratori di recuperare informazioni relative a tutte le impostazioni di configurazione del servizio per dispositivi mobili attualmente in uso nell'organizzazione.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsMcxConfiguration** i membri dei gruppi seguenti: RTCUniversalServerAdmins.

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
<td><p>Consente di utilizzare i caratteri jolly per restituire una raccolta di impostazioni di configurazione del servizio per dispositivi mobili. Per restituire, ad esempio, una raccolta di tutte le impostazioni configurate nell'ambito del sito, utilizzare la sintassi seguente:</p>
<p>-Filter site:*</p>
<p>Per restituire una raccolta di tutte le impostazioni configurate nell'ambito del servizio, utilizzare la sintassi seguente:</p>
<p>-Filter service:*</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Indica l'identificatore univoco della raccolta di impostazioni di configurazione del servizio per dispositivi mobili da restituire. Per fare riferimento alle impostazioni globali, utilizzare la sintassi seguente:</p>
<p>-Identity global</p>
<p>Per far riferimento a una raccolta configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity site:Redmond</p>
<p>Per fare riferimento a una raccolta configurata nell'ambito del servizio, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity service:WebServer:atl-cs-001.litwareinc.com</p>
<p>Si noti che non è possibile utilizzare caratteri jolly quando si specifica un parametro Identity. Se si desidera utilizzare i caratteri jolly, è necessario utilizzare il parametro Filter.</p>
<p>Se questo parametro non è specificato, il cmdlet <strong>Get-CsMcxConfiguration</strong> restituisce una raccolta di tutte le impostazioni di configurazione del servizio per dispositivi mobili in uso nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione del servizio per dispositivi mobili dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Get-CsMcxConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsMcxConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WriteableConfig.Settings.McxConfiguration.McxConfiguration.

