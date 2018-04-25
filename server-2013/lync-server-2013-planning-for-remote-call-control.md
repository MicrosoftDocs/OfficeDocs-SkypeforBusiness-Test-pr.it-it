---
title: 'Lync Server 2013: Pianificazione del controllo delle chiamate remote'
TOCTitle: Pianificazione del controllo delle chiamate remote
ms:assetid: 688a0328-1aa7-449f-b5f7-98c876112ed2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558658(v=OCS.15)
ms:contentKeyID: 49300856
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione del controllo delle chiamate remote in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-05_

In Lync Server 2013 il supporto degli scenari di controllo delle chiamate remote consente agli utenti di controllare i propri telefoni PBX (Private Branch eXchange) utilizzando Lync 2013 nei computer desktop. In questa sezione vengono illustrati le funzionalità di controllo delle chiamate remote e i requisiti per distribuire il controllo delle chiamate remote.

L'integrazione tra un PBX e Lync Server 2013 consente agli utenti abilitati per il controllo delle chiamate remote di utilizzare l'interfaccia utente di Lync 2013 per controllare le chiamate nei rispettivi telefoni PBX nei modi seguenti:


> [!NOTE]
> In sintesi, le capacità del PBX che ospita il telefono PBX di un utente determinano le funzionalità di controllo delle chiamate remote che saranno disponibili per tale utente.



  - Effettuare una chiamata in uscita

  - Rispondere a una chiamata in arrivo

  - Rispondere a una chiamata in arrivo con un messaggio istantaneo
    

    > [!NOTE]
    > Ovvero, quando il numero di telefono del chiamante può essere associato a un indirizzo di messaggistica istantanea nell'elenco indirizzi globale dell'organizzazione, nell'elenco Contatti di Lync del destinatario della chiamata o in un'organizzazione del partner federata.



  - Trasferire una chiamata

  - Inoltrare una chiamata in arrivo

  - Mettere in attesa le chiamate

  - Alternare tra più chiamate simultanee

  - Rispondere a una seconda chiamata quando ne è già attiva un'altra (ovvero, avviso di chiamata)

  - Comporre cifre DTMF (Dual-Tone Multifrequency)

  - Digitare note nel programma per la creazione di appunti Microsoft Office OneNote dalla finestra di conversazione

Quando un utente è abilitato per il controllo delle chiamate remote, inoltre, Lync 2013 offre le informazioni sulla chiamate seguenti:

  - Identificazione di un chiamante in base al nome quando il numero di telefono del chiamante esiste nell'elenco Contatti del client per la messaggistica e la collaborazione Microsoft Office Outlook, nell'elenco Contatti di Lync o nell'Elenco indirizzi globale dell'organizzazione di un utente abilitato per il controllo delle chiamate remote.

  - Chiamate in arrivo e in uscita effettuate, salvate nella cartella Cronologia conversazioni in Outlook.

  - Notifiche di chiamate senza risposta, inviate alla cartella Posta in arrivo di Outlook dell'utente, ma generate solo se Lync è in esecuzione al momento della ricezione della chiamata in arrivo.

## Controllo delle chiamate remote e VoIP aziendale

Sebbene le funzionalità di controllo delle chiamate remote siano separate dalle funzionalità VoIP aziendale e gli utenti non possano essere abilitati per entrambe, VoIP aziendale offre un sottoinsieme di funzionalità disponibili anche per gli utenti abilitati per il controllo delle chiamate remote. Se si distribuisce VoIP aziendale, gli utenti abilitati per il controllo delle chiamate remote possono utilizzare Lync per accedere alle funzionalità VoIP aziendale seguenti:

  - Effettuare e ricevere chiamate audio su un altro client Lync

  - Partecipare alla parte audio di una conferenza creata da un utente abilitato per VoIP aziendale

## Contenuto della sezione

  - [Attività di distribuzione per il controllo delle chiamate remote in Lync Server 2013](lync-server-2013-deployment-tasks-for-remote-call-control.md)

