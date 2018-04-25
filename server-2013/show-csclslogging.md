---
title: Show-CsClsLogging
TOCTitle: Show-CsClsLogging
ms:assetid: 19b2de51-5c14-4a8b-97e5-573c3285b174
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619173(v=OCS.15)
ms:contentKeyID: 49299827
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Show-CsClsLogging

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Visualizza lo stato corrente del servizio di registrazione centralizzata. In altri termini, mostra gli scenari di registrazione centralizzata attualmente attivi. La registrazione centralizzata consente agli amministratori di abilitare o disabilitare la traccia di Lync Server 2013 su più computer contemporaneamente. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Show-CsClsLogging [-AsXml <SwitchParameter>] [-Computers <String[]>] [-Pools <String[]>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce informazioni sugli scenari in corso di registrazione in tutti i computer della topologia.

    Show-CsClsLogging

## Esempio 2

Nell'esempio 2 vengono restituite informazioni di registrazione per tutti i server del pool atl-cs-001…litwareinc.com…

    Show-CsClsLogging -Pools "atl-cs-001.litwareinc.com"

## Descrizione dettagliata

Il servizio di registrazione centralizzata, che sostituisce gli strumenti OCSLogger e OCSTracer utilizzati in Microsoft Lync Server 2010, consente agli amministratori di gestire la registrazione e la traccia per tutti i computer e i pool che eseguono Lync Server 2013. La registrazione centralizzata consente agli amministratori di arrestare, avviare e configurare la registrazione per uno o più pool e computer utilizzando un solo comando. È ad esempio possibile utilizzare un comando per abilitare la registrazione del Servizio Rubrica in tutti i server della Rubrica. Questo comportamento è diverso rispetto agli strumenti OCSLogger e OCSTracer, che devono essere gestiti singolarmente (avviati e arrestati individualmente) in ogni server. Il servizio di registrazione centralizzata inoltre consente agli amministratori di eseguire ricerche nei log di traccia dal comando utilizzando l'interfaccia della riga di comando Windows PowerShell e il cmdlet [Search-CsClsLogging](search-csclslogging.md).

La registrazione centralizzata si basa su una serie di scenari predefiniti che assicurano un approccio alla registrazione più mirato di quello garantito dalle precedenti versioni di Lync Server. Questi scenari predeterminano i componenti server e la registrazione e quindi un amministratore che abiliti lo scenario RGS può star certo che registrerà solo le informazioni attinenti al Response Group Service e non quelle concernenti, ad esempio, il servizio provider di servizi di audioconferenza.

È inoltre possibile definire scenari personalizzati utilizzando il cmdlet [New-CsClsScenario](new-csclsscenario.md).

Il cmdlet **Show-CsClsLogging** restituisce informazioni su tutti gli scenari attualmente sottoposti a registrazione in un computer o in una serie di computer. Queste informazioni includono il nome e la durata di ogni scenario attivo, oltre a data e ora di avvio della registrazione.

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
<td><p><em>AsXml</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se specificato, le informazioni vengono restituite in XML.</p></td>
</tr>
<tr class="even">
<td><p><em>Computers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String[]</p></td>
<td><p>Consente agli amministratori di restituire informazioni di registrazione da un server specifico o una serie di server. Per restituire informazioni da un solo server, specificare il nome di dominio completo del server in questione. Ad esempio:</p>
<p>-Computers &quot;atl-server-001.litwareinc.com&quot;</p>
<p>È possibile specificare più server separando i nomi di dominio completi (FQDN) dei computer con virgole:</p>
<p>-Computers &quot;atl-server-001.litwareinc.com&quot;,&quot;red-server-002.litwareinc.com&quot;</p>
<p>Se non si include il parametro Computers o Pools, il cmdlet <strong>Show-CsClsLogging</strong> visualizzerà lo stato di tutti i computer della topologia.</p></td>
</tr>
<tr class="odd">
<td><p><em>Pools</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String[]</p></td>
<td><p>Consente agli amministratori di restituire informazioni di registrazione per ogni server di un pool. Per restituire informazioni per un pool, specificare il nome di dominio completo del pool. Ad esempio:</p>
<p>-Pools &quot;atl-cs-001.litwareinc.com&quot;</p>
<p>È possibile specificare più pool separando i relativi nomi di dominio completi (FQDN) con virgole:</p>
<p>-Pools &quot;atl-cs-001.litwareinc.com&quot;,&quot;red-cs-002.litwareinc.com&quot;</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Show-CsClsLogging** non accetta input da pipeline.

## Tipi restituiti

Valore stringa o output XML. Il cmdlet **Show-CsClsLogging** non restituisce oggetti.

## Vedere anche

#### Ulteriori risorse

[Search-CsClsLogging](search-csclslogging.md)  
[Start-CsClsLogging](start-csclslogging.md)  
[Stop-CsClsLogging](stop-csclslogging.md)  
[Sync-CsClsLogging](sync-csclslogging.md)  
[Update-CsClsLogging](update-csclslogging.md)

