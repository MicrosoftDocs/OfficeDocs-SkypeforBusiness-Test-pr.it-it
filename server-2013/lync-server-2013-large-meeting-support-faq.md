---
title: "#VALUE!"
TOCTitle: "#VALUE!"
ms:assetid: 34b4fb6a-e35c-47e8-8ab1-f8331741fed2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204804(v=OCS.15)
ms:contentKeyID: 49300145
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Domande frequenti sul supporto delle riunioni di grandi dimensioni in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-22_

Le sezioni seguenti forniscono risposte alle domande comuni sulla creazione e sull'esecuzione di riunioni di grandi dimensioni.

## D: quanti utenti possono partecipare a una riunione di grandi dimensioni?

Il modello di utente di Lync Server specifica il limite di 250 utenti in un pool condiviso o di 1000 utenti in un pool dedicato alle riunioni di grandi dimensioni, tuttavia questi valori si riferiscono al numero di utenti sottoposto a test e al set di componenti hardware specifico usato durante il test. Il test consente di stabilire i limiti consigliati per le dimensioni massime. È tuttavia possibile controllare il numero effettivo di partecipanti consentito nelle riunioni dell'organizzazione mediante la configurazione di uno o più criteri di conferenza. Questa operazione può essere eseguita utilizzando i cmdlet Windows PowerShell in Lync Server Management Shell o mediante il Pannello di controllo di Lync Server. Il valore specificato in un criterio di conferenza può essere qualsiasi numero intero a 32 bit compreso tra 1 e 4.294.967.295, tuttavia la dimensione consigliata è compresa tra 2 e 250 partecipanti e il valore predefinito è 250.

## D: quante riunioni o altri carichi di lavoro si posso avere in un pool dedicato alle riunioni di grandi dimensioni?

Per offrire la migliore esperienza utente nelle riunioni di grandi dimensioni che includono fino a 1000 partecipanti, è consigliabile ospitare una sola grande riunione per volta in un pool dedicato alle riunioni di grandi dimensioni. È inoltre preferibile non consentire l'esecuzione di altri carichi di lavoro sullo stesso pool durante una riunione di questo tipo.

## D: gli organizzatori di riunioni di grandi dimensioni devono essere ospitati nel pool dedicato?

No. È consigliabile non ospitare nel pool dedicato utenti al di fuori del personale dedicato che gestisce la pianificazione di riunioni di grandi dimensioni. In questo modo si evita che ulteriore traffico di comunicazioni in tempo reale determini problemi con le riunioni di grandi dimensioni ospitate nel pool. È necessario pianificare le riunioni di grandi dimensioni nel pool dedicato utilizzando un account utente del personale preposto alla pianificazione delle riunioni di questo tipo. L'account utente dell'organizzatore della riunione (l'utente che richiede una riunione di grandi dimensioni) deve essere aggiunto come relatore della riunione.

## D: quali supporti multimediali posso usare in una riunione di grandi dimensioni?

Le riunioni di grandi dimensioni con un massimo di 1000 utenti possono includere audio, video, condivisione PowerPoint, lavagne e sondaggio delle presenze.

## D: posso usare la messaggistica istantanea di gruppo nelle riunioni di grandi dimensioni?

Sì, anche se un numero elevato di messaggi istantanei, soprattutto se inviati da molti partecipanti durante una riunione, può compromettere l'esperienza dell'utente a causa del testo veloce che scorre nella finestra di messaggistica istantanea. L'invio di una grande quantità di messaggi istantanei a un numero di utenti che può arrivare a 1000 può anche introdurre carichi server significativi che possono influire sulle prestazioni. La messaggistica istantanea generalmente è richiesta solo per lo scambio di domande e risposte.

## Gli utenti possono partecipare alle riunioni di grandi dimensioni componendo un numero da un telefono?

Sì. Se il pool di Lync Server 2013 è stato distribuito correttamente ed è abilitato per le conferenze telefoniche con accesso esterno, gli utenti potranno partecipare alle conferenze di grandi dimensioni componendo un numero telefonico. Il test ha rilevato che fino al 15% dei 1000 utenti può partecipare alla riunione per un periodo superiore ai 10 minuti.

## D: posso ospitare riunioni di grandi dimensioni in una topologia virtuale?

Non sono stati eseguiti test sulle riunioni di grandi dimensioni in una topologia virtuale, pertanto non l'uso delle macchine virtuali per ospitare un pool dedicato per le riunioni di grandi dimensioni non è supportato.

