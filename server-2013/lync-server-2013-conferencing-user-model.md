---
title: Modello utente per conferenze
TOCTitle: Modello utente per conferenze
ms:assetid: ba4bbba9-f2e3-4cab-8eba-b51f12133cab
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205199(v=OCS.15)
ms:contentKeyID: 49301799
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modello utente per conferenze

 

_**Ultima modifica dell'argomento:** 2012-10-22_

Un aspetto importante del modello utente per le conferenze di Lync Server è rappresentato dalle dimensioni delle riunioni. Dopo avere raccolto i dati dai diversi punti dati, come illustrato nella sezione precedente, è stato possibile determinare quanto segue:

  - Nella maggior parte dei casi le riunioni sono riunioni di piccole dimensioni per la collaborazione con una media di 4-6 partecipanti.

  - All'incirca l'80% delle riunioni ha meno di 20 partecipanti.

  - Il 99,98% delle riunioni ha meno di 100.

Oltre alle dimensioni delle riunioni, nel modello utente per le conferenze vengono inoltre considerati diversi fattori, tra cui i seguenti:

  - **Riunioni simultanee**   Quanti utenti si prevede siano coinvolti in riunioni nello stesso momento?

  - **Combinazione multimediale**   Quali tipi di contenuti multimediali sono disponibili e si prevede che vengano utilizzati dagli utenti durante le riunioni?

  - **Tipi di utenti**   Gli utenti sono interni, remoti, federati o anonimi?

  - **Accesso alle riunioni**   Quanto tempo è necessario a tutti gli utenti di una riunione per accedervi?

Per informazioni dettagliate sul modello utente, vedere [Modelli utente in Lync Server 2013](lync-server-2013-user-models.md).

Per determinare il numero di riunioni e utenti da utilizzare per il testing, sono state eseguite le operazioni seguenti:

  - Il numero totale degli utenti di un'organizzazione (ad esempio, 80.000 utenti) è stato moltiplicato per la percentuale di riunioni simultanee (ad esempio, il 5% di tutti gli utenti) per determinare il numero totale di utenti che si prevede partecipino a riunioni nello stesso momento (in questo caso, 4.000 utenti).

  - Il numero totale degli utenti è stato diviso per il numero di Front End Server di Lync Server 2013 inclusi nella distribuzione (ad esempio, 8 server) per determinare il numero stimato di partecipanti a riunioni per ogni Front End Server (in questo caso, 500 utenti per Front End Server).

  - Il numero degli utenti per Front End Server è stato diviso per la dimensione media delle riunioni (ad esempio, 4 utenti) per determinare il numero medio stimato di riunioni per ogni Front End Server (in questo caso, 125 riunioni per Front End Server).

  - Per ottenere il carico per tipo di contenuto multimediale in ogni Front End Server, è stata stimata la combinazione multimediale. Ad esempio, presupponendo che il 75% delle riunioni non richieda solo il supporto audio e che il 50% di tali riunioni richieda la condivisione delle applicazioni, in media 47 riunioni e 188 utenti si connettono simultaneamente a ogni Front End Server per la condivisione delle applicazioni.

  - I test sono stati eseguiti su riunioni di diverse dimensioni (in base al modello utente di un massimo di 250 utenti in un pool condiviso) per assicurare la scalabilità dei server.

