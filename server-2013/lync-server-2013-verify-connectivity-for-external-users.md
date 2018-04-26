---
title: 'Lync Server 2013: Verificare la connettività per gli utenti esterni'
TOCTitle: Verificare la connettività per gli utenti esterni
ms:assetid: 5c02bd6e-1c96-448a-a21d-58c9961c6640
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398402(v=OCS.15)
ms:contentKeyID: 49300668
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verificare la connettività per gli utenti esterni in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-19_

La convalida della connettività per gli utenti esterni garantisce la connettività dagli utenti al server e alla porta per il servizio Access Edge.

Il sito Remote Connectivity Analyzer ( <https://www.testocsconnectivity.com/>) è una risorsa preziosa per verificare la configurazione e la possibilità di connettersi e inviare e ricevere i messaggi corretti per gli scenari richiesti per l'accesso di utenti esterni. Il sito viene gestito e mantenuto aggiornato dal Servizio Supporto Tecnico Clienti Microsoft. Per accedere a Remote Connectivity Analyzer, aprire il sito Web in un browser e seguire le istruzioni per selezionare lo scenario.

## Verificare la connettività degli utenti esterni e l'accesso esterno

I test per l'accesso utente esterno devono includere ogni tipo di utente esterno supportato dall'organizzazione, inclusi alcuni o tutti quelli indicati di seguito:

  - Utenti da almeno un dominio federato, con testing di messaggistica istantanea, presenza, audio/video e condivisione del desktop.

  - Utenti di ogni provider di servizi di messaggistica istantanea pubblica supportati dall'organizzazione e per i quali è stato completato il provisioning.

  - Utenti anonimi.

  - Utenti nell'organizzazione connessi a Lync in remoto, ma che non utilizzano una rete VPN.

Questi test determinano se il server perimetrale:

  - È in attesa sulle porte necessarie tramite un client telnet dall'esterno della rete.
    
      - Esempio: telnet sip.contoso.com 443
    
      - Eseguire il test precedente sulle porte utilizzate nel server perimetrale o nel pool di server perimetrali, a seconda della distribuzione.

  - Esegue la risoluzione DNS esterna in modo accurato.
    
      - Dall'esterno della rete, eseguire il ping di ognuno degli FQDN esterni del server perimetrale o del pool di server perimetrali. Anche se il ping non riesce verranno visualizzati gli indirizzi IP, confrontabili con quelli assegnati.

