---
title: Stop-CsClsLogging
TOCTitle: Stop-CsClsLogging
ms:assetid: 63d0f0d6-5eec-4a16-b834-37611c584f52
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619180(v=OCS.15)
ms:contentKeyID: 49300779
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Stop-CsClsLogging

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Interrompe lo scenario del servizio di registrazione centralizzata specificato. La registrazione centralizzata consente agli amministratori di abilitare o disabilitare simultaneamente la traccia diLync Server 2013 in più computer. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Stop-CsClsLogging -Scenario <String> [-AsXml <SwitchParameter>] [-Computers <String[]>] [-Pools <String[]>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 interrompe lo scenario di registrazione CPS su tutti i server della topologia.

    Stop-CsClsLogging -Scenario "cps"

## Esempio 2

Nell'esempio 2, lo scenario di registrazione CPS viene interrotto su tutti i server del pool atl-cs-001.litwareinc.com.

    Stop-CsClsLogging -Scenario "cps" -Pools "atl-cs-001.litwareinc.com"

## Descrizione dettagliata

Il servizio di registrazione centralizzata, che sostituisce gli strumenti OCSLogger e OCSTracer utilizzati in Microsoft Lync Server 2010, consente agli amministratori di gestire le funzioni di registrazione e traccia per tutti i computer e i pool che eseguono Lync Server 2013. Il servizio consente infatti di interrompere, avviare e configurare la registrazione per uno o più pool e computer con un solo comando. È ad esempio possibile utilizzare un comando per abilitare la registrazione del servizio Rubrica in tutti i server della Rubrica. Questa procedura non è invece eseguibile con gli strumenti OCSLogger e OCSTracer, che devono essere gestiti singolarmente (e anche arrestati e avviati singolarmente) in ogni server. Il servizio di registrazione centralizzata inoltre consente agli amministratori di eseguire ricerche nei log di traccia dal comando utilizzando l'interfaccia della riga di comando Windows PowerShell e il cmdlet [Search-CsClsLogging](search-csclslogging.md).

La registrazione centralizzata si basa su una serie di scenari predefiniti che assicurano un approccio alla registrazione più mirato di quello garantito dalle precedenti versioni diLync Server. Questi scenari predeterminano i componenti server e la registrazione e quindi un amministratore che abiliti lo scenario RGS può star certo che registrerà solo le informazioni attinenti al Response Group Service e non quelle concernenti, ad esempio, il servizio provider di servizi di audioconferenza.

È inoltre possibile definire scenari personalizzati usando il cmdlet [New-CsClsScenario](new-csclsscenario.md).

Il cmdlet [Start-CsClsLogging](start-csclslogging.md)consente agli amministratori di avviare la registrazione di un determinato scenario in un computer o in una serie di computer. Per impostazione predefinita, l'operazione di registrazione continuerà a essere eseguita fino alla scadenza della durata. Gli amministratori possono comunque interrompere manualmente un'operazione di registrazione in qualsiasi momento mediante il cmdlet **Stop-CsClsLogging**.

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
<td><p><em>Scenario</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome dello scenario di registrazione centralizzata da interrompere. Gli scenari disponibili, e i relativi nomi, possono essere restituiti tramite il seguente comando:</p>
<p>Get-CsClsScenario | Select-Object Name</p></td>
</tr>
<tr class="even">
<td><p><em>AsXml</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se specificato, le informazioni vengono restituite in XML.</p></td>
</tr>
<tr class="odd">
<td><p><em>Computers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String[]</p></td>
<td><p>Consente agli amministratori di interrompere la registrazione in un determinato server o in una serie di server. Per interrompere la registrazione in un solo server, specificare il nome di dominio completo del server in questione. Ad esempio:</p>
<p>-Computers &quot;atl-server-001.litwareinc.com&quot;</p>
<p>È possibile specificare più server separando i nomi di dominio completi (FQDN) dei computer con virgole:</p>
<p>-Computers &quot;atl-server-001.litwareinc.com&quot;,&quot;red-server-002.litwareinc.com&quot;</p>
<p>Se non si include il parametro Computers o Pools, il cmdlet <strong>Stop-CsClsLogging</strong> eseguirà il comando per tutti i pool della topologia.</p></td>
</tr>
<tr class="even">
<td><p><em>Pools</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String[]</p></td>
<td><p>Consente agli amministratori di interrompere la registrazione in ogni server di un pool. Per interrompere la registrazione in un pool, specificare il nome di dominio completo del pool in questione. Ad esempio:</p>
<p>-Pools &quot;atl-cs-001.litwareinc.com&quot;</p>
<p>È possibile specificare più pool separando i relativi nomi di dominio completi (FQDN) con virgole:</p>
<p>-Pools &quot;atl-cs-001.litwareinc.com&quot;,&quot;red-cs-002.litwareinc.com&quot;</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Stop-CsClsLogging** non accetta input da pipeline.

## Tipi restituiti

Valore stringa oppure output XML. Il cmdlet **Stop-CsClsLogging** non restituisce oggetti.

## Vedere anche

#### Ulteriori risorse

[Search-CsClsLogging](search-csclslogging.md)  
[Show-CsClsLogging](show-csclslogging.md)  
[Start-CsClsLogging](start-csclslogging.md)  
[Sync-CsClsLogging](sync-csclslogging.md)  
[Update-CsClsLogging](update-csclslogging.md)

