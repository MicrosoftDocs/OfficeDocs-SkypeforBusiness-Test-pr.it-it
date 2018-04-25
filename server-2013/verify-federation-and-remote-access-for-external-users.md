---
title: Verificare la federazione e l'accesso remoto per gli utenti esterni
TOCTitle: Verificare la federazione e l'accesso remoto per gli utenti esterni
ms:assetid: a383fefb-c428-4462-93fd-15ba540fa867
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688163(v=OCS.15)
ms:contentKeyID: 49887689
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verificare la federazione e l'accesso remoto per gli utenti esterni

 

_**Ultima modifica dell'argomento:** 2012-09-18_

Dopo aver effettuato la transizione della route di federazione nel server perimetrale di Lync Server 2013, è consigliabile eseguire alcuni test funzionali per verificare che la federazione funzioni nel modo previsto. I test per l'accesso utenti esterni devono includere ogni tipo di utente esterno supportato dall'organizzazione, inclusi alcuni o tutti quelli indicati di seguito.

## Verificare la connettività degli utenti esterni e l'accesso esterno

  - Utenti di almeno un dominio federato, un utente interno in Lync Server 2013 e un utente in Lync Server 2010. Testare la messaggistica istantanea, il traffico audio/video e la condivisione del desktop.

  - Utenti di ogni provider di servizi di messaggistica istantanea supportato dall'organizzazione (e per cui sia stato completato il provisioning) che comunicano con un utente in Lync Server 2013 e un utente in Lync Server 2010.

  - Verificare che gli utenti anonimi siano in grado di partecipare alle conferenze.

  - Utente ospitato in Lync Server 2010 che utilizza accesso utente remoto (accedendo a Lync Server 2010 dall'esterno della rete Intranet ma senza VPN) con un utente in Lync Server 2013 e un utente in Lync Server 2010. Testare la messaggistica istantanea, la presenza, il traffico audio/video e la condivisione del desktop.

  - Utente ospitato in Lync Server 2013 che utilizza accesso utente remoto (accedendo a Lync Server 2013 dall'esterno della rete Intranet ma senza VPN) con un utente in Lync Server 2013 e un utente in Lync Server 2010. Testare la messaggistica istantanea, la presenza, il traffico audio/video e la condivisione del desktop.

