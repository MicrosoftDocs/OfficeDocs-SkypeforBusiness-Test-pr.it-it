---
title: Update-CsClsLogging
TOCTitle: Update-CsClsLogging
ms:assetid: 104ecc02-789d-4538-8203-0451448d4301
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619170(v=OCS.15)
ms:contentKeyID: 49299707
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Update-CsClsLogging

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Aggiorna la durata di tutti gli scenari di registrazione centralizzata attivi. La registrazione centralizzata consente agli amministratori di abilitare o disabilitare simultaneamente la traccia di Lync Server 2013 in più computer. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Update-CsClsLogging -Duration <String> [-AsXml <SwitchParameter>] [-Computers <String[]>] [-Pools <String[]>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 modifica la durata della registrazione per i server della topologia. In questo esempio, la durata è impostata su un'ora (60 minuti).

    Update-CsClsLogging -Duration 60

## Esempio 2

Nell'esempio 2, la durata viene modificata per tutti i server del pool atl-cs-001.litwareinc.com.

    Update-CsClsLogging -Duration 60 -Pools "atl-cs-001.litwareinc.com"

## Descrizione dettagliata

Il servizio di registrazione centralizzata, che sostituisce gli strumenti OCSLogger e OCSTracer utilizzati in Microsoft Lync Server 2010, consente agli amministratori di gestire la registrazione e la traccia per tutti i computer e i pool che eseguono Lync Server 2013. La registrazione centralizzata consente agli amministratori di arrestare, avviare e configurare la registrazione per uno o più pool e computer utilizzando un solo comando. È ad esempio possibile utilizzare un comando per abilitare la registrazione del Servizio Rubrica in tutti i server della Rubrica. Questo comportamento è diverso rispetto agli strumenti OCSLogger e OCSTracer, che devono essere gestiti singolarmente (avviati e arrestati individualmente) in ogni server. Il servizio di registrazione centralizzata inoltre consente agli amministratori di eseguire ricerche nei log di traccia dal comando utilizzando l'interfaccia della riga di comando Windows PowerShell e il cmdlet [Search-CsClsLogging](search-csclslogging.md).

La registrazione centralizzata si basa su una serie di scenari predefiniti che assicurano un approccio alla registrazione più mirato di quello garantito dalle precedenti versioni di Lync Server. Questi scenari predeterminano i componenti server e la registrazione e quindi un amministratore che abiliti lo scenario RGS può star certo che registrerà solo le informazioni attinenti al Response Group Service e non quelle concernenti, ad esempio, il servizio provider di servizi di audioconferenza.

È inoltre possibile definire scenari personalizzati utilizzando il cmdlet [New-CsClsScenario](new-csclsscenario.md).

Per impostazione predefinita, le operazioni di registrazione vengono eseguite per 4 ore (240 minuti) prima dell'interruzione automatica. Gli amministratori possono però specificare una durata diversa quando avviano la registrazione. Utilizzando il cmdlet **Update-CsClsLogging**, possono inoltre modificare la durata per tutti gli scenari attualmente sottoposti a registrazione.

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
<td><p><em>Duration</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Intervallo di esecuzione dell'operazione di registrazione. Questa sintassi fa sì, ad esempio, che l'operazione di registrazione venga eseguita per 2 ore (120 minuti) e quindi si interrompa:</p>
<p>-Duration 120</p>
<p>La sintassi seguente specifica una durata di 3 ore e 15 minuti:</p>
<p>-Duration 3:15</p>
<p>La sintassi seguente specifica una durata di 6 giorni, 5 ore e 12 minuti:</p>
<p>-Duration 6.5:12</p>
<p>Il valore predefinito è 30 minuti.</p></td>
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
<td><p>Consente agli amministratori di aggiornare il servizio di registrazione centralizzata in un server specifico o una serie di server. Per aggiornare un solo server, specificare il nome di dominio completo del server in questione. Ad esempio:</p>
<p>-Computers &quot;atl-server-001.litwareinc.com&quot;</p>
<p>È possibile specificare più server separando i nomi di dominio completi (FQDN) dei computer con virgole:</p>
<p>-Computers &quot;atl-server-001.litwareinc.com&quot;,&quot;red-server-002.litwareinc.com&quot;</p>
<p>Se non si include il parametro Computers o Pools, Update-CsClsLogging verrà eseguito automaticamente su tutti i computer della topologia.</p></td>
</tr>
<tr class="even">
<td><p><em>Pools</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String[]</p></td>
<td><p>Consente agli amministratori di aggiornare il servizio di registrazione centralizzata su ogni server di un pool. Per aggiornare i server di un pool, specificare il nome di dominio completo del pool. Ad esempio:</p>
<p>-Pools &quot;atl-cs-001.litwareinc.com&quot;</p>
<p>È possibile specificare più pool separando i relativi nomi di dominio completi (FQDN) con virgole:</p>
<p>-Pools &quot;atl-cs-001.litwareinc.com&quot;,&quot;red-cs-002.litwareinc.com&quot;</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Update-CsClsLogging** non accetta input da pipeline.

## Tipi restituiti

Valore stringa.

## Vedere anche

#### Ulteriori risorse

[Search-CsClsLogging](search-csclslogging.md)  
[Show-CsClsLogging](show-csclslogging.md)  
[Start-CsClsLogging](start-csclslogging.md)  
[Stop-CsClsLogging](stop-csclslogging.md)  
[Sync-CsClsLogging](sync-csclslogging.md)

