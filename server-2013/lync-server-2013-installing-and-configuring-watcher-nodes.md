---
title: Installazione e configurazione dei nodi Watcher
TOCTitle: Installazione e configurazione dei nodi Watcher
ms:assetid: 61f6deea-e3ef-4468-9be8-a65705815ebb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204943(v=OCS.15)
ms:contentKeyID: 49300757
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Installazione e configurazione dei nodi Watcher

 

_**Ultima modifica dell'argomento:** 2015-03-09_

I *nodi Watcher* sono computer che eseguono periodicamente transazioni sintetiche di Lync Server. Le *transazioni sintetiche* sono cmdlet di Windows PowerShell che verificano il corretto funzionamento previsto per scenari chiave per gli utenti finali, come la possibilità di accedere al sistema o la possibilità di scambiarsi messaggi istantanei. Per Lync Server 2013, System Center Operations Manager consente l'esecuzione delle transazioni sintetiche descritte nella tabella seguente. Esistono tre tipi diversi di transazioni sintetiche:

  - **Predefinite**. Queste sono le transazioni sintetiche eseguite per impostazione predefinita da un nodo Watcher. Quando si crea un nuovo nodo Watcher esiste la possibilità di specificare quali transazioni sintetiche verranno eseguite dal nodo. (Questo è lo scopo del parametro Tests utilizzato dal cmdlet **New-CsWatcherNodeConfiguration**.) Se non si utilizza il parametro Tests al momento della creazione del nodo Watcher, il nodo eseguirà automaticamente tutte le transazioni sintetiche predefinite e non eseguirà alcuna delle transazioni sintetiche non predefinite. Ciò significa,ad esempio, che il nodo Watcher verrà configurato per eseguire il test Test-CsAddressBookService, ma non il test Test-CsExumConnectivity.

  - **Non predefinite**. Come indica il nome, le transazioni sintetiche non predefinite sono i test che non vengono eseguiti per impostazione predefinita dai nodi Watcher. Il nodo Watcher può essere tuttavia abilitato all'esecuzione di qualsiasi transazione sintetica non predefinita. È possibile specificare questa impostazione durante la creazione del nodo Watcher (tramite il cmdlet **New-CsWatcherNodeConfiguration**) o in qualsiasi momento in seguito. Per molte delle transazioni sintetiche non predefinite sono necessari passaggi aggiuntivi di configurazione. Per informazioni dettagliate, vedere [Istruzioni di configurazione speciali per le transazioni sintetiche](lync-server-2013-special-setup-instructions-for-synthetic-transactions.md).

  - **Estese**. I test estesi sono un tipo speciale di transazione sintetica non predefinita. Diversamente da altre transazioni sintetiche, i test estesi possono essere eseguiti più volte durante ogni passaggio. Si tratta di un'opzione utile durante la verifica di comportamenti come più route vocali PSTN (Public Switched Telephone Network) per un pool. Per ottenere questa configurazione è sufficiente aggiungere più istanze di un test esteso a un nodo Watcher.

Per informazioni dettagliate sul processo di aggiunta di altre transazioni sintetiche a un nodo Watcher, vedere [Gestione dei nodi Watcher](lync-server-2013-managing-watcher-nodes.md). È possibile utilizzare Lync Server Management Shell per rimuovere le transazioni sintetiche da un nodo Watcher.

Le transazioni sintetiche disponibili per i nodi Watcher includono le seguenti:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome del cmdlet (nome test)</th>
<th>Descrizione</th>
<th>Tipo di transazione sintetica</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Test-CsAddressBookService (ABS)</p></td>
<td><p>Conferma che gli utenti siano in grado di cercare utenti non presenti nel loro elenco contatti.</p></td>
<td><p>Predefinita</p></td>
</tr>
<tr class="even">
<td><p>Test-CsAddressBookWebQuery (ABWQ)</p></td>
<td><p>Conferma che gli utenti siano in grado di cercare utenti non presenti nel loro elenco contatti tramite HTTP.</p></td>
<td><p>Predefinita</p></td>
</tr>
<tr class="odd">
<td><p>Test-CsIM (IM)</p></td>
<td><p>Conferma che gli utenti siano in grado di inviare messaggi istantanei peer-to-peer.</p></td>
<td><p>Predefinita</p></td>
</tr>
<tr class="even">
<td><p>Test-CsP2PAV (P2PAV)</p></td>
<td><p>Conferma che gli utenti siano in grado di effettuare chiamate audio peer-to-peer (solo segnalazione).</p></td>
<td><p>Predefinita</p></td>
</tr>
<tr class="odd">
<td><p>Test-CsPresence (Presence)</p></td>
<td><p>Conferma che gli utenti siano in grado visualizzare la presenza di altri utenti.</p></td>
<td><p>Predefinita</p></td>
</tr>
<tr class="even">
<td><p>Test-CsRegistration (Registration)</p></td>
<td><p>Conferma che gli utenti siano in grado di accedere a Lync.</p></td>
<td><p>Predefinita</p></td>
</tr>
<tr class="odd">
<td><p>Test-CsAudioConferencingProvider (ACP)</p></td>
<td><p>Non utilizzata con la versione locale di Lync Server 2013</p></td>
<td><p>Estesa</p></td>
</tr>
<tr class="even">
<td><p>Test-CsPstnPeerToPeerCall (PSTN)</p></td>
<td><p>Conferma che gli utenti siano in grado di effettuare e ricevere chiamate con persone esterne all'organizzazione (numeri PSTN).</p></td>
<td><p>Non predefinita, estesa</p></td>
</tr>
<tr class="odd">
<td><p>Test-CsAVConference (AvConference)</p></td>
<td><p>Conferma che gli utenti siano in grado di creare conferenze audio/video e di parteciparvi.</p></td>
<td><p>Predefinita</p></td>
</tr>
<tr class="even">
<td><p>Test-CsAVEdgeConnectivity (AVEdgeConnectivity)</p></td>
<td><p>Conferma che gli A/V Edge Server siano in grado di accettare connessioni da chiamate e conferenze telefoniche peer-to-peer.</p></td>
<td><p>Non predefinita</p></td>
</tr>
<tr class="odd">
<td><p>Test-CsDataConference (DataConference)</p></td>
<td><p>Conferma che gli utenti possano partecipare a conferenze con collaborazione dati, ovvero una riunione online che include attività come lavagne e sondaggi.</p></td>
<td><p>Non predefinita</p></td>
</tr>
<tr class="even">
<td><p>Test-CsExumConnectivity (ExumConnectivity)</p></td>
<td><p>Conferma che un utente possa connettersi a Messaggistica unificata di Exchange.</p></td>
<td><p>Non predefinita</p></td>
</tr>
<tr class="odd">
<td><p>Test-CsGroupIM (GroupIM)</p></td>
<td><p>Conferma che gli utenti siano in grado di inviare messaggi istantanei in conferenze e partecipare a conversazioni istantanee con tre o più persone.</p></td>
<td><p>Predefinita</p></td>
</tr>
<tr class="even">
<td><p>Test-CsGroupIM –TestJoinLauncher (JoinLauncher)</p></td>
<td><p>Conferma che gli utenti siano in grado di creare riunioni pianificate e parteciparvi tramite un collegamento a un indirizzo Web.</p></td>
<td><p>Non predefinita</p></td>
</tr>
<tr class="odd">
<td><p>Test-CsMCXP2PIM (MCXP2PIM)</p></td>
<td><p>Conferma che gli utenti di dispositivi mobili siano in grado di registrarsi e inviare messaggi istantanei.</p></td>
<td><p>Non predefinita</p></td>
</tr>
<tr class="even">
<td><p>Test-CsPersistentChatMessage (PersistentChatMessage)</p></td>
<td><p>Conferma che gli utenti possano scambiarsi messaggi tramite il servizio Chat persistente.</p></td>
<td><p>Non predefinita</p></td>
</tr>
<tr class="odd">
<td><p>Test-CsUnifiedContactStore (UnifiedContactStore)</p></td>
<td><p>Conferma che i contatti di un utente siano accessibili tramite l'archivio contatti unificati, che offre un modo per gestire un singolo set di contatti e accedervi tramite Lync 2013, Outlook e/o Outlook Web Access.</p></td>
<td><p>Non predefinita</p></td>
</tr>
<tr class="even">
<td><p>Test-CsXmppIM (XmppIM)</p></td>
<td><p>Conferma che sia possibile inviare un messaggio istantaneo attraverso il gateway XMPP (Extensible Messaging and Presence Protocol).</p></td>
<td><p>Non predefinita</p></td>
</tr>
</tbody>
</table>


Non è necessario installare nodi Watcher per poter utilizzare System Center Operations Manager. Se non si installano questi nodi, è comunque possibile ricevere avvisi in tempo reale dai componenti di Lync Server 2013 quando si verifica un problema. (Il Component and User Management Pack non utilizza nodi Watcher.) I nodi Watcher, tuttavia, sono necessari se si desidera monitorare scenari end-to-end tramite Active Monitoring Management Pack.


> [!NOTE]
> Gli amministratori possono inoltre eseguire transazioni sintetiche manualmente, senza dover utilizzare o installare Operations Manager. Per informazioni dettagliate sui vari cmdlet Test-Cs, vedere <A href="https://docs.microsoft.com/en-us/powershell/module/skype/?view=skype-ps">Indice dei cmdlet di Lync Server 2013</A>.



A seconda delle dimensioni della distribuzione, le transazioni sintetiche potrebbero usare una grande quantità di memoria e tempo del processore del computer. Per questo motivo, è consigliabile usare un computer dedicato come nodo Watcher. Non è ad esempio consigliabile configurare un Front End Server come nodo Watcher. I nodi Watcher devono soddisfare le specifiche hardware seguenti:


> [!NOTE]
> Non è possibile collocare un nodo Watcher Microsoft Lync Server 2010 legacy nello stesso computer di un nodo Watcher Lync Server 2013, perché i file principali di sistema per Lync Server 2010 e Lync Server 2013 non possono essere installati nello stesso computer.<BR>I nodi Watcher Lync Server 2013, tuttavia, possono gestire contemporaneamente il monitoraggio sia di Lync Server 2013 che di Lync Server 2010. Le transazioni sintetiche predefinite sono supportate in entrambe le versioni.



È possibile distribuire i nodi Watcher Lync Server 2013 sia all'interno che all'esterno di un'organizzazione per facilitare le seguenti verifiche:

   Connettività ai pool per gli utenti all'interno dell'organizzazione.

   Connettività tramite reti perimetrali per gli utenti remoti che lavorano all'esterno dell'organizzazione.
  
   Connettività a Survivable Branch Appliance.
  
   Connettività a Lync Server 2010 all'interno dell'organizzazione e attraverso le reti perimetrali.

Sono disponibili opzioni di autenticazione diverse per le connessioni dall'interno e dall'esterno per semplificare l'amministrazione. Per informazioni dettagliate, vedere [Configurazione di un nodo Watcher per l'esecuzione di transazioni sintetiche](lync-server-2013-configuring-a-watcher-node-to-run-synthetic-transactions.md).

Per configurare un computer come nodo Watcher, è necessario eseguire le operazioni seguenti dopo aver installato System Center Operations Manager e aver importato i Management Pack di Lync Server 2013.

Prima di installare i file principali di Lync Server 2013 e i file agente di System Center, è inoltre necessario assicurarsi che il computer del nodo Watcher soddisfi tutti i prerequisiti per l'installazione di Lync Server 2013. Nel computer del nodo Watcher, inoltre, dovrebbero essere installati gli elementi seguenti:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente hardware</th>
<th>Requisiti minimi</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CPU</p></td>
<td><p>Uno dei seguenti:</p>
<ul>
<li><p>Processore a 64 bit, quad-core, 2,33 GHz o superiore</p></li>
<li><p>Processore a 2 vie a 64 bit, dual-core, 2,33 GHz o superiore</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Memoria</p></td>
<td><p>8 GB</p></td>
</tr>
<tr class="odd">
<td><p>Sistema operativo di rete</p></td>
<td><ul>
<li><p>1 scheda di rete da 1 Gbps</p></li>
<li><p>Windows Server 2008 R2, Windows Server 2012 o</p>
<p>Windows Server 2012 R2</p></li>
</ul></td>
</tr>
</tbody>
</table>


  - Versione completa di .NET Framework 4.5.

  - Windows Identity Foundation.

  - Windows PowerShell 3.0.

Quando tutti questi prerequisiti sono soddisfatti è possibile procedere alla configurazione del nodo Watcher con i passaggi seguenti:

  - Installazione dei file principali di Lync Server 2013 nel computer del nodo Watcher.

  - Installazione dell'agente di System Center Operations Manager nel computer del nodo Watcher.

  - Esecuzione del file eseguibile Watchernode.msi.

  - Utilizzo dei cmdlet **CsWatcherNodeConfiguration** per configurare gli utenti di prova utilizzati dal nodo Watcher.

