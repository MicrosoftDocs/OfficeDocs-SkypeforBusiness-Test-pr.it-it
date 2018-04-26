---
title: 'Lync Server 2013: Funzionalità di resilienza dei siti di succursale'
TOCTitle: Funzionalità di resilienza dei siti di succursale
ms:assetid: 8e3feda5-9a38-4e3c-b808-af29f19c5eb9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398715(v=OCS.15)
ms:contentKeyID: 49301281
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Funzionalità di resilienza dei siti di succursale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-02-10_

Se si fornisce la resilienza dei siti derivati, in caso di errore della connessione WAN di un sito derivato con un sito centrale o qualora il sito centrale non sia raggiungibile, le funzionalità vocali seguenti devono continuare a essere disponibili:


  - Chiamate PSTN in entrata e in uscita

  - Chiamate Enterprise tra utenti dello stesso sito e di due siti diversi

  - Gestione di base delle chiamate inclusi la messa in attesa, il recupero e il trasferimento

  - Messaggistica istantanea tra due parti

  - Inoltro di chiamata, squillo simultaneo degli endpoint, delega delle chiamate e servizi di intercettazione team, ma solo se delegante e delegato (ad esempio un capo e l'amministratore del capo), oppure tutti i membri del team, sono configurati nello stesso sito

  - Registrazione dettagli chiamata (CDR)

  - Conferenze telefoniche con accesso esterno PSTN con Operatore automatico conferenza

  - Funzionalità di segreteria telefonica, se si configurano le impostazioni di rerouting della segreteria telefonica. (Per informazioni dettagliate, vedere [Requisiti di resilienza dei siti di succursale per Lync Server 2013](lync-server-2013-branch-site-resiliency-requirements.md).)

  - Autenticazione e autorizzazione utente

Le funzionalità seguenti saranno disponibili solo se la soluzione di resilienza in uso è una distribuzione completa di Lync Server nel sito di succursale:

  - Conferenze di messaggistica istantanea, Web e audio/video

  - Routing in base a presenza e Non disturbare (le chiamate non squillano agli interni che hanno il Non disturbare attivato)

  - Aggiornamento delle impostazioni di inoltro di chiamata.

  - applicazione Response Group e applicazione Parcheggio di chiamata

  - Provisioning di nuovi telefoni e client, ma solo se Servizi di dominio Active Directory è presente nel sito di succursale.

  - Enhanced 9-1-1 (E9-1-1)
    
    Se è stato distribuito Enhanced 9-1-1 (E9-1-1) e il trunk SIP del sito centrale non è disponibile perché il collegamento WAN non è attivo, Survivable Branch Appliance eseguirà il routing delle chiamate E9-1-1 al gateway della succursale locale. Per abilitare questa funzionalità, i criteri vocali degli utenti del sito di succursale devono eseguire il routing delle chiamate al gateway locale in caso di errore della WAN.


> [!NOTE]
> SBA (Survivable Branch Appliance) non è supportato per XMPP. Gli utenti ospitati in configurazioni SBA non potranno inviare messaggi istantanei o visualizzare la presenza dei contatti XMPP.


