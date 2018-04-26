---
title: Sync-CsClsLogging
TOCTitle: Sync-CsClsLogging
ms:assetid: 0df996b7-1834-42f1-84e5-346ba74631e7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619169(v=OCS.15)
ms:contentKeyID: 49299676
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Sync-CsClsLogging

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Scarica la cache del servizio di registrazione centralizzata. La registrazione centralizzata consente agli amministratori di abilitare o disabilitare simultaneamente la traccia di Lync Server 2013 in più computer. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Sync-CsClsLogging [-AsXml <SwitchParameter>] [-Computers <String[]>] [-Pools <String[]>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 scarica le cache di registrazione centralizzata in tutti i server della topologia.

    Sync-CsClsLogging 

## Esempio 2

Nell'esempio 2, le cache di registrazione centralizzata vengono scaricate in tutti i server del pool atl-cs-001.litwareinc.com.

    Sync-CsClsLogging -Pools "atl-cs-001.litwareinc.com"

## Descrizione dettagliata

Il servizio di registrazione centralizzata, che sostituisce gli strumenti OCSLogger e OCSTracer utilizzati in Microsoft Lync Server 2010, consente agli amministratori di gestire la registrazione e la traccia per tutti i computer e i pool che eseguono Lync Server 2013. La registrazione centralizzata consente agli amministratori di arrestare, avviare e configurare la registrazione per uno o più pool e computer utilizzando un solo comando. È ad esempio possibile utilizzare un comando per abilitare la registrazione del Servizio Rubrica in tutti i server della Rubrica. Questo comportamento è diverso rispetto agli strumenti OCSLogger e OCSTracer, che devono essere gestiti singolarmente (avviati e arrestati individualmente) in ogni server. Il servizio di registrazione centralizzata inoltre consente agli amministratori di eseguire ricerche nei log di traccia dal comando utilizzando l'interfaccia della riga di comando Windows PowerShell e il cmdlet [Search-CsClsLogging](search-csclslogging.md).

La registrazione centralizzata si basa su una serie di scenari predefiniti che assicurano un approccio alla registrazione più mirato di quello garantito dalle precedenti versioni di Lync Server. Questi scenari predeterminano i componenti server e la registrazione e quindi un amministratore che abiliti lo scenario RGS può star certo che registrerà solo le informazioni attinenti al Response Group Service e non quelle concernenti, ad esempio, il servizio provider di servizi di audioconferenza.

È inoltre possibile definire scenari personalizzati utilizzando il cmdlet [New-CsClsScenario](new-csclsscenario.md).

Quando viene registrato uno scenario, il servizio mantiene i dati in memoria e quindi li scrive periodicamente sul disco. Gli amministratori possono tuttavia eseguire in qualsiasi momento il cmdlet **Sync-CsClsLogging** per "scaricare" la cache dei dati. Quando viene eseguita questa operazione, tutti i dati di registrazione attualmente in memoria vengono scritti sul disco, le cache dei dati vengono cancellate e i file di log diventano disponibili per la ricerca.

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
<td><p>Consente agli amministratori di scaricare la cache del servizio di registrazione centralizzata in un server specifico o una serie di server. Per scaricare la cache di un solo server, specificare il nome di dominio completo del server in questione. Ad esempio:</p>
<p>-Computers &quot;atl-server-001.litwareinc.com&quot;</p>
<p>È possibile specificare più server separando i nomi di dominio completi (FQDN) dei computer con virgole:</p>
<p>-Computers &quot;atl-server-001.litwareinc.com&quot;,&quot;red-server-002.litwareinc.com&quot;</p>
<p>Se non si include il parametro Computers o Pools, il cmdlet <strong>Sync-CsClsLogging</strong> applicherà il comando a tutti i pool della topologia.</p></td>
</tr>
<tr class="odd">
<td><p><em>Pools</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String[]</p></td>
<td><p>Consente agli amministratori di scaricare la cache del servizio di registrazione centralizzata in ogni server di un pool. Per scaricare le cache dei server di un pool, specificare il nome di dominio completo del pool. Ad esempio:</p>
<p>-Pools &quot;atl-cs-001.litwareinc.com&quot;</p>
<p>È possibile specificare più pool separando i relativi nomi di dominio completi (FQDN) con virgole:</p>
<p>-Pools &quot;atl-cs-001.litwareinc.com&quot;,&quot;red-cs-002.litwareinc.com&quot;</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Sync-CsClsLogging** non accetta input da pipeline.

## Tipi restituiti

Valore stringa. Il cmdlet **Sync-CsClsLogging** non restituisce oggetti.

## Vedere anche

#### Ulteriori risorse

[Search-CsClsLogging](search-csclslogging.md)  
[Show-CsClsLogging](show-csclslogging.md)  
[Start-CsClsLogging](start-csclslogging.md)  
[Stop-CsClsLogging](stop-csclslogging.md)  
[Update-CsClsLogging](update-csclslogging.md)

