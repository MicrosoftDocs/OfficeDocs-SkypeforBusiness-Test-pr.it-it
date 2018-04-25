---
title: 'Lync Server 2013: Funzionalità della messaggistica unificata integrata'
TOCTitle: Funzionalità della messaggistica unificata integrata e Lync Server
ms:assetid: 094f549d-fccc-43ab-9f39-6ddd18130915
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398144(v=OCS.15)
ms:contentKeyID: 49299615
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Funzionalità della messaggistica unificata integrata e Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-01_

VoIP aziendale di Lync Server 2013 utilizza l'infrastruttura della Messaggistica unificata di Exchange per fornire servizi di risponditore automatico, notifica di chiamata, accesso vocale (inclusa la segreteria telefonica) e operatore automatico.

## Risponditore automatico

Il risponditore automatico riceve messaggi vocali per conto di utenti occupati o che non hanno risposto a una chiamata. Questa funzionalità prevede la riproduzione di un messaggio di saluto personale, la registrazione di un messaggio e l'invio del messaggio in coda per il recapito alla cassetta postale dell'utente archiviata nel server Cassette postali di Exchange.

L'eventuale messaggio lasciato da un chiamante viene instradato alla cartella Posta in arrivo dell'utente. Se invece un chiamante sceglie di non lasciare messaggi, nella cassetta postale dell'utente viene archiviata una notifica di chiamata non risposta. Gli utenti possono quindi accedere alla rispettiva cartella Posta in arrivo utilizzando il client di messaggistica e collaborazione Microsoft Office Outlook, Outlook Web Access, la tecnologia Exchange ActiveSync o Outlook Voice Access. L'oggetto e la priorità delle chiamate possono essere visualizzati in modo simile a quelli di un messaggio di posta elettronica.

## Outlook Voice Access

Outlook Voice Access consente a un utente di VoIP aziendale di accedere non solo alla segreteria telefonica, ma anche alla Posta in arrivo di Exchange, inclusi i messaggi di posta elettronica, il calendario e i contatti, da un'interfaccia di telefonia. Il numero di accesso del sottoscrittore viene assegnato da un amministratore della Messaggistica unificata di Exchange.

## Operatore automatico

L'operatore automatico è una funzionalità della Messaggistica unificata di Exchange che è possibile utilizzare per configurare un numero di telefono che utenti esterni possono comporre per raggiungere i dipendenti della società. In particolare, fornisce una serie di istruzioni vocali che consentono a un chiamante esterno di spostarsi in un sistema di menu. L'elenco delle opzioni disponibili viene configurato nel server di Messaggistica unificata di Exchange dall'amministratore della Messaggistica unificata di Exchange.

## Servizi fax

La Messaggistica unificata di Exchange include funzionalità fax che consentono agli utenti di ricevere i fax in arrivo nelle rispettive cassette postali di Exchange. Per informazioni dettagliate, vedere la pagina relativa alla messaggistica unificata nella documentazione di Microsoft Exchange Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=135652](http://go.microsoft.com/fwlink/p/?linkid=135652).


> [!NOTE]
> I servizi fax offerti dal server di messaggistica unificata di Exchange non sono disponibili nelle distribuzioni di Lync Server integrate con Microsoft Exchange Server 2010, Exchange 2010 con il Service Pack più recente o Exchange 2013.


