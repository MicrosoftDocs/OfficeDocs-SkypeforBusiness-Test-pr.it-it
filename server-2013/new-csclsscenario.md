---
title: New-CsClsScenario
TOCTitle: New-CsClsScenario
ms:assetid: 79ff443f-82ff-4b49-bde5-98e51e8b1ed2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205022(v=OCS.15)
ms:contentKeyID: 49301061
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClsScenario

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo scenario di configurazione della registrazione centralizzata. Uno scenario rappresenta una situazione o un componente particolare di Lync Server 2013, ad esempio la messaggistica istantanea e la presenza, che gli amministratori possono abilitare o disabilitare ai fini della traccia. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    New-CsClsScenario -Identity <XdsIdentity> <COMMON PARAMETERS>

    New-CsClsScenario -Name <String> -Parent <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Provider <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

I comandi riportati nell'esempio 1 creano un nuovo scenario di registrazione centralizzata con identità (Identity) global/RedmondHybridVoice. A tale scopo, il primo comando dell'esempio utilizza il cmdlet **New-CsClsProvider** per creare un provider da assegnare allo scenario. Tale nuovo provider viene archiviato nella variabile $provider.

Dopo la creazione della descrizione e del provider, il comando finale dell'esempio chiama il cmdlet **New-CsClsScenario** per creare lo scenario, utilizzando i dati archiviati in $provider per assegnare un valore alla proprietà Provider.

    $provider = New-CsClsProvider -Name "RedmondHybridVoice" -Type "WPP" -Level "Info" -Flags "All"
    
    New-CsClsScenario -Identity "global/RedmondHybridVoice"-Provider $provider

## Descrizione dettagliata

Il servizio di registrazione centralizzata, che sostituisce gli strumenti OCSLogger e OCSTracer utilizzati in Microsoft Lync Server 2010, consente agli amministratori di gestire la registrazione e la traccia per tutti i computer e i pool che eseguono Lync Server 2013. La registrazione centralizzata consente agli amministratori di arrestare, avviare e configurare la registrazione per uno o più pool e computer utilizzando un solo comando. È ad esempio possibile utilizzare un comando per abilitare la registrazione del servizio Rubrica in tutti i server della Rubrica. Questo comportamento è diverso rispetto agli strumenti OCSLogger e OCSTracer, che devono essere gestiti singolarmente (avviati e arrestati individualmente) in ogni server. Il servizio di registrazione centralizzata inoltre consente agli amministratori di eseguire ricerche nei log di traccia dal comando utilizzando l'interfaccia della riga di comando Windows PowerShell e il cmdlet [Search-CsClsLogging](search-csclslogging.md).

La registrazione centralizzata si basa su una serie di scenari predefiniti che offrono un metodo di registrazione più dettagliato rispetto alle versioni precedenti di Lync Server. Questi scenari predeterminano automaticamente i componenti del server e la registrazione. In questo modo, un amministratore che abilita lo scenario RGS avrà la certezza che verranno registrate solo le informazioni pertinenti per il servizio Response Group e non ad esempio per il servizio del provider di servizi di audioconferenza.

Gli scenari personalizzati possono essere creati utilizzando il cmdlet New-CsClsScenario e aggiungendo quindi il nuovo scenario a una raccolta di impostazioni di configurazione della registrazione centralizzata.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt di Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClsScenario"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **New-CsClsScenario** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Identificatore univoco del nuovo scenario. Uno scenario è costituito da due parti: l'ambito in cui lo scenario viene configurato, ovvero la raccolta di impostazioni di configurazione della registrazione centralizzata in cui è disponibile lo scenario, e il nome dello scenario stesso. Ad esempio:</p>
<p>-Identity &quot;site:Redmond/AddressBook&quot;</p>
<p>Se si utilizza il parametro Identity, non sarà possibile utilizzare il parametro Name o il parametro Parent nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome univoco del nuovo scenario. Ad esempio:</p>
<p>-Name &quot;RedmondHybridVoice&quot;</p>
<p>Se si utilizza il parametro Name, sarà inoltre necessario specificare il parametro Parent. Non utilizzare tuttavia il parametro Identity nello stesso comando dei parametri Name e Parent.</p></td>
</tr>
<tr class="odd">
<td><p><em>Parent</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Ambito delle impostazioni di configurazione della registrazione centralizzata in cui verrà inserito il nuovo scenario. Ad esempio, per aggiungere il nuovo scenario alle impostazioni globali, utilizzare la sintassi seguente:</p>
<p>-Parent &quot;global&quot;</p>
<p>È possibile restituire le identità di tutti gli &quot;elementi padre&quot; di registrazione centralizzata utilizzando il comando seguente:</p>
<p>Get-CsClsConfiguration | Select-Object Identity</p>
<p>Se si utilizza il parametro Name, sarà inoltre necessario specificare il parametro Parent. Non utilizzare tuttavia il parametro Identity nello stesso comando dei parametri Name e Parent.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>Provider</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Provider di registrazione per lo scenario. I nuovi provider devono essere creati utilizzando il cmdlet New-CsClsProvider, ad esempio:</p>
<p>$provider = New-CsClsProvider –Name &quot;UserServices&quot; –Type &quot;WPP&quot; –Level &quot;Info&quot; –Flags &quot;All&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsClsScenario** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **New-CsClsScenario** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Scenario\#Decorated.

