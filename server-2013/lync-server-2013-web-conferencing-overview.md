---
title: Panoramica di Web Conferencing in Lync Server 2013
TOCTitle: Panoramica di Web Conferencing in Lync Server 2013
ms:assetid: 40616dc4-f705-4890-85bf-79f76a033a9b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425913(v=OCS.15)
ms:contentKeyID: 49300319
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Panoramica di Web Conferencing in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-30_

Con le conferenze Web, gli utenti possono condividere documenti, quali presentazioni di PowerPoint, e collaborare a essi durante le conferenze. Possono inoltre condividere interamente o in parte il loro desktop con gli altri utenti in tempo reale, come se le persone che partecipano alla conferenza fossero sedute attorno allo stesso tavolo per la riunione.

## Lavagna e annotazioni

La lavagna è una schermata vuota che può essere utilizzata per la collaborazione con l'aiuto di strumenti come testo, inchiostro, disegni e immagini. Le annotazioni effettuate sulle lavagne verranno visualizzate da tutti i partecipanti. Tale funzionalità facilita la collaborazione, consentendo ai partecipanti alle riunioni di discutere, mettere insieme idee, prendere appunti e così via.

## Sondaggi

La funzionalità per sondaggi migliora la collaborazione consentendo ai relatori di determinare rapidamente le preferenze dei partecipanti. Durante le riunioni e le conversazioni online, i relatori possono utilizzare i sondaggi per raccogliere risposte anonime dai partecipanti. Tutti i relatori possono vedere i risultati e decidere se nasconderli o mostrarli a tutti i partecipanti.

## Condivisione programmi e condivisione desktop

Durante una conferenza è possibile condividere l'intero desktop, una singola applicazione o singoli monitor in un ambiente a più monitor. Oltre a visualizzare il contenuto, gli altri partecipanti alla conferenza possono anche richiedere il controllo dello schermo e, con l'autorizzazione appropriata, possono interagire con il contenuto (anche con operazioni di scorrimento e modifica).


> [!NOTE]
> I partecipanti che visualizzano la conferenza possono anche prendere il controllo e iniziare a condividere il contenuto durante la riunione



## Condivisione con PowerPoint

In Lync 2010 le presentazioni di PowerPoint venivano visualizzate in due possibili modi. Per gli utenti che eseguivano Lync 2010 venivano visualizzate utilizzando il formato PowerPoint 97-2003 mediante una copia incorporata del visualizzatore di PowerPoint. Per gli utenti che eseguivano Lync Web App, venivano convertite in file HTML dinamici e visualizzate mediante una combinazione di tali file DHTML personalizzati e di Silverlight. Anche se efficace in termini generali, questo approccio presentava alcune limitazioni:

  - Il visualizzatore incorporato di PowerPoint (che offre un'esperienza di visualizzazione ottimale) è disponibile solo nella piattaforma Windows.

  - Molti dispositivi mobili, inclusi alcuni dei più diffusi cellulari, non supportano Silverlight.

  - Il visualizzatore di PowerPoint e l'approccio DHTML/Silverlight non supportano tutte le funzionalità, quali le transizioni diapositive e i video incorporati, disponibili nelle edizioni più recenti di PowerPoint.

Per superare questi limiti e migliorare l'esperienza complessiva degli utenti in termini di introduzione o visualizzazione delle presentazioni di PowerPoint, Lync Server 2013 impiega Office Web Apps e il Server Office Web Apps per gestirle. Tra gli altri vantaggi, questo nuovo approccio offre:

  - Visualizzazioni di risoluzione superiore e supporto migliorato di funzionalità di PowerPoint, come le animazioni, le transizioni diapositive e i video incorporati.

  - Dispositivi mobili aggiuntivi per accedere a tali presentazioni. Questo perché Lync Server 2013 usa l'approccio DHTML e JavaScript standard per la trasmissione delle presentazioni di PowerPoint anziché l'approccio DHTML e Silverlight personalizzato.

  - Utenti dotati dei privilegi appropriati per lo scorrimento di una presentazione di PowerPoint indipendentemente dalla presentazione stessa. Ad esempio, mentre Ken Myer introduce la sua presentazione, Pilar Ackerman può esaminare tutte le diapositive che vuole, senza interferire con la presentazione di Ken.

