---
title: Configurazione di un nodo Watcher per l'esecuzione di transazioni sintetiche
TOCTitle: Configurazione di un nodo Watcher per l'esecuzione di transazioni sintetiche
ms:assetid: cedda508-8881-4079-88d5-49798f342ddf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205314(v=OCS.15)
ms:contentKeyID: 49302007
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione di un nodo Watcher per l'esecuzione di transazioni sintetiche

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Dopo l'installazione dei file dell'agente System Center, è necessario configurare il nodo Watcher vero e proprio. Le operazioni da eseguire per configurare un nodo Watcher variano a seconda che il computer del nodo Watcher si trovi all'interno o all'esterno della rete perimetrale.

Quando si configura un nodo Watcher, è inoltre necessario scegliere il tipo di metodo di autenticazione che deve essere utilizzato dal nodo. Lync Server 2013 consente di scegliere uno dei due metodi di autenticazione seguenti: server attendibile o autenticazione basata sulle credenziali. Le differenze tra questi due metodi sono descritte nella tabella seguente:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Configurazione</th>
<th>Descrizione</th>
<th>Posizioni supportate</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Server attendibile</p></td>
<td><p>Viene utilizzato un certificato per rappresentare un server interno ed evitare le difficoltà dell'autenticazione.</p>
<p>È utile per gli amministratori che preferiscono gestire un singolo certificato anziché numerose password utente in ogni nodo Watcher.</p></td>
<td><p>All'interno dell'organizzazione.</p>
<p>Si noti che con questo metodo il nodo Watcher deve trovarsi nello stesso dominio dei pool monitorati. Se il nodo Watcher e i pool monitorati si trovano in domini diversi, utilizzare l'autenticazione basata sulle credenziali.</p></td>
</tr>
<tr class="even">
<td><p>Autenticazione basata sulle credenziali</p></td>
<td><p>I nomi e le password utente vengono archiviati in modo sicuro in Gestione credenziali di Windows.</p>
<p>Questa modalità richiede maggiori attività di gestione delle password, ma è l'unica opzione per i nodi Watcher posizionati all'esterno dell'organizzazione. Questi nodi Watcher non possono essere gestiti come endpoint attendibile per l'autenticazione.</p></td>
<td><p>All'esterno dell'organizzazione.</p>
<p>All'interno dell'organizzazione.</p></td>
</tr>
</tbody>
</table>


È inoltre consigliabile verificare che per nel firewall siano presenti regole connessioni in entrata per both MonitoringHost.exe e PowerShell.exe. Se tali processi sono bloccati dal firewall, le transazioni sintetiche non riusciranno e verrà restituito un errore 504 (timeout del server).

