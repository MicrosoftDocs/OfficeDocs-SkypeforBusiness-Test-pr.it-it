---
title: Search-CsClsLogging
TOCTitle: Search-CsClsLogging
ms:assetid: a2eddada-a494-4bc6-b7d0-9b511dfc4ac1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619189(v=OCS.15)
ms:contentKeyID: 49301523
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Search-CsClsLogging

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Offre un'opzione della riga di comando per la ricerca nei file di log della registrazione centralizzata. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Search-CsClsLogging [-AsXml <SwitchParameter>] [-CallId <String>] [-Components <String[]>] [-Computers <String[]>] [-ConferenceId <String>] [-CorrelationIds <String[]>] [-EndTime <DateTime>] [-IP <IPAddress>] [-LogLevel <String>] [-MatchAll <SwitchParameter>] [-MatchAny <SwitchParameter>] [-OutputFilePath <String>] [-Phone <String>] [-Pools <String[]>] [-SipContents <String>] [-SkipNetworkLogs <SwitchParameter>] [-StartTime <DateTime>] [-Uri <String>]

## Esempi

## Esempio 1

Il comando mostrato nell'Esempio 1 cerca l'indirizzo IP 192.168.0.242 nei file di log disponibili nel computer atl-cs-001.litwareinc.com.

    Search-CsClsLogging -Computers "atl-cs-001.litwareinc.com" -IP "192.168.0.242"

## Esempio 2

Nell'Esempio 2 vengono cercate le voci che corrispondono sia all'indirizzo IP 192.168.0.242 che all'URI sip:kenmyer@litwareinc.com. Il parametro MatchAll specifica che devono essere soddisfatti tutti i criteri per poter registrare una voce come corrispondenza.

    Search-CsClsLogging -Computers "atl-cs-001.litwareinc.com" -IP "192.168.0.242" -Uri "sip:kenmyer@litwareinc.com" -MatchAll

## Esempio 3

Il comando mostrato nell'Esempio 3 cerca le voci che corrispondono all'indirizzo IP 192.168.0.242 o all'URI sip:kenmyer@litwareinc.com. Il parametro MatchAny specifica che è necessario soddisfare solo uno dei criteri per poter registrare una voce come corrispondenza.

    Search-CsClsLogging -Computers "atl-cs-001.litwareinc.com" -IP "192.168.0.242" -Uri "sip:kenmyer@litwareinc.com" -MatchAny

## Descrizione dettagliata

Il servizio di registrazione centralizzata, che sostituisce gli strumenti OCSLogger e OCSTracer utilizzati in Microsoft Lync Server 2010, consente agli amministratori di gestire la registrazione e la traccia per tutti i computer e i pool che eseguono Lync Server 2013. La registrazione centralizzata consente agli amministratori di arrestare, avviare e configurare la registrazione per uno o più pool e computer utilizzando un solo comando. È ad esempio possibile utilizzare un comando per abilitare la registrazione del servizio Rubrica in tutti i server della Rubrica. Questo comportamento è diverso rispetto agli strumenti OCSLogger e OCSTracer, che devono essere gestiti singolarmente (avviati e arrestati individualmente) in ogni server. Il servizio di registrazione centralizzata inoltre consente agli amministratori di eseguire ricerche nei log di traccia dal comando utilizzando l'interfaccia della riga di comando Windows PowerShell e il cmdlet [Search-CsClsLogging](search-csclslogging.md).

La registrazione centralizzata si basa su una serie di scenari predefiniti che offrono un approccio più mirato alla registrazione rispetto alle versioni precedenti di Lync Server. Tali scenari prevedono componenti server e registrazione predefiniti per l'utente e di conseguenza un amministratore che abilita lo scenario RGS può essere sicuro che registrerà solo informazioni dei log rilevanti per il servizio Response Group e non, ad esempio, per il servizio del provider di servizi di audioconferenza.

Il cmdlet **Search-CsClsLogging** offre un'opzione della riga di comando per la ricerca nei file di log generati dal servizio di registrazione centralizzata.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Search-CsClsLogging"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Search-CsClsLogging** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Se specificato, le informazioni sul codice restituito provenienti da ogni computer in cui è stata eseguita la ricerca vengono restituite in formato XML anziché come valore stringa.</p></td>
</tr>
<tr class="even">
<td><p><em>CallId</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Identificatore di chiamata da cercare.</p></td>
</tr>
<tr class="odd">
<td><p><em>Components</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String[]</p></td>
<td><p>Elenco di componenti separati da virgola in cui effettuare la ricerca.</p></td>
</tr>
<tr class="even">
<td><p><em>Computers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String[]</p></td>
<td><p>Elenco separato da virgola dei computer in cui effettuare la ricerca. Ad esempio:</p>
<p>-Computers &quot;server-cs-001.litwareinc.com&quot;, &quot;server-cs-002.litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>ConferenceId</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>ID di conferenza da cercare.</p></td>
</tr>
<tr class="even">
<td><p><em>CorrelationIds</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String[]</p></td>
<td><p>Elenco separato da virgola di ID di correlazione da cercare. Una correlazione è un numero intero a 32 bit associato a ogni richiesta.</p></td>
</tr>
<tr class="odd">
<td><p><em>EndTime</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.DateTime</p></td>
<td><p>Data e ora di fine della ricerca delle voci di log. Specificate nel fuso orario locale. Il valore predefinito è 5 minuti dopo l'ora corrente se StartTime non è stato specificato. In caso contrario, il valore predefinito è 30 minuti dopo StartTime. Ad esempio, sul computer che esegue la versione in lingua inglese di Lync Server 2013, questa sintassi limita la ricerca alle voci registrate prima delle 8:00 AM del 31 agosto 2012:</p>
<p>-StartTime &quot;8/31/2012 8:00AM&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>IP</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Net.IPAddress</p></td>
<td><p>Indirizzo IP da cercare. Deve essere un indirizzo IP effettivo e non può contenere caratteri jolly.</p></td>
</tr>
<tr class="odd">
<td><p><em>LogLevel</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Specifica il tipo minimo di voce di log da restituire. I valori consentiti sono:</p>
<p>* Fatal</p>
<p>* Error</p>
<p>* Warning</p>
<p>* Info</p>
<p>* Verbose</p>
<p>* Debug</p>
<p>* All</p>
<p>Per &quot;tipo minimo di voce di log da restituire&quot; si intende che il cmdlet <strong>Search-CsClsLogging</strong> restituirà tutte le voci di log al livello di gravità specificato, oltre a tutte le voci di log con un livello di gravità maggiore. Se ad esempio si imposta LogLevel su Warning, il cmdlet restituirà le voci contrassegnate come Fatal ed Error, nonché quelle contrassegnate come Warning.</p></td>
</tr>
<tr class="even">
<td><p><em>MatchAll</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Quando è presente, è necessario soddisfare tutti i criteri inclusi, come nel caso di una query AND in SQL Server.</p></td>
</tr>
<tr class="odd">
<td><p><em>MatchAny</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Quando è presente, è necessario soddisfare solo uno dei criteri inclusi, come nel caso di una query OR in SQL Server. Si tratta del valore predefinito.</p></td>
</tr>
<tr class="even">
<td><p><em>OutputFilePath</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Se presente, specifica il percorso completo in cui scrivere un file di testo contenente i risultati della ricerca. In caso contrario, vengono scritti nella console.</p></td>
</tr>
<tr class="odd">
<td><p><em>Phone</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Numero di telefono da cercare. Tale numero deve essere immesso utilizzando il formato E.164 e non deve includere caratteri jolly.</p></td>
</tr>
<tr class="even">
<td><p><em>Pools</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String[]</p></td>
<td><p>Elenco separato da virgole dei pool in cui effettuare la ricerca. Ad esempio:</p>
<p>-Pools &quot;atl-cs-001.litwareinc.com&quot;, &quot;red-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>SipContents</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Testo arbitrario da cercare nel corpo di un messaggio SIP.</p></td>
</tr>
<tr class="even">
<td><p><em>SkipNetworkLogs</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Quando è presente, indica al cmdlet <strong>Search-CsClsLogging</strong> di evitare la ricerca nei log di rete.</p></td>
</tr>
<tr class="odd">
<td><p><em>StartTime</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.DateTime</p></td>
<td><p>Data e ora di inizio della ricerca delle voci di log. Specificate nel fuso orario locale. Il valore predefinito è 30 minuti dopo EndTime. Ad esempio, sul computer che esegue la versione in lingua inglese di Lync Server 2013, questa sintassi limita la ricerca alle voci registrate alle 8:00 AM del 1 agosto 2012 o di una data successiva:</p>
<p>-StartTime &quot;8/1/2012 8:00AM&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Uri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URI da cercare.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Search-CsClsLogging** non accetta input tramite pipeline.

## Tipi restituiti

Valori stringa o XML.

## Vedere anche

#### Ulteriori risorse

[Show-CsClsLogging](show-csclslogging.md)  
[Start-CsClsLogging](start-csclslogging.md)  
[Stop-CsClsLogging](stop-csclslogging.md)  
[Sync-CsClsLogging](sync-csclslogging.md)  
[Update-CsClsLogging](update-csclslogging.md)

