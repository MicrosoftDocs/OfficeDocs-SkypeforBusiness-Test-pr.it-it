---
title: 'Lync Server 2013: Soluzioni di resilienza dei siti di succursale'
TOCTitle: Soluzioni di resilienza dei siti di succursale
ms:assetid: 1700f99b-709c-4e47-88eb-c0a5490e26e2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398234(v=OCS.15)
ms:contentKeyID: 49299802
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Soluzioni di resilienza dei siti di succursale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il fatto di garantire per l'organizzazione la resilienza dei siti derivati offre ovvi vantaggi. In particolare, se la connessione al sito centrale va persa, gli utenti dei siti di succursale possono comunque continuare a disporre del servizio VoIP aziendale e della segreteria telefonica, sempre che siano state configurate di conseguenza le impostazioni di reindirizzamento della segreteria telefonica. Per informazioni dettagliate, vedere [Requisiti di resilienza dei siti di succursale per Lync Server 2013](lync-server-2013-branch-site-resiliency-requirements.md)). Per i siti con meno di 25 utenti, una soluzione di resilienza tuttavia può non risultare economicamente conveniente.

Se si decide di garantire la resilienza dei siti di succursale, sono disponibili tre opzioni. Per scegliere l'opzione più adatta all'organizzazione, utilizzare come riferimento la tabella riportata di seguito.



<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Se...</th>
<th>È consigliabile utilizzare un…</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nel sito di succursale vengono ospitati dai 25 ai 1000 utenti e l'utile sugli investimenti non consente una distribuzione completa oppure non è disponibile supporto amministrativo locale</p></td>
<td><p>Survivable Branch Appliance</p>
<p>Survivable Branch Appliance è un blade server standard del settore con la funzione di registrazione di Lync Server e Mediation Server in esecuzione in Windows Server 2008 R2. In Survivable Branch Appliance è inoltre incluso un gateway PSTN (Public Switched Telephone Network). I dispositivi di terze parti qualificati, sviluppati da partner Microsoft nell'ambito del programma di qualifica e certificazione degli SBA (Survivable Branch Appliance), forniscono una connessione PSTN continua in caso di problemi della rete WAN, ma non garantiscono un servizio di presenza o conferenza resiliente perché tali funzionalità dipendono dai Front End Server nel sito centrale.</p>
<p>Per informazioni dettagliate sui Survivable Branch Appliance, vedere &quot;Dettagli sul Survivable Branch Appliance&quot; più avanti in questo argomento.</p>
<p><strong>Nota:</strong> se si decide di utilizzare anche un trunk SIP con Survivable Branch Appliance, contattare il fornitore di Survivable Branch Appliance per individuare il provider di servizi più adatto per l'organizzazione.</p></td>
</tr>
<tr class="even">
<td><p>Nel sito di succursale vengono ospitati dai 1000 ai 2000 utenti, manca una connessione WAN resiliente e sono disponibili amministratori di Lync Server addestrati</p></td>
<td><p>Survivable Branch Server o due Survivable Branch Appliance.</p>
<p>Il Survivable Branch Server è un server Windows che soddisfa i requisiti hardware specificati e in cui è installato il software della funzione di registrazione e del Mediation Server di Lync Server. Deve connettersi a un gateway PSTN o a un trunk SIP verso un provider di servizi telefonici.</p>
<p>Per informazioni dettagliate sui Survivable Branch Server, vedere &quot;Dettagli sul Survivable Branch Server &quot; più avanti in questo argomento.</p></td>
</tr>
<tr class="odd">
<td><p>Sono necessarie le funzionalità di presenza e conferenza oltre alle funzionalità vocali per un massimo di 5000 utenti e sono disponibili amministratori di Lync Server addestrati</p></td>
<td><p>Eseguire la distribuzione come sito centrale con un server Standard Edition anziché come sito di succursale.</p>
<p>Una distribuzione di Lync Server completa fornisce una connessione PSTN continua e servizi di presenza e conferenza resilienti in caso di problemi della rete WAN.</p>
<p>Per informazioni dettagliate sulla preparazione per tale soluzione, vedere <a href="lync-server-2013-planning-for-your-organization.md">Pianificazione per l'organizzazione per Lync Server 2013</a>, <a href="lync-server-2013-determining-your-system-requirements.md">Determinazione dei requisiti di sistema per Lync Server 2013</a>, <a href="lync-server-2013-determining-your-infrastructure-requirements.md">Determinazione dei requisiti dell'infrastruttura per Lync Server 2013</a> e altre sezioni pertinenti nella documentazione relativa alla pianificazione.</p></td>
</tr>
</tbody>
</table>


## Topologie di resilienza

Nella figura seguente vengono illustrate le topologie consigliate per la resilienza dei siti di succursale.

**Opzioni di resilienza per i siti di succursale**

![Opzioni di resilienza vocale dei siti di succursale (o siti derivati)](images/Gg398234.47eecd19-08ae-4d82-acbe-61f0de760306(OCS.15).jpg "Opzioni di resilienza vocale dei siti di succursale (o siti derivati)")

## Dettagli relativi al Survivable Branch Appliance

In Survivable Branch Appliance di Lync Server sono inclusi i componenti seguenti:

  - Una funzione di registrazione per l'autenticazione degli utenti, la registrazione e il routing delle chiamate

  - Un Mediation Server per la gestione dei segnali tra la funzione di registrazione e un gateway PSTN

  - Un gateway PSTN per il routing delle chiamate alla rete PSTN come trasporto di fallback in caso di problemi della rete WAN

  - SQL Server Express per l'archiviazione dei dati degli utenti in locale

Nel Survivable Branch Appliance sono inoltre inclusi trunk PSTN, porte analogiche e una scheda Ethernet.

Se la connessione WAN del sito di succursale a un sito centrale non è più disponibile, gli utenti interni del sito di succursale continueranno a essere registrati nella funzione di registrazione di Survivable Branch Appliance e a ottenere senza interruzioni il servizio vocale mediante la connessione di Survivable Branch Appliance alla rete PSTN. Gli utenti del sito di succursale che si connettono da casa o da altre postazioni remote saranno in grado di registrarsi in un server di registrazione presso un sito centrale in caso di non disponibilità del collegamento WAN al sito di succursale. Tali utenti disporranno della funzionalità di comunicazione unificata completa, con l'unica eccezione che le chiamate in ingresso nel sito di succursale verranno indirizzate alla segreteria telefonica. Quando la connessione WAN torna disponibile, per gli utenti del sito di succursale viene ripristinata la funzionalità completa. Non è necessaria la presenza di un amministratore IT per il failover su Survivable Branch Appliance o per il ripristino del servizio.

Lync Server supporta fino a due Survivable Branch Appliance in un sito di succursale.

## Panoramica della distribuzione del Survivable Branch Appliance

Survivable Branch Appliance viene prodotto da OEM (Original Equipment Manufacturer) partner di Microsoft e distribuito per loro conto da parte di rivenditori. Tale distribuzione deve essere implementata solo dopo che Lync Server è stato distribuito nel sito centrale, che è stata allestita una connessione WAN al sito di succursale e che gli utenti di tale sito sono stati abilitati per VoIP aziendale.

Per informazioni dettagliate su queste fasi, vedere [Distribuzione di Survivable Branch Appliance o Survivable Branch Server con Lync Server 2013](lync-server-2013-deploying-a-survivable-branch-appliance-or-server.md) nella documentazione relativa alla distribuzione.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Fase</th>
<th>Passaggi</th>
<th>Diritti utente</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Impostare Servizi di dominio Active Directory per il Survivable Branch Appliance.</p></td>
<td><p><strong>Nel sito centrale:</strong></p>
<ol>
<li><p>Creare un account utente di dominio (o un'identità aziendale) per il tecnico che installerà e attiverà il Survivable Branch Appliance nel sito di succursale.</p></li>
<li><p>Creare un account computer (con il nome di dominio completo (FQDN) applicabile) per Survivable Branch Appliance in Servizi di dominio Active Directory.</p></li>
<li><p>In Generatore di topologie creare e pubblicare il Survivable Branch Appliance.</p></li>
</ol></td>
<td><p>L'account utente del tecnico deve essere membro del gruppo RTCUniversalSBATechnicians. Il Survivable Branch Appliance deve appartenere al gruppo RTCSBAUniversalServices e questo avviene automaticamente quando si utilizza Generatore di topologie.</p></td>
</tr>
<tr class="even">
<td><p>Installare e attivare il Survivable Branch Appliance.</p></td>
<td><p><strong>Nel sito di succursale:</strong></p>
<ol>
<li><p>Collegare il Survivable Branch Appliance a una porta Ethernet e a una porta PSTN.</p></li>
<li><p>Avviare Survivable Branch Appliance.</p></li>
<li><p>Aggiungere il Survivable Branch Appliance al dominio utilizzando l'account utente di dominio creato per il Survivable Branch Appliance nel sito centrale. Impostare l'FQDN e l'indirizzo IP in modo che corrispondano all'FQDN creato nell'account computer.</p></li>
<li><p>Configurare il Survivable Branch Appliance mediante l'interfaccia utente dell'OEM.</p></li>
<li><p>Verificare la connettività PSTN.</p></li>
</ol></td>
<td><p>L'account utente del tecnico deve essere membro del gruppo RTCUniversalSBATechnicians.</p></td>
</tr>
</tbody>
</table>


## Dettagli relativi al Survivable Branch Server

In Generatore di topologie creare il sito di succursale, aggiungere il Survivable Branch Server a tale sito e quindi eseguire la Distribuzione guidata di Lync Server nel computer in cui si desidera installare il ruolo.

## Vedere anche

#### Ulteriori risorse

[Distribuzione di Lync Server 2013](lync-server-2013-deploying-lync-server.md)

