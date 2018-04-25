---
title: Get-CsAutodiscoverConfiguration
TOCTitle: Get-CsAutodiscoverConfiguration
ms:assetid: 221d26d6-0f77-4873-8872-d600913eb98b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690014(v=OCS.15)
ms:contentKeyID: 49299922
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAutodiscoverConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle impostazioni di configurazione del servizio di individuazione automatica attualmente in uso in un'organizzazione. Tale servizio consente ad applicazioni client come Lync Web App di individuare risorse chiave, ad esempio il pool principale di un utente o l'URL per partecipare a una conferenza telefonica con accesso esterno. Questo cmdlet è stato introdotto nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011.

## Sintassi

    Get-CsAutodiscoverConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsAutodiscoverConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Tramite il comando illustrato nell'esempio 1 vengono restituite tutte le impostazioni di configurazione del servizio di individuazione automatica attualmente in uso nell'organizzazione.

    Get-CsAutoDiscoverConfiguration

## ESEMPIO 2

Nell'esempio 2 viene restituita solo una raccolta di impostazioni di configurazione del servizio di individuazione automatica, ovvero la raccolta globale.

    Get-CsAutoDiscoverConfiguration -Identity "global"

## ESEMPIO 3

Il comando riportato nell'esempio 3 restituisce tutte le impostazioni di configurazione del servizio di individuazione automatica assegnate nell'ambito del sito. Per ottenere questo risultato, viene incluso il parametro Filter con valore "site:\*". Questo valore di filtro garantisce che vengano restituite solo le impostazioni con parametro Identity che inizia con il valore stringa "site:". Per definizione, le impostazioni con un parametro Identity che inizia con "site:" sono impostazioni configurate nell'ambito del sito.

    Get-CsAutoDiscoverConfiguration -Filter "site:*"

## ESEMPIO 4

Il comando riportato nell'esempio 4 restituisce tutte le impostazioni di configurazione del servizio di individuazione automatica che includono un URL di individuazione automatica per fabrikam.com. A tale scopo, nel comando viene utilizzato innanzitutto il cmdlet **Get-CsAutoDiscoverConfiguration** per restituire una raccolta di tutte le impostazioni di individuazione automatica attualmente in uso nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà WebLinks include il valore stringa "fabrikam.com".

    Get-CsAutoDiscoverConfiguration | Where-Object {$_.WebLinks -like "*fabrikam.com"}

## Descrizione dettagliata

Per un utilizzo ottimale di Lync Server nelle applicazioni client, è necessario che tali applicazioni conoscano la posizione dei componenti chiave di Lync Server. Gli utenti autenticati ad esempio devono essere in grado di individuare il proprio pool principale. Dopotutto possono essere autenticati solo da tale pool. Analogamente, gli utenti non autenticati devono essere in grado di eseguire operazioni come l'individuazione dell'URL utilizzato per partecipare a una conferenza.

Se tutti gli utenti hanno eseguito l'accesso all'interno del firewall dell'organizzazione, l'individuazione di tali percorsi è relativamente semplice. Questa operazione tuttavia si complica quando gli utenti accedono al sistema dall'esterno utilizzando applicazioni come Lync Web App.

Questa situazione si verifica in modo particolare in scenari di dominio diviso, in cui alcuni utenti di un'organizzazione dispongono di account nella versione locale di Lync Server, mentre altri dispongono di account in Skype for Business online. In questi casi, gli account utente possono trovarsi in foreste di Active Directory diverse e questo può rivelarsi problematico. Se ad esempio un utente degli Stati Uniti accede dall'Europa, il sistema deve essere in grado di riconoscere la relativa foresta e quindi associare la richiesta di accesso al pool appropriato.

Il servizio di individuazione automatica è stato introdotto nell'aggiornamento cumulativo per Lync Server di novembre 2011 per ovviare a questi problemi. Quando un'applicazione client tenta di accedere a Lync Server, il servizio di individuazione automatica analizza l'indirizzo SIP del client e quindi reindirizza la richiesta al pool appropriato. Le applicazioni client si connettono al servizio di individuazione automatica inviando una richiesta HTTP a un URL di individuazione automatica. Per il corretto funzionamento del servizio di individuazione automatica, è necessario che questi URL siano configurati dagli amministratori. Oltre a configurare gli URL, gli amministratori devono anche creare record DNS corrispondenti a tali URL.

Gli URL di individuazione automatica vengono assegnati alle impostazioni di configurazione del servizio di individuazione automatica, le quali a loro volta possono essere applicate all'ambito globale o all'ambito del sito. Il cmdlet **Get-CsAutoDiscoverConfiguration** consente di restituire informazioni sulle impostazioni di individuazione automatica, e sugli URL di individuazione automatica, attualmente in uso nell'organizzazione.

Utenti autorizzati a eseguire questo cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsAutoDiscoverConfiguration** i membri dei gruppi seguenti: RTCUniversalServerAdmins.

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
<td><p>Consente di utilizzare i caratteri jolly per specificare l'identità delle impostazioni di configurazione del servizio di individuazione automatica da restituire. Con la sintassi seguente, ad esempio, vengono restituite tutte le impostazioni configurate nell'ambito del sito:</p>
<p>-Filter &quot;site:*&quot;</p>
<p>Si noti che non è possibile utilizzare entrambi i parametri Identity e Filter nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per la raccolta di impostazioni di configurazione del servizio di individuazione automatica da recuperare. Per recuperare le impostazioni globali, utilizzare la sintassi seguente:</p>
<p>-Identity &quot;global&quot;</p>
<p>Per recuperare le impostazioni configurate nell'ambito del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>Se questo parametro non viene incluso, il cmdlet <strong>Get-CsAutoDiscoverConfiguration</strong> restituisce tutte le impostazioni di configurazione del servizio di individuazione automatica attualmente in uso nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione del servizio di individuazione automatica dalla replica locale dell'archivio di gestione centrale anziché direttamente dall'archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Get-CsAutoDiscoverConfiguration** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsAutoDiscoverConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WriteableConfig.Settings.AutoDiscoverConfiguration.AutoDiscoverConfiguration.

