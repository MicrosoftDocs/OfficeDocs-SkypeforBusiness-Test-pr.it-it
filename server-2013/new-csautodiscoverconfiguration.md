---
title: New-CsAutodiscoverConfiguration
TOCTitle: New-CsAutodiscoverConfiguration
ms:assetid: 6b878b0e-f0c0-46a2-99b8-fd2105250600
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690022(v=OCS.15)
ms:contentKeyID: 49300886
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsAutodiscoverConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta di impostazioni di configurazione del servizio di individuazione automatica nell'ambito del sito. Questo servizio consente ad applicazioni client come Lync Web App o Microsoft Lync Mobile di individuare risorse chiave come ad esempio il pool principale di un utente o l'URL per partecipare a una conferenza telefonica con accesso esterno. Questo cmdlet è stato introdotto nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011.

## Sintassi

    New-CsAutodiscoverConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-ExternalSipClientAccessFqdn <String>] [-ExternalSipClientAccessPort <UInt32>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WebLinks <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando illustrato nell'esempio 1 consente di creare una nuova raccolta di impostazioni di configurazione del servizio di individuazione automatica per il sito Redmond. Poiché il parametro WebLinks non è stato incluso, queste impostazioni non conterranno URL di individuazione automatica.

    New-CsAutoDiscoverConfiguration -Identity "site:Redmond"

## ESEMPIO 2

I comandi riportati nell'esempio 2 creano una nuova raccolta di impostazioni di configurazione del servizio di individuazione automatica per il sito Redmond e assegnano alle nuove impostazioni due URL di individuazione automatica: http://LyncDiscover.fabrikam.com e http://LyncDiscoverInternal.fabrikam.com. A tale scopo, i primi due comandi utilizzano il cmdlet **New-CsWebLink** per creare i due URL di individuazione automatica. I nuovi URL creati vengono quindi archiviati in variabili denominate $Link1 e $Link2. Dopo la creazione dei due URL, il terzo comando utilizza il cmdlet **New-CsAutoDiscoverConfiguration** per creare le nuove impostazioni di configurazione del servizio di individuazione automatica. Per assegnare i due URL a queste impostazioni, viene incluso il parametro WebLinks insieme al valore di parametro @{Add=$Link1,$Link2}. Questa sintassi comporta l'aggiunta dei valori archiviati nelle variabili $Link1 e $Link2 nella proprietà WebLinks.

    $Link1 = New-CsWebLink -Token "Fabrikam" -Href "http://LyncDiscover.fabrikam.com"
    $Link2 = New-CsWebLink -Token "Fabrikam" -Href "http://LyncDiscoverInternal.fabrikam.com"
    
    New-CsAutoDiscoverConfiguration -Identity "site:Redmond" -WebLinks @{Add=$Link1,$Link2}

## Descrizione dettagliata

Per un utilizzo ottimale di Lync Server nelle applicazioni client, è necessario che tali applicazioni conoscano la posizione dei componenti chiave di Lync Server. Gli utenti autenticati ad esempio devono essere in grado di individuare il proprio pool principale. Dopotutto possono essere autenticati solo da tale pool. Analogamente, gli utenti non autenticati devono essere in grado di eseguire operazioni come l'individuazione dell'URL utilizzato per partecipare a una conferenza.

Se tutti gli utenti hanno eseguito l'accesso all'interno del firewall dell'organizzazione, l'individuazione di tali percorsi è relativamente semplice. Questa operazione tuttavia si complica quando gli utenti accedono al sistema dall'esterno utilizzando Microsoft Lync Mobile o Lync Web App.

Questa situazione si verifica in modo particolare in scenari di dominio diviso, in cui alcuni utenti di un'organizzazione dispongono di account nella versione locale di Lync Server, mentre altri dispongono di account in Skype for Business online. In questi casi, gli account utente possono trovarsi in foreste di Active Directory diverse e questo può rivelarsi problematico. Se ad esempio un utente degli Stati Uniti accede dall'Europa, il sistema deve essere in grado di riconoscere la relativa foresta e quindi associare la richiesta di accesso al pool appropriato.

Il servizio di individuazione automatica è stato introdotto nell'aggiornamento cumulativo per Lync Server di novembre 2011 per ovviare a questi problemi. Quando un'applicazione client tenta di accedere a Lync Server, il servizio di individuazione automatica analizza l'indirizzo SIP del client e quindi reindirizza la richiesta al pool appropriato. Le applicazioni client si connettono al servizio di individuazione automatica inviando una richiesta HTTP a un URL di individuazione automatica. Per il corretto funzionamento del servizio di individuazione automatica, è necessario che questi URL siano configurati dagli amministratori. Oltre a configurare gli URL, gli amministratori devono anche creare record DNS corrispondenti a tali URL.

Gli URL di individuazione automatica vengono assegnati alle impostazioni di configurazione del servizio di individuazione automatica. Queste impostazioni a loro volta possono essere applicate nell'ambito globale o nell'ambito del sito. Quando si installa Lync Server, viene creata automaticamente una raccolta globale di impostazioni. A tale raccolta tuttavia non viene assegnato alcun URL di individuazione automatica. Se una singola raccolta di impostazioni di individuazione automatica non soddisfa le proprie esigenze, è possibile utilizzare il cmdlet **New-CsAutoDiscoverConfiguration** per creare ulteriori impostazioni di configurazione nell'ambito del sito.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **New-CsAutoDiscoverConfiguration** in locale: RTCUniversalServerAdmins.

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
<td><p>Identificatore univoco per la raccolta di impostazioni di configurazione del servizio di individuazione automatica da modificare. Per creare una raccolta configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;site:Redmond&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExternalSipClientAccessFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo del server utilizzato per l'accesso dei client esterni.</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalSipClientAccessPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Porta utilizzata per l'accesso dei client esterni.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire il commit dell'oggetto come modifica permanente. Se si assegna l'output di un comando chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di tali modifiche chiamando il cmdlet <strong>Set-CsAutoDiscoverConfiguration</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>WebLinks</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Raccolta di URL di individuazione automatica. Questi URL devono essere creati tramite il cmdlet <strong>New-CsWebLink</strong>.</p></td>
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

Il cmdlet **New-CsAutoDiscoverConfiguration** non accetta input inviato tramite pipe.

## Tipi restituiti

Crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WriteableConfig.Settings.AutoDiscoverConfiguration.AutoDiscoverConfiguration.

