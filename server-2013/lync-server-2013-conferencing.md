---
title: 'Lync Server 2013: Servizi di conferenza'
TOCTitle: Servizi di conferenza
ms:assetid: 6129b7e0-9abd-488e-a54e-86094eb9df7a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg417161(v=OCS.15)
ms:contentKeyID: 49300739
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Servizi di conferenza in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-11_

Con le conferenze unificate in Lync Server 2013 gli utenti possono collaborare, condividere informazioni e coordinare il proprio lavoro in tempo reale. Tutti gli utenti possono avvalersi dell'intera gamma di strumenti per la collaborazione spontanea, le riunioni pianificate e le riunioni. Le funzionalità per conferenze audio e video possono essere utilizzate da qualsiasi posizione con una connessione Internet e gli utenti lontani da un computer possono partecipare a conferenze audio chiamando con un telefono PSTN (Public Switched Telephone Network) .

Gli strumenti per riunioni integrati in Outlook consentono agli organizzatori di pianificare una riunione o avviare una conferenza estemporanea con un solo clic e inoltre di rendere altrettanto semplice l'accesso dei partecipanti. Un client Web estende le funzionalità per conferenze avanzate ai partecipanti che non eseguono la versione desktop di Lync

## Conferenze audio e video

L'esperienza utente offerta da Lync Server è familiare per gli utenti di servizi di ponte audio tradizionali, inclusi i servizi di accesso esterno PSTN con comandi di controllo delle chiamate a toni. Sono allo stesso tempo incluse funzionalità avanzate per pianificazione, partecipazione e gestione disponibili solo con una piattaforma di comunicazioni unificate integrata.

Con un solo clic gli utenti possono pianificare una riunione da Outlook. I dettagli, come l'ora, il luogo e i partecipanti della riunione seguono il noto modello di Outlook, Le informazioni specifiche della chiamata per la conferenza, inoltre, come numero di accesso, ID delle riunioni e promemoria per i PIN, vengono compilate automaticamente.

Per assicurarsi che solo le persone autorizzate possano partecipare a una chiamata, in Lync Server sono disponibili più livelli di autenticazione per i partecipanti. Gli utenti che partecipano tramite Lync sono già autenticati da Servizi di dominio Active Directory e non viene loro richiesto di immettere un PIN, un passcode o l'ID della riunione.

In Lync, l'esperienza utente per le conferenze video risulta semplificata grazie all'incorporamento del video nel client unificato, in modo che la pianificazione di una riunione con video o l'escalation spontanea a conferenza video sia semplice e lineare.

Con Lync Server basta un solo clic per aggiungere l'elemento video a una chiamata telefonica standard. Se alla chiamata video o a una conferenza partecipano più utenti, ogni utente può vedere il video di un massimo di cinque altri utenti contemporaneamente e un relatore può scegliere una sola origine video per essere l'unico a essere visibile per tutti i partecipanti.

Per le chiamate peer-to-peer tra utenti che eseguono Lync in computer di fascia alta sono supportate risoluzioni video ad alta definizione (1270 x 720 con proporzioni 16:9) e VGA (640 x 480 con proporzioni 4:3). La risoluzione disponibile per ogni partecipante a una singola conversazione può essere diversa, a seconda delle capacità video del rispettivo hardware di ogni utente.

Gli amministratori IT possono impostare criteri per limitare o disabilitare il video ad alta definizione o VGA nei client, in base alle caratteristiche del computer, alla larghezza di banda della rete e alla presenza di videocamere in grado di offrire la risoluzione richiesta. Questi criteri vengono applicati tramite il provisioning di tipo in-band.

## Conferenze Web

Lync Server integra le funzionalità di condivisione per le conferenze, come desktop, applicazioni, allegati, lavagna, sondaggi e PowerPoint in una versione di Lync semplificata. In combinazione con le funzionalità per conferenze audio o video, il risultato è una sessione di collaborazione molto coinvolgente e facile da coordinare.

Per offrire un'esperienza utente complessivamente migliore per la presentazione o la visualizzazione di presentazioni di PowerPoint, Lync Server 2013 utilizza Office Web Apps per gestire le presentazioni di PowerPoint. Gli utenti possono condividere un'immagine oppure copiare e incollare testo tramite una lavagna nella riunione Lync. I relatori possono condurre sondaggi nella riunione Lync per richiedere e raccogliere le opinioni dei partecipanti.

La condivisione del desktop consente ai relatori di trasmettere elementi visivi, applicazioni, pagine Web, documenti, software o parte del desktop ai partecipanti remoti in tempo reale, direttamente da Lync. I membri del pubblico possono seguire e contribuire con movimenti del mouse e input da tastiera. I relatori possono scegliere di condividere l'intero schermo o solo una parte. Con la condivisione dei desktop, i relatori possono intrattenere il pubblico con dimostrazioni di prodotti o software interattive da qualsiasi luogo.

Con la condivisione delle applicazioni i relatori possono condividere il controllo del software sul desktop senza perdere di vista i commenti e suggerimenti o le domande testuali dei partecipanti. I relatori hanno inoltre la possibilità di delegare il controllo dell'applicazione ai partecipanti alla riunione.

## Conferenza telefonica con accesso esterno

Per gli utenti che non utilizzano un PC sono disponibili vari metodi per partecipare a una conferenza telefonica di Lync Server. Un utente PSTN può comporre un numero di accesso, accedere al ponte della riunione e quindi immettere l'ID della riunione. Per una maggiore sicurezza delle riunioni, è inoltre possibile che all'utente venga richiesto di immettere il PIN per l'autenticazione in Active Directory. In Lync Server sono inoltre supportati dispositivi Lync Phone Edition, ovvero dispositivi telefonici IP autonomi forniti da partner Microsoft.

