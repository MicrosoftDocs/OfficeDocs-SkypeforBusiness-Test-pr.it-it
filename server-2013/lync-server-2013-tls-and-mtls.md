---
title: TLS e MTLS per Lync Server 2013
TOCTitle: TLS e MTLS per Lync Server 2013
ms:assetid: b32a5b85-fc82-42dc-a9b2-96400f8cd2b8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn481133(v=OCS.15)
ms:contentKeyID: 59679243
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# TLS e MTLS per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-11-07_

I protocolli TLS (Transport Layer Security) e MTLS (Mutual Transport Layer Security) consentono di eseguire comunicazioni crittografate e di effettuare l'autenticazione degli endpoint tramite Internet. Microsoft Lync Server 2013 utilizza questi due protocolli per creare una rete di server attendibili e assicurare che tutte le comunicazioni in tale rete siano crittografate. Tutte le comunicazioni SIP tra i server avvengono tramite MTLS. Le comunicazioni SIP da client a server avvengono tramite TLS.

TLS consente agli utenti di autenticare i server Lync Server 2013 a cui si connettono attraverso il proprio software client. In una connessione TLS, il client richiede al server un certificato valido. Per essere valido, il certificato deve essere stato emesso da una CA considerata attendibile anche dal client e il nome DNS del server deve corrispondere al nome DNS nel certificato. Se il certificato è valido, il client utilizza la chiave pubblica nel certificato per crittografare le chiavi di crittografia simmetrica da utilizzare per la comunicazione, in modo che solo il proprietario originale del certificato possa utilizzare la propria chiave privata per decrittografare i contenuti della comunicazione. La connessione che si viene a creare è dunque ritenuta attendibile e non viene verificata da altri server o client attendibili. In questo contesto, è possibile associare i certificati SSL (Secure Sockets Layer) utilizzati con i servizi Web come certificati basati su TLS.

Le connessioni tra server si basano su MTLS per l'autenticazione reciproca. In una connessione MTLS, il server che invia il messaggio e il server che lo riceve scambiano i propri certificati tramite una CA ritenuta affidabile da entrambi. I certificati dimostrano l'identità di ciascun server all'altro. Nelle distribuzioni di Lync Server 2013, i certificati emessi da una CA globale (enterprise) che si trovano nel periodo di validità e non sono stati revocati dalla CA emittente vengono considerati automaticamente validi da tutti i client e i server interni, perché tutti i membri del dominio Active Directory ritengono attendibile la CA globale (enterprise) in quel dominio. Negli scenari federati, è necessario che la CA emittente sia ritenuta attendibile da entrambi i partner federati. Ogni partner può utilizzare una CA diversa, se lo desidera, purché anche tale CA sia ritenuta attendibile dall'altro partner. Questa attendibilità può essere ottenuta rapidamente dai server perimetrali che presentano il certificato CA radice del partner nelle proprie CA radice attendibili oppure tramite l'utilizzo di una CA di terze parti ritenuta attendibile da entrambe le parti.

TLS e MTLS permettono di impedire attacchi man-in-the-middle e di eavesdropping. In un attacco man-in-the-middle, l'autore dell'attacco reindirizza le comunicazioni tra due entità di rete tramite il proprio computer senza che l'altra parte ne sia consapevole. TLS e la specifica dei server attendibili di Lync Server 2013 (solo quelli specificati nel Generatore di topologie) riducono parzialmente il rischio di un attacco man-in-the middle a livello dell'applicazione utilizzando la crittografia end-to-end coordinata tramite la crittografia della chiave pubblica tra i due endpoint. L'autore dell'attacco, infatti, per decrittografare la comunicazione dovrebbe possedere un certificato valido e ritenuto attendibile con la chiave privata corrispondente, emesso con il nome del servizio con cui il client sta comunicando. È comunque necessario seguire le procedure di sicurezza consigliate per la propria infrastruttura di rete (in questo caso il DNS aziendale). Lync Server 2013 presuppone che il server DNS sia attendibile nello stesso modo in cui ritiene attendibili i controller di dominio e i cataloghi globali. DNS, tuttavia, fornisce effettivamente un livello di protezione dagli attacchi per assumere il controllo di DNS impedendo al server dell'autore dell'attacco di rispondere a una richiesta con un nome falsificato.

Nella figura seguente viene mostrato in che modo Lync Server 2013 utilizza MTLS per creare una rete di server attendibili.

**Connessioni attendibili in una rete Lync Server**

![Uso di MTLS](images/Dn481133.437749da-c372-4f0d-ac72-ccfd5191696b(OCS.15).jpg "Uso di MTLS")

