---
title: Remove-CsAutodiscoverConfiguration
TOCTitle: Remove-CsAutodiscoverConfiguration
ms:assetid: f7cda472-c23b-4eb9-b45b-b9353b93e1df
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690054(v=OCS.15)
ms:contentKeyID: 49302505
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsAutodiscoverConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una raccolta di impostazioni di configurazione del servizio di individuazione automatica. Questo servizio consente ad applicazioni client come Lync Web App di individuare risorse chiave come ad esempio il pool principale di un utente o l'URL per partecipare a una conferenza telefonica con accesso esterno. Questo cmdlet è stato introdotto nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011.

## Sintassi

    Remove-CsAutodiscoverConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando illustrato nell'esempio 1 consente di eliminare le impostazioni di configurazione del servizio di individuazione automatica per il sito Redmond.

    Remove-CsAutoDiscoverConfiguration -Identity "site:Redmond"

## ESEMPIO 2

Nell'esempio 2 vengono rimosse tutte le impostazioni di configurazione del servizio di individuazione automatica assegnate all'ambito del sito. A tale scopo, nel comando vengono prima utilizzati il cmdlet **Get-CsAutoDiscoverConfiguration** e il parametro Filter per restituire una raccolta delle impostazioni di configurazione. Il valore di filtro "site:\*" fa in modo che vengano restituite solo le impostazioni in cui l'identità inizia con il valore di stringa "site:". Tale raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsAutoDiscoverConfiguration**, che elimina ogni elemento della raccolta.

    Get-CsAutoDiscoverConfiguration -Filter "site:*" | Remove-CsAutoDiscoverConfiguration

## Descrizione dettagliata

Per un utilizzo ottimale di Lync Server nelle applicazioni client, è necessario che tali applicazioni conoscano il percorso dei componenti chiave di Lync Server. Gli utenti autenticati, ad esempio, devono essere in grado di individuare il proprio pool principale. Dopotutto possono essere autenticati solo da tale pool. Analogamente, gli utenti non autenticati devono essere in grado di eseguire operazioni come l'individuazione dell'URL utilizzato per partecipare a una conferenza.

Se tutti gli utenti hanno eseguito l'accesso all'interno del firewall dell'organizzazione, l'individuazione di tali percorsi è relativamente semplice. Questa operazione tuttavia si complica quando gli utenti accedono al sistema dall'esterno utilizzando applicazioni come Lync Web App.

Questa situazione si verifica in modo particolare in scenari di dominio diviso, in cui alcuni utenti di un'organizzazione dispongono di account nella versione locale di Lync Server, mentre altri dispongono di account in Skype for Business online. In questi casi, gli account utente possono trovarsi in foreste di Active Directory diverse e questo può rivelarsi problematico. Se, ad esempio, un utente degli Stati Uniti accede dall'Europa, il sistema deve essere in grado di riconoscere la relativa foresta e quindi associare la richiesta di accesso al pool appropriato.

Il servizio di individuazione automatica è stato introdotto nell'aggiornamento cumulativo per Lync Server di novembre 2011 per ovviare a questi problemi. Quando un'applicazione client tenta di accedere a Lync Server, il servizio di individuazione automatica analizza l'indirizzo SIP del client e quindi reindirizza la richiesta al pool appropriato. Le applicazioni client si connettono al servizio di individuazione automatica inviando una richiesta HTTP a un URL di individuazione automatica. Per il corretto funzionamento del servizio di individuazione automatica, è necessario che questi URL siano configurati dagli amministratori. Oltre a configurare gli URL, gli amministratori devono anche creare record DNS corrispondenti a tali URL.

Gli URL di individuazione automatica vengono assegnati alle impostazioni di configurazione del servizio di individuazione automatica, le quali a loro volta possono essere applicate all'ambito globale o all'ambito del sito. Se successivamente si decide di rimuovere le impostazioni assegnate all'ambito del sito, è possibile eseguire a tale scopo il cmdlet **Remove-CsAutoDiscoverConfiguration**. Si noti che questo cmdlet può essere eseguito anche per le impostazioni globali. In tal caso, tuttavia, le impostazioni globali non verranno rimosse, mentre verranno eliminati tutti gli URL di individuazione automatica assegnati alla raccolta globale.

Utenti autorizzati a eseguire questo cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsAutoDiscoverConfiguration** i membri dei gruppi seguenti: RTCUniversalServerAdmins.

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
<td><p>Identificatore univoco delle impostazioni di individuazione automatica da rimuovere. È possibile configurare tali impostazioni nell'ambito globale o del sito. Per &quot;rimuovere&quot; i criteri globali, utilizzare la sintassi seguente: -Identity global. Si noti che le impostazioni globali non possono essere effettivamente rimosse. Verranno invece reimpostati i valori predefiniti di tutte le relative proprietà.</p>
<p>Per rimuovere le impostazioni configurate nell'ambito del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>Non sono consentiti caratteri jolly per specificare un parametro Identity.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non irreversibile che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive cosa accadrebbe se si eseguisse il comando senza eseguirlo effettivamente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Microsoft.Rtc.Management.WriteableConfig.Settings.AutoDiscoverConfiguration.AutoDiscoverConfiguration. Il cmdlet **Remove-CsAutoDiscoverConfiguration** accetta l'input da pipeline di oggetti AutoDiscoverConfiguration

## Tipi restituiti

Nessuno. Il cmdlet elimina invece le istanze dell'oggetto Microsoft.Rtc.Management.WriteableConfig.Settings.AutoDiscoverConfiguration.AutoDiscoverConfiguration.

