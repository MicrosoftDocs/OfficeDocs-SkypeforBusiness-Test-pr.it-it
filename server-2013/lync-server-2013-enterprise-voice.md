---
title: 'Lync Server 2013: VoIP aziendale'
TOCTitle: VoIP aziendale
ms:assetid: c9da8099-6f4f-4346-ac67-f041bb96072c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg417163(v=OCS.15)
ms:contentKeyID: 49301978
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# VoIP aziendale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-04-08_

Con VoIP aziendale, Lync Server offre un protocollo VoIP (Voice over Internet Protocol) autonomo per migliorare o sostituire i centralini (PBX) tradizionali. Gli utenti di VoIP aziendale possono chiamare i colleghi sulla rete VoIP o sul sistema PBX dell'organizzazione, nonché numeri di telefono tradizionali all'esterno dell'organizzazione. La soluzione VoIP aziendale include funzionalità di chiamata comuni quali la risposta, l'inoltro, il trasferimento, l'attesa, la deviazione, il rilascio e il parcheggio, nonché servizi di chiamate di emergenza (Enhanced 9-1-1 o E9-1-1 è disponibile solo negli Stati Uniti). VoIP aziendale supporta inoltre una vasta gamma di dispositivi IP e USB correnti e meno recenti.

## Effettuare e ricevere chiamate

Gli utenti che dispongono di client Lync possono effettuare chiamate digitando un nome o un numero di telefono sulla tastiera oppure utilizzando una tastiera visualizzata sullo schermo. Possono inoltre eseguire le chiamate direttamente dal proprio elenco Contatti, nonché distribuire i dispositivi Lync Phone Edition, ovvero dispositivi telefonici IP autonomi forniti da partner Microsoft.

Gli utenti possono disporre di più dispositivi telefonici registrati in Lync Server e passare dall'uno all'altro facilmente.

Vengono avvisati in caso di chiamate in arrivo su tutti i dispositivi contemporaneamente, mediante suonerie personalizzabili sui dispositivi telefonici IP e una notifica simile a un messaggio istantaneo sul PC.

Gli utenti possono inoltre impostare un singolo numero di telefono che si connette al telefono da tavolo, al PC e al cellulare, in modo da essere raggiungibili in qualsiasi luogo.

## Funzionalità di chiamata di base

Durante una chiamata, un utente può rispondere ad altre chiamate in arrivo o avviare chiamate in uscita mentre la chiamata attiva esistente viene automaticamente messa in attesa. Le chiamate possono essere trasferite da un utente all'altro, direttamente o dopo che il primo utente ha parlato in privato con il secondo. Gli utenti possono inoltre trasferire le chiamate a un altro dispositivo, ad esempio possono trasferire una chiamata attiva al loro cellulare mentre varcano la porta del proprio ufficio.

## Comunicazioni più complete

Quando parlano con un altro utente utilizzando Lync, gli utenti possono aggiungere facilmente funzionalità di condivisione del desktop, testo o video alla chiamata. La funzionalità Non disturbare è integrata nelle impostazioni relative alla presenza di Lync.

Grazie al servizio Messaggistica unificata di Exchange, Lync e Lync Server sono integrati con Microsoft Exchange Server 2013 e Microsoft Outlook 2013. Gli utenti possono verificare la presenza di nuovi messaggi nella segreteria telefonica sia dalla finestra di Lync che dalla posta elettronica. Mentre è aperto il programma di posta elettronica, possono fare clic per riprodurre l'audio della segreteria telefonica in un messaggio di posta elettronica o visualizzare una trascrizione del messaggio della segreteria telefonica.

## Funzionalità di chiamata avanzate

VoIP aziendale include inoltre diverse funzionalità di chiamata avanzate, come la delega, l'intercettazione team, la risposta alle chiamate di gruppo e i Response Group.

La delega consente agli utenti di delegare la gestione delle chiamate a uno o più assistenti. Consente inoltre di eseguire più attività di chiamata per conto dell'utente, ad esempio la selezione delle chiamate, l'esecuzione di chiamate e l'avvio delle conferenze.

Con l'intercettazione team, è possibile fare in modo che le chiamate in arrivo vengano inviate contemporaneamente ai telefoni dei membri di un team in modo che ogni membro del team possa rispondere alla chiamata.

La risposta alle chiamate di gruppo, una nuova caratteristica degli aggiornamenti cumulativi per Lync Server 2013 di febbraio 2013, consente agli utenti di rispondere alle chiamate in arrivo ai colleghi dai propri telefoni. La risposta alle chiamate di gruppo è diversa dall'intercettazione team principalmente perché una chiamata in arrivo squilla solo sul telefono del destinatario desiderato, ma qualsiasi altro utente può scegliere di rispondere componendo un numero di risposta alle chiamate di gruppo.

I Response Group possono essere impostati per l'accodamento e il routing intelligente delle chiamate agli agenti designati. Gli usi comuni includono l'helpdesk IT, le hotline delle risorse umane e altri centri di contatto interni.

## Amministrazione VoIP aziendale

Lync Server si basa sugli standard e le interfacce pubblicate per interagire con l'infrastruttura esistente. Supporta sia le opzioni gateway che SIP, ad esempio il trunking SIP, per l'interconnessione con i sistemi IP PBX e le reti PSTN, in modo da consentire la migrazione graduale degli utenti a VoIP aziendale, riducendo al tempo stesso le interruzioni. Lync Server supporta i codec tradizionali, ad esempio G.711, G.722 e G.723.1, per l'interoperabilità con le soluzioni VoIP tradizionali.

Grazie al servizio Controllo di ammissione di chiamata, gli amministratori possono impostare limiti sulla quantità di traffico vocale e video di Lync Server attraverso collegamenti di rete vincolati e specificare l'azione da intraprendere quando una nuova chiamata supera il limite impostato. Le azioni possono includere il routing con un percorso alternativo o il rifiuto della chiamata.

Lync Server può essere utilizzato con Survivable Branch Appliance di terze parti per offrire servizi di chiamate locali e la connessione alla rete PSTN delle succursali in caso di errore WAN nel sito centrale.

