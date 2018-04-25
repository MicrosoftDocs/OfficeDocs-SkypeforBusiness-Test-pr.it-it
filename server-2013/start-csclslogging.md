---
title: Start-CsClsLogging
TOCTitle: Start-CsClsLogging
ms:assetid: cac15f5a-5a0c-4b3c-9bef-bb4fd44005b2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619190(v=OCS.15)
ms:contentKeyID: 49301961
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Start-CsClsLogging

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Avvia lo scenario del servizio di registrazione centralizzata specificato. La registrazione centralizzata consente agli amministratori di abilitare o disabilitare contemporaneamente la traccia di Lync Server 2013 su più computer. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Start-CsClsLogging -Scenario <String> [-AsXml <SwitchParameter>] [-Computers <String[]>] [-Duration <String>] [-Pools <String[]>]

## Esempi

## Esempio 1

Nell'esempio 1 viene avviata la registrazione dello scenario AlwaysOn su tutti i computer della topologia corrente.

    Start-CsClsLogging -Scenario "AlwaysOn"

## Esempio 2

Il comando mostrato nell'esempio 2 avvia la registrazione CPS su tutti i computer inclusi nel pool atl-cs-001.litwareinc.com con una durata di 12 ore.

    Start-CsClsLogging -Scenario "cps" -Pools "atl-cs-001.litwareinc.com" -Duration 12:0

## Descrizione dettagliata

Il servizio di registrazione centralizzata (che sostituisce gli strumenti OCSLogger e OCSTracer utilizzati in Microsoft Lync Server 2010) consente agli amministratori di gestire la registrazione e la traccia per tutti i computer e i pool che eseguono Lync Server 2013. Grazie alla registrazione centralizzata, gli amministratori possono arrestare, avviare e configurare la registrazione per uno o più pool e computer utilizzando un singolo comando. È ad esempio possibile utilizzare un comando per abilitare la registrazione del servizio Rubrica su tutti i server Rubrica. Ciò rappresenta una differenza rispetto agli strumenti OCSLogger e OCSTracer che devono essere gestiti, e persino arrestati e avviati, singolarmente in ogni server. Il servizio di registrazione centralizzata consente inoltre agli amministratori di effettuare ricerche nei log di traccia tramite il comando, utilizzando l'interfaccia della riga di comando Windows PowerShell e il cmdlet [Search-CsClsLogging](search-csclslogging.md).

La registrazione centralizzata si basa su una serie di scenari predefiniti che offrono un approccio più mirato alla registrazione rispetto alle versioni precedenti di Lync Server. Tali scenari prevedono componenti server e registrazione predefiniti per l'utente e di conseguenza un amministratore che abilita lo scenario RGS può essere sicuro che registrerà solo informazioni dei log rilevanti per il servizio Response Group e non, ad esempio, per il servizio del provider di servizi di audioconferenza.

È anche possibile definire scenari personalizzati utilizzando il cmdlet [New-CsClsScenario](new-csclsscenario.md).

Il cmdlet **Start-CsClsLogging** consente agli amministratori di avviare la registrazione di uno scenario specificato su un computer o su un set di computer. Per impostazione predefinita, tale operazione di registrazione continuerà fino alla scadenza del limite di tempo Duration. Gli amministratori possono tuttavia arrestare un'operazione di registrazione in qualsiasi momento utilizzando il cmdlet [Stop-CsClsLogging](stop-csclslogging.md).

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
<td><p>Nome dello scenario di registrazione centralizzato da avviare. Gli scenari disponibili (e i relativi nomi) possono essere restituiti utilizzando il comando seguente:</p>
<p>Get-CsClsScenario | Select-Object Name</p>
<p>Si noti che è possibile specificare un solo scenario per chiamata nel cmdlet <strong>Start-CsClsLogging</strong>. È inoltre possibile avviare in un computer un solo scenario in qualsiasi momento, oltre allo scenario AlwaysOn.</p></td>
</tr>
<tr class="even">
<td><p><em>AsXml</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Quando viene specificato, le informazioni vengono restituite mediante XML.</p></td>
</tr>
<tr class="odd">
<td><p><em>Computers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String[]</p></td>
<td><p>Consente agli amministratori di avviare la registrazione su un server o su un set di server specificato. Per avviare la registrazione su un singolo server, specificarne il nome di dominio completo. Ad esempio:</p>
<p>-Computers &quot;atl-server-001.litwareinc.com&quot;</p>
<p>È possibile specificare più server separando con una virgola i nomi di dominio completi dei computer:</p>
<p>-Computers &quot;atl-server-001.litwareinc.com&quot;,&quot;red-server-002.litwareinc.com&quot;</p>
<p>Se non si include il parametro Computers o il parametro Pools, il cmdlet <strong>Start-CsClsLogging</strong> verrà automaticamente eseguito in tutti i computer della topologia.</p></td>
</tr>
<tr class="even">
<td><p><em>Duration</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Intervallo di tempo per l'esecuzione dell'operazione di registrazione. Specificando la sintassi seguente, ad esempio, l'operazione di registrazione viene eseguita per 2 ore (0 giorni.02 ore:00 minuti) e quindi arrestata:</p>
<p>-Duration 0.02:00</p>
<p>La sintassi seguente specifica una durata di 3 ore e 15 minuti:</p>
<p>-Duration 0.03:15</p>
<p>La sintassi seguente specifica una durata di 6 giorni, 5 ore e 12 minuti:</p>
<p>-Duration 6.05:12</p>
<p>Il valore predefinito è 4 ore (04:00).</p></td>
</tr>
<tr class="odd">
<td><p><em>Pools</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String[]</p></td>
<td><p>Consente agli amministratori di avviare la registrazione di uno scenario su ogni server incluso in un pool. Per avviare la registrazione in un pool, specificarne il nome di dominio completo. Ad esempio:</p>
<p>-Pools &quot;atl-cs-001.litwareinc.com&quot;</p>
<p>È possibile specificare più pool separandone con una virgola il nome di dominio completo:</p>
<p>-Pools &quot;atl-cs-001.litwareinc.com&quot;,&quot;red-cs-002.litwareinc.com&quot;</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Start-CsClsLogging** non accetta input inviato tramite pipeline.

## Tipi restituiti

Valore stringa o output XML. Il cmdlet **Start-CsClsLogging** non restituisce oggetti.

## Vedere anche

#### Ulteriori risorse

[Search-CsClsLogging](search-csclslogging.md)  
[Show-CsClsLogging](show-csclslogging.md)  
[Stop-CsClsLogging](stop-csclslogging.md)  
[Sync-CsClsLogging](sync-csclslogging.md)  
[Update-CsClsLogging](update-csclslogging.md)

