---
title: Set-CsClsScenario
TOCTitle: Set-CsClsScenario
ms:assetid: 00de6571-a1ad-4f69-a21e-8a9ae115882f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204622(v=OCS.15)
ms:contentKeyID: 49299483
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsClsScenario

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di modificare uno scenario di configurazione della registrazione centralizzata. Uno scenario rappresenta una situazione o un componente particolare di Lync Server 2013, ad esempio la messaggistica istantanea e la presenza, che gli amministratori possono abilitare o disabilitare ai fini della traccia. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsClsScenario [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsClsScenario [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Provider <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

I comandi riportati nell'esempio 1 creano un nuovo provider di scenari di registrazione centralizzata e quindi aggiungono il provider allo scenario WAC configurato per il sito Redmond. A tal scopo, il primo comando dell'esempio utilizza il cmdlet **New-CsClsProvider** per creare un nuovo provider con il nome WebInfrastructure. Questo nuovo provider viene archiviato in una variabile denominata $provider. Il secondo comando dell'esempio aggiunge quindi il nuovo provider allo scenario site:Redmond/WAC. Poiché il comando utilizza la sintassi @{Add=$provider}, il nuovo provider verrà aggiunto allo scenario WAC oltre a tutti gli altri provider già configurati

    $provider = New-CsClsProvider -Name "WebInfrastructure" -Type "WPP" -Level "Warning" -Flags "All"
    
    Set-CsClsScenario -Identity "site:Redmond/WAC" -Provider @{Add=$provider}

## Esempio 2

Il comando dell'esempio 2 è una variante del comando dell'esempio 1. Nell'esempio 2, tuttavia, il nuovo provider sostituirà tutti gli altri eventuali provider esistenti configurati per lo scenario WAC. A tal scopo viene utilizzata la sintassi @{Replace=$provider}.

    $provider = New-CsClsProvider -Name "WebInfrastructure" -Type "WPP" -Level "Warning" -Flags "All"
    
    Set-CsClsScenario -Identity "site:Redmond/WAC" -Provider @{Replace=$provider}

## Descrizione dettagliata

Il servizio di registrazione centralizzata, che sostituisce gli strumenti OCSLogger e OCSTracer utilizzati in Microsoft Lync Server 2010, consente agli amministratori di gestire la registrazione e la traccia per tutti i computer e i pool che eseguono Lync Server 2013. La registrazione centralizzata consente agli amministratori di arrestare, avviare e configurare la registrazione per uno o più pool e computer utilizzando un solo comando. È ad esempio possibile utilizzare un comando per abilitare la registrazione del Servizio Rubrica in tutti i server della Rubrica. Questo comportamento è diverso rispetto agli strumenti OCSLogger e OCSTracer, che devono essere gestiti singolarmente (avviati e arrestati individualmente) in ogni server. Il servizio di registrazione centralizzata inoltre consente agli amministratori di eseguire ricerche nei log di traccia dal comando utilizzando l'interfaccia della riga di comando Windows PowerShell e il cmdlet [Search-CsClsLogging](search-csclslogging.md).

La registrazione centralizzata si basa su una serie di scenari predefiniti che offrono un metodo di registrazione più dettagliato rispetto alle versioni precedenti di Lync Server. Questi scenari predeterminano automaticamente i componenti del server e la registrazione. In questo modo, un amministratore che abilita lo scenario RGS avrà la certezza che verranno registrate solo le informazioni pertinenti per il servizio Response Group e non ad esempio per il servizio del provider di servizi di audioconferenza.

Personalizzare gli scenari utilizzando il cmdlet [New-CsClsScenario](new-csclsscenario.md) e aggiungendo quindi il nuovo scenario a una raccolta di impostazioni di configurazione della registrazione centralizzata. Gli scenari personalizzati possono quindi essere modificati utilizzando il cmdlet **Set-CsClsScenario**.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli del controllo di accesso basato sui ruoli creati personalmente), al prompt di Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsClsScenario"}

Pannello di controllo di Lync Server: le funzioni eseguite dal cmdlet **Set-CsClsScenario** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco dello scenario da modificare. Uno scenario è costituito da due parti: l'ambito in cui è configurato, ovvero la raccolta di impostazioni di configurazione della registrazione centralizzata in cui si trova lo scenario, e il nome. Ad esempio:</p>
<p>-Identity &quot;site:Redmond/AddressBook&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Consente di passare un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Provider</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Provider di registrazione per lo scenario. I nuovi provider devono essere creati utilizzando il cmdlet <strong>New-CsClsProvider</strong>. Ad esempio:</p>
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

Il cmdlet **Set-CsClsScenario** accetta le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Scenario\#Decorated inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsClsScenario** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Scenario\#Decorated.

