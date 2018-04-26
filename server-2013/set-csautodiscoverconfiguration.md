---
title: Set-CsAutodiscoverConfiguration
TOCTitle: Set-CsAutodiscoverConfiguration
ms:assetid: 06f59d62-b4dd-4b50-9cf3-40d6d41d74af
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh689980(v=OCS.15)
ms:contentKeyID: 49299574
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsAutodiscoverConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una raccolta esistente di impostazioni di configurazione del servizio di individuazione automatica. Questo servizio consente ad applicazioni client come Lync Web App o Lync Mobile di individuare risorse chiave come ad esempio il pool principale di un utente o l'URL per partecipare a una conferenza telefonica con accesso esterno. Questo cmdlet è stato introdotto nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011.

## Sintassi

    Set-CsAutodiscoverConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsAutodiscoverConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-ExternalSipClientAccessFqdn <String>] [-ExternalSipClientAccessPort <UInt32>] [-Force <SwitchParameter>] [-WebLinks <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

I comandi riportati nell'esempio 1 aggiungono un nuovo URL di individuazione automatica (http://LyncDiscover.fabrikam.com) alle impostazioni di configurazione del servizio di individuazione automatica assegnate al sito Redmond. A tale scopo, nel primo comando dell'esempio viene utilizzato il cmdlet **New-CsWebLink** per creare un nuovo URL di individuazione automatica. Tale URL viene archiviato in una variabile denominata $Link1. Nel secondo comando viene utilizzato il cmdlet **Set-CsAutoDiscoverConfiguration** per aggiungere il nuovo URL agli URL già assegnati a tali impostazioni. Questa operazione viene effettuata utilizzando il parametro WebLinks con il valore @{Add=$Link1}.

    $Link1 = New-CsWebLink -Token "Fabrikam" -Href "http://LyncDiscover.fabrikam.com"
    
    Set-CsAutoDiscoverConfiguration -Identity "site:Redmond" -WebLinks @{Add=$Link1}

## ESEMPIO 2

I comandi riportati nell'esempio 2 illustrano come rimuovere un URL da una raccolta di impostazioni di configurazione del servizio di individuazione automatica. A tale scopo, il primo comando della raccolta recupera un riferimento oggetto all'URL da eliminare (un URL con Token uguale a "Fabrikam"). Questa operazione viene effettuata innanzitutto chiamando il cmdlet **Get-CsAutoDiscoverConfiguration** per recuperare le impostazioni del servizio di individuazione automatica per il sito Redmond. Tale raccolta viene quindi inviata tramite pipe al cmdlet **Select-Object**, che utilizza il parametro ExpandProperty per "espandere" la proprietà WebLinks. Quando una proprietà è espansa, al cmdlet **Get-CsAutoDiscoverConfiguration** viene fornito l'accesso ai singoli oggetti in essa archiviati. Questi oggetti WebLinks vengono quindi inviati tramite pipe al cmdlet **Where-Object**, che seleziona l'oggetto con proprietà Token uguale a "Fabrikam". Tale oggetto WebLinks viene quindi archiviato in una variabile denominata $Link1.

Nel secondo comando dell'esempio viene quindi utilizzato il cmdlet **Set-CsAutoDiscoverConfiguration** per rimuovere l'oggetto archiviato in $Link1. A tale scopo, nel comando vengono utilizzati il parametro WebLinks e il valore @{Remove=$Link1}.

    $Link1 = Get-CsAutoDiscoverConfiguration  -Identity "site:Redmond" | Select-Object -ExpandProperty WebLinks | Where-Object {$_.Token -eq "Fabrikam"}
    
    Set-CsAutoDiscoverConfiguration -Identity "site:Redmond" -WebLinks @{Remove=$Link1}

## ESEMPIO 3

Nell'esempio 3 viene illustrato come sostituire una raccolta esistente di URL di individuazione automatica con, in questo caso, un singolo URL. Per eseguire questa operazione, nel primo comando dell'esempio viene utilizzato il cmdlet **New-CsWebLink** per creare un nuovo URL di individuazione automatica per http://LyncDiscover.contoso.com. L'URL risultante viene archiviato in una variabile denominata $Link2. Nel secondo comando vengono quindi utilizzati il cmdlet **Set-CsAutoDiscoverConfiguration** e il parametro WebLinks per rimuovere gli URL precedentemente assegnati al sito Redmond e sostituirli con l'URL per http://LyncDiscover.contoso.com. A tale scopo, nel comando viene utilizzato il metodo Replace anziché il metodo Add o Remove.

    $Link2 = New-CsWebLink -Token "Contoso" -Href "http://LyncDiscover.contoso.com"
    
    Set-CsAutoDiscoverConfiguration -Identity "site:Redmond" -WebLinks @{Replace=$Link2}

## ESEMPIO 4

Il comando illustrato nell'esempio 4 consente di rimuovere tutti gli URL di individuazione automatica assegnati al sito Redmond. A tale scopo, il comando imposta la proprietà WebLinks su un valore Null. In questo modo vengono eliminati tutti gli URL precedentemente assegnati a tale proprietà.

    Set-CsAutoDiscoverConfiguration -Identity "site:Redmond" -WebLinks $Null

## Descrizione dettagliata

Per un utilizzo ottimale di Lync Server nelle applicazioni client, è necessario che tali applicazioni conoscano la posizione dei componenti chiave di Lync Server. Gli utenti autenticati ad esempio devono essere in grado di individuare il proprio pool principale. Dopotutto possono essere autenticati solo da tale pool. Analogamente, gli utenti non autenticati devono essere in grado di eseguire operazioni come l'individuazione dell'URL utilizzato per partecipare a una conferenza.

Se tutti gli utenti hanno eseguito l'accesso all'interno del firewall dell'organizzazione, l'individuazione di tali percorsi è relativamente semplice. Questa operazione tuttavia si complica quando gli utenti accedono al sistema dall'esterno utilizzando Lync Mobile o Lync Web App.

Questa situazione si verifica in modo particolare in scenari di dominio diviso, in cui alcuni utenti di un'organizzazione dispongono di account nella versione locale di Lync Server, mentre altri dispongono di account in Office 365. In questi casi, gli account utente possono trovarsi in foreste di Active Directory diverse e questo può rivelarsi problematico. Se ad esempio un utente degli Stati Uniti accede dall'Europa, il sistema deve essere in grado di riconoscere la relativa foresta e quindi associare la richiesta di accesso al pool appropriato.

Il servizio di individuazione automatica è stato introdotto nell'aggiornamento cumulativo per Lync Server di novembre 2011 per ovviare a questi problemi. Quando un'applicazione client tenta di accedere a Lync Server, il servizio di individuazione automatica analizza l'indirizzo SIP del client e quindi reindirizza la richiesta al pool appropriato. Le applicazioni client si connettono al servizio di individuazione automatica inviando una richiesta HTTP a un URL di individuazione automatica. Per il corretto funzionamento del servizio di individuazione automatica, è necessario che questi URL siano configurati dagli amministratori. Oltre a configurare gli URL, gli amministratori devono creare record DNS corrispondenti a tali URL.

Gli URL di individuazione automatica vengono assegnati alle impostazioni di configurazione del servizio di individuazione automatica. Queste impostazioni a loro volta possono essere applicate all'ambito globale o all'ambito del sito. Quando si installa Lync Server, viene creata automaticamente una raccolta globale di impostazioni. A tale raccolta tuttavia non viene assegnato alcun URL di individuazione automatica. Se una singola raccolta di impostazioni di individuazione automatica non soddisfa le proprie esigenze, è possibile utilizzare il cmdlet **New-CsAutoDiscoverConfiguration** per creare ulteriori impostazioni di configurazione nell'ambito del sito. Da tale posizione è possibile utilizzare il cmdlet **Set-CsAutoDiscoverConfiguration** per aggiungere o rimuovere gli URL di individuazione automatica dalla raccolta globale o da qualsiasi raccolta nell'ambito del sito.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsAutoDiscoverConfiguration** in locale: RTCUniversalServerAdmins.

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
<td><p><em>ExternalSipClientAccessFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo (FQDN) del server utilizzato per l'accesso dei client esterni.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExternalSipClientAccessPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Porta utilizzata per l'accesso dei client esterni.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per la raccolta di impostazioni di configurazione del servizio di individuazione automatica da modificare. Per modificare la raccolta globale, utilizzare la sintassi seguente:</p>
<p>-Identity &quot;global&quot;</p>
<p>Per modificare una raccolta configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>Se questo parametro non è specificato, il cmdlet <strong>Set-CsAutoDiscoverConfiguration</strong> modifica automaticamente le impostazioni globali.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto AutoDiscoverConfiguration</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
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

Il cmdlet **Set-CsAutoDiscoverConfiguration** accetta l'input da pipeline dell'oggetto Microsoft.Rtc.Management.WriteableConfig.Settings.AutoDiscoverConfiguration.AutoDiscoverConfiguration.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsAutoDiscoverConfiguration** modifica le istanze dell'oggetto Microsoft.Rtc.Management.WriteableConfig.Settings.AutoDiscoverConfiguration.AutoDiscoverConfiguration.

