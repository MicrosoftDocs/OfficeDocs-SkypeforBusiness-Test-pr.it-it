---
title: "Lync Server 2013: Requisiti dell'infrastruttura dei certificati"
TOCTitle: Requisiti dell'infrastruttura dei certificati
ms:assetid: 0051aa23-0bbe-4e72-9f29-e01c6bcc6190
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398066(v=OCS.15)
ms:contentKeyID: 49299478
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti dell'infrastruttura dei certificati per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-03-22_

Lync Server 2013 richiede un'infrastruttura a chiave pubblica (PKI) per supportare connessioni TLS e MTLS (Mutual TLS).

Lync Server utilizza certificati per gli scopi seguenti:

  - Connessioni TLS tra client e server

  - Connessioni MTLS tra server

  - Federazione con individuazione DNS automatica dei partner

  - Accesso utente remoto per la messaggistica istantanea

  - Accesso utente esterno a sessioni audio/video (A/V), condivisione applicazioni e conferenze

  - Richieste mobili con individuazione automatica dei servizi Web

Per Lync Server si applicano i requisiti comuni seguenti:

  - Tutti i certificati del server devono supportare l'autorizzazione server (utilizzo chiavi avanzato del server).

  - Tutti i certificati del server devono contenere un punto di distribuzione CRL (CDP).

  - Tutti i certificati devono essere firmati mediante un algoritmo di firma supportato dal sistema operativo. Lync Server 2013 supporta i gruppi di dimensioni del digest SHA-1 e SHA-2 (a 224, 256, 384 e 512 bit) e soddisfa i requisiti del sistema operativo o dispone di requisiti superiori a quelli richiesti. Per il supporto del sistema operativo, vedere [http://go.microsoft.com/fwlink/?LinkId=287002](http://go.microsoft.com/fwlink/?linkid=287002).

  - La registrazione automatica è supportata per i server interni che eseguono Lync Server.

  - La registrazione automatica non è supportata per i server perimetrali Lync Server.

  - Quando si invia una richiesta di certificato Web a un'autorità di certificazione (CA) di Windows Server 2003, è necessario inviarla da un computer che esegue Windows Server 2003 con SP2 oppure Windows XP.
    
    Benché nell'articolo KB922706 venga fornito il supporto per risolvere i problemi di registrazione dei certificati Web con la funzionalità di registrazione Web dei Servizi certificati di Windows Server 2003, non è possibile utilizzare Windows Server 2008, Windows Vista o Windows 7 per richiedere un certificato a una CA di Windows Server 2003.

  - Le lunghezze supportate per le chiavi di crittografia sono 1024, 2048 e 4096. È consigliabile utilizzare chiavi di lunghezza uguale o superiore a 2048.

  - L'algoritmo di firma hash o digest predefinito è RSA. Sono inoltre supportati gli algoritmi ECDH\_P256, ECDH\_P384 ed ECDH\_P521. 

## Argomenti della sezione

  - [Requisiti dei certificati per i server interni in Lync Server 2013](lync-server-2013-certificate-requirements-for-internal-servers.md)

  - [Requisiti dei certificati per l'accesso utente esterno in Lync Server 2013](lync-server-2013-certificate-requirements-for-external-user-access.md)

  - [Requisiti dei certificati per il server Chat persistente in Lync Server 2013](lync-server-2013-certificate-requirements-for-persistent-chat-server.md)

  - [Requisiti dei certificati per i dispositivi mobili in Lync Server 2013](lync-server-2013-certificate-requirements-for-mobility.md)

