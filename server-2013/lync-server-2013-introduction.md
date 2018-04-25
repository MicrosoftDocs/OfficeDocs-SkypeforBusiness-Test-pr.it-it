---
title: 'Lync Server 2013: Introduzione'
TOCTitle: Introduzione a Lync Server
ms:assetid: 99dd6b65-e591-421f-852b-ee9fe9588998
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398795(v=OCS.15)
ms:contentKeyID: 49301426
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Introduzione a Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Lync Server 2013 e il relativo software client, ad esempio Lync 2013, offre agli utenti nuovi modi di rimanere in contatto indipendentemente dalla località geografica. Lync e Lync Server uniscono i diversi modi in cui le persone comunicano in una singola interfaccia client, vengono distribuiti come piattaforma unificata e sono amministrati tramite una sola infrastruttura di gestione.

In questa tabella e nelle sezioni successive vengono illustrati i principali set di funzionalità, o *carichi di lavoro* , che Lync Server rende disponibili agli utenti.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Carico di lavoro</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Messaggistica istantanea e presenza</p></td>
<td><p>Messaggistica istantanea (IM) e presenza consentono agli utenti di trovarsi e comunicare tra loro in modo efficace ed efficiente.</p>
<p>La messaggistica istantanea fornisce una piattaforma IM con cronologia delle conversazioni e supporta la connettività di messaggistica istantanea pubblica con gli utenti di reti come MSN/Windows Live, Yahoo!, AOL e Google Talk.</p>
<div class="alert">
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Dal 1 settembre 2012, la licenza di sottoscrizione utenti per la connettività di messaggistica istantanea pubblica di Microsoft Lync (“PIC USL”) non è più disponibile per l'acquisto per i nuovi contratti o quelli in fase di rinnovo. I clienti con licenze attive potranno continuare a eseguire la federazione con Yahoo! Messenger fino alla data di chiusura del servizio. Giugno 2014 è la data di fine servizio annunciata per Yahoo! e AOL. Per informazioni dettagliate, vedere <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Supporto della connettività per messaggistica istantanea pubblica in Lync Server 2013</a>.</p></li>
<li><p>La licenza PIC USL è una licenza di sottoscrizione di tipo mensile per utente, richiesta per la federazione di Lync Server o Office Communications Server con Yahoo! Messenger. La capacità di Microsoft di fornire questo servizio dipende dal supporto offerto da Yahoo! e il contratto sottostante è in fase di chiusura.</p></li>
<li><p>Oggi più che mai, Lync è un potente strumento per la connessione tra diverse organizzazioni e con utenti di tutto il mondo. La federazione con Windows Live Messenger non richiede ulteriori licenze per utente/dispositivo in aggiunta alla licenza CAL Standard per Lync. La federazione con Skype verrà aggiunta a questo elenco, consentendo agli utenti di Lync di raggiungere centinaia di milioni di persone tramite messaggistica istantanea e comunicazioni vocali.</p></li>
</ul></td>
</tr>
</tbody>
</table>

</div>
<p>La presenza determina e visualizza la disponibilità personale di un utente e la sua volontà di comunicare, mediante l'utilizzo di stati comuni quali <strong>Disponibile</strong> o <strong>Occupato</strong> nonché con stati più dettagliati quali <strong>Torno subito</strong> e <strong>Non disturbare</strong> . Queste informazioni sulla presenza avanzata consentono agli altri utenti di utilizzare immediatamente scelte di comunicazione efficienti.</p></td>
</tr>
<tr class="even">
<td><p>Servizi di conferenza</p></td>
<td><p>Lync Server include il supporto per conferenze di messaggistica istantanea, conferenze audio, conferenze Web, conferenze video e condivisione delle applicazioni, per riunioni sia pianificate che estemporanee. Tutti questi tipi di riunione sono supportati mediante un unico client. Lync Server supporta inoltre le conferenze telefoniche con accesso esterno, che consentono agli utenti di telefoni PSTN di accedere ai contenuti audio di una conferenza.</p>
<p>Le conferenze possono cambiare e crescere in tempo reale senza problemi. Ad esempio, una singola conferenza può iniziare come un semplice scambio di messaggi istantanei tra pochi utenti e trasformarsi in una conferenza audio con condivisione del desktop e con un pubblico più vasto istantaneamente, facilmente e senza interrompere il flusso di conversazione.</p></td>
</tr>
<tr class="odd">
<td><p>VoIP aziendale</p></td>
<td><p><em>VoIP aziendale</em> è l'offerta VoIP (Voice over Internet Protocol) disponibile in Lync Server, che offre un'opzione vocale per migliorare o sostituire i sistemi PBX tradizionali. In aggiunta alle funzionalità di telefonia complete di un IP PBX, VoIP aziendale integra presenza avanzata, messaggistica istantanea, collaborazione e riunioni. Funzionalità quali la risposta, l'attesa, la ripresa, il trasferimento, l'inoltro e la deviazione delle chiamate sono supportate direttamente, mentre i pulsanti personalizzati di composizione veloce sono sostituiti da elenchi di contatti e l'intercom automatico è sostituito dalla messaggistica istantanea.</p>
<p>VoIP aziendale supporta la disponibilità elevata mediante controllo di ammissione di chiamata (CAC), branch office survivability e opzioni estese per la resilienza dei dati.</p></td>
</tr>
<tr class="even">
<td><p>Supporto per gli utenti remoti</p></td>
<td><p>È possibile rendere disponibili agli utenti che attualmente si trovano all'esterno dei firewall aziendali tutte le funzionalità di Lync Server mediante la distribuzione di server denominati <em>server perimetrali</em> , che forniscono una connessione per gli utenti remoti. Tali utenti possono connettersi alle conferenze utilizzando un personal computer con Lync 2013 installato, tramite telefono o tramite un'interfaccia Web.</p>
<p>La distribuzione dei server perimetrali consente inoltre di attuare la <em>federazione</em> con altre organizzazioni, ad esempio partner o fornitori. Una relazione federata consente agli utenti di inserire gli utenti federati nei propri elenchi di contatti, scambiare con essi informazioni sulla presenza e messaggi istantanei e invitarli a chiamate audio, chiamate video e conferenze.</p></td>
</tr>
<tr class="odd">
<td><p>Supporto di client mobili</p></td>
<td><p>Inoltre, con i servizi per dispositivi mobili di Lync Server, gli utenti possono accedere alle funzionalità di Lync con dispositivi mobili Apple iOS, Android, Windows Phone o Nokia supportati ed eseguire attività quali lo scambio di messaggio istantanei, la visualizzazione dei contatti e della presenza. Inoltre, i dispositivi mobili supportano alcune funzionalità di VoIP aziendale, quali l'accesso con un clic alle conferenze, la chiamata tramite ufficio, il numero unico, la segreteria telefonica e le chiamate senza risposta. Le notifiche push sono inoltre supportate per i dispositivi mobili che non supportano applicazioni in esecuzione in background.</p></td>
</tr>
<tr class="even">
<td><p>Integrazione con altri prodotti</p></td>
<td><p>Lync Server si integra con vari altri prodotti per fornire ulteriori vantaggi a utenti e amministratori.</p>
<p>Gli strumenti per riunioni sono integrati in Outlook per consentire agli organizzatori di pianificare una riunione o avviare una conferenza estemporanea con un solo clic e rendere altrettanto semplice l'accesso dei partecipanti.</p>
<p>Le informazioni sulla presenza sono integrate in Outlook e SharePoint.</p>
<p>La messaggistica unificata di Exchange offre numerose funzionalità di integrazione. Gli utenti possono controllare la presenza di nuovi messaggi in segreteria telefonica all'interno di Lync Server. Possono fare clic su un pulsante di riproduzione nel messaggio di Outlook per ascoltare l'audio del messaggio, oppure visualizzarne una trascrizione nel messaggio di notifica.</p>
<p>Inoltre, l'esecuzione di Lync Server 2013 con Exchange 2013 rende disponibili nuove funzionalità quali l'archivio contatti unificato accessibile dai client di entrambi i prodotti, nonché le foto dei contatti ad alta risoluzione archiviate nel database di Exchange 2013.</p></td>
</tr>
<tr class="odd">
<td><p>Distribuzione semplice</p></td>
<td><p>Per agevolare la pianificazione e la distribuzione di server e client, Lync Server fornisce il Generatore di topologie.</p>
<p></p>
<p>Generatore di topologie è un componente dell'installazione di Lync Server. Si utilizza Generatore di topologie per creare, adattare e pubblicare la topologia pianificata, quindi convalidarla prima di avviare le installazioni dei server. Quando si installa Lync Server nei singoli server, il programma di installazione distribuisce il server in base alle indicazioni nella topologia.</p></td>
</tr>
<tr class="even">
<td><p>Gestione semplice</p></td>
<td><p>Dopo la distribuzione di Lync Server saranno disponibili gli strumenti di gestione semplici e potenti descritti di seguito:</p>
<ul>
<li><p>La gestione centrale della configurazione che consente di gestire le modifiche in modo centralizzato e di replicarle rapidamente nell'intera distribuzione.</p></li>
<li><p>Pannello di controllo di Lync Server, una interfaccia grafica basata sul Web grazie alla quale gli amministratori di Lync Server possono gestire i sistemi via Internet sulla rete aziendale senza dover installare software di gestione professionali sui propri computer.</p></li>
<li><p>Strumento di gestione da riga di comando Lync Server Management Shell, basato sull' interfaccia della riga di comando Windows PowerShell. Fornisce un ampio set di comandi per l'amministrazione di tutti gli aspetti del prodotto e consente agli amministratori di Lync Server di automatizzare le attività ripetitive servendosi di uno strumento familiare.</p></li>
</ul></td>
</tr>
</tbody>
</table>


Le funzionalità di messaggistica istantanea e presenza vengono installate automaticamente in ogni distribuzione di Lync Server, ma è possibile scegliere di distribuire o meno funzionalità di conferenza, VoIP aziendale e accesso utente remoto in base alle specifiche esigenze dell'organizzazione.

## Argomenti della sezione

  - [Messaggistica istantanea e presenza in Lync Server 2013](lync-server-2013-im-and-presence.md)

  - [Servizi di conferenza in Lync Server 2013](lync-server-2013-conferencing.md)

  - [VoIP aziendale in Lync Server 2013](lync-server-2013-enterprise-voice.md)

  - [Scalabilità con Lync Server 2013](lync-server-2013-scalability.md)

