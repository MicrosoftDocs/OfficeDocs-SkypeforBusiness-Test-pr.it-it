---
title: Supporto di riunioni di grandi dimensioni tramite Lync Server 2013
TOCTitle: Supporto di riunioni di grandi dimensioni tramite Lync Server 2013
ms:assetid: 509a424f-a33d-4e72-8f87-a3ec7bb1ddeb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204894(v=OCS.15)
ms:contentKeyID: 49300563
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Supporto di riunioni di grandi dimensioni tramite Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-03_

Le riunioni di grandi dimensioni non seguono il modello di test descritto nella sezione precedente, poiché hanno le caratteristiche seguenti:

  - La riunione è una presentazione uno a molti.

  - Pochi utenti hanno il ruolo di relatori o il relatore è uno solo e gli altri utenti sono solo partecipanti.

  - La principale attività di collaborazione dati è la condivisione di presentazioni di PowerPoint.

  - L'audio è indispensabile e possono essere usate anche le funzionalità video.

  - Una persona dedicata, di solito l'organizzatore della riunione o un assistente dell'organizzatore, imposta la riunione con buon anticipo.

  - Uno staff dedicato (non i relatori) si occupa di aspetti della riunione quali la connessione alla riunione online, la verifica del funzionamento di audio, video e condivisione delle diapositive, la gestione della sala di attesa e dei ruoli utente, la disattivazione e la riattivazione dell'audio dei partecipanti, la raccolta delle domande e la gestione delle registrazione, come più opportuno.

Per supportare riunioni di grandi dimensioni con un massimo di 1000 utenti, è necessario affrontare i problemi relativi al modello dell'hardware condiviso e al modello senza prenotazione.

Per disporre di risorse di CPU e di memoria per riunioni con un massimo di 1000 utenti, i Front End Server host non devono ospitare altri carichi di lavoro di messaggistica istantanea e presenza o VoIP aziendale. Inoltre, non devono ospitare altre riunioni, non importa quanto grandi. Questo significa che per ospitare riunioni con un massimo di 1000 utenti è necessario configurare un pool Lync Server separato dedicato.

Un pool Lync Server destinato a ospitare riunioni di grandi dimensioni deve ospitare una e una sola riunione con un massimo di 1000 utenti alla volta, ed è quindi necessario prenotare in anticipo gli orari delle riunioni tramite un processo di programmazione fuori banda per garantire il supporto specifico da parte dei Front End Server. Per supportare più riunioni di grandi dimensioni contemporaneamente, si consiglia di configurare più pool dedicati.

Si consiglia inoltre di dedicare una persona all'esecuzione e al monitoraggio della parte online delle riunioni di grandi dimensioni. Questa persona può essere l'organizzatore, un delegato dell'organizzatore o del relatore o un membro del team di supporto alle riunioni di grandi dimensioni, a seconda delle preferenze dell'organizzazione.

Nelle sezioni seguenti è descritto come implementare un pool dedicato per le riunioni di grandi dimensioni. Sono illustrate anche le procedure consigliate per l'uso di Lync Server 2013 negli scenari di riunioni di questo tipo.

## Argomenti della sezione

  - [Configurazione del supporto per le riunioni di grandi dimensioni](lync-server-2013-setting-up-support-for-large-meetings.md)

  - [Gestione di riunioni di grandi dimensioni](lync-server-2013-managing-large-meetings.md)

