---
title: Configurazione dei requisiti per il proxy inverso in Lync Server 2013
TOCTitle: Configurazione dei requisiti per il proxy inverso in Lync Server 2013
ms:assetid: c37d688a-28e4-4822-80cc-6add59c71052
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945651(v=OCS.15)
ms:contentKeyID: 52062308
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione dei requisiti per il proxy inverso in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-03-05_

Lync Server 2013 impone alcuni requisiti per le comunicazioni dal client esterno che vengono quindi passate ai servizi Web esterni ospitati nel Server Director, nel pool di server Director, nel Front End Server o nel pool Front End. Se agli utenti viene offerto un servizio conferenze, il proxy inverso è inoltre responsabile della pubblicazione di Server Office Web Apps.


> [!NOTE]
> Per Lync Server 2013 non è necessario utilizzare un particolare proxy inverso. Lync Server 2013 definisce solo i requisiti operativi che il proxy inverso deve soddisfare. Il proxy inverso già distribuito nell'infrastruttura soddisfa in genere i requisiti.



## Requisiti relativi al proxy inverso

Le operazioni funzionali che un proxy inverso deve eseguire per Lync Server 2013 sono le seguenti:

  - Utilizzare SSL (Secure Socket Layer) e TLS (Transport Layer Security) implementati utilizzando i certificati acquisiti da un'autorità di certificazione pubblica per connettersi ai servizi Web esterni pubblicati del Server Director, del pool di server Director, del Front End Server o del pool Front End. Il Server Director e il Front End Server possono trovarsi in un pool con carico bilanciato grazie ai dispositivi di bilanciamento del carico hardware.

  - Essere in grado di pubblicare i siti Web interni utilizzando i certificati per la crittografia o di pubblicarli in modo non crittografato, se necessario.

  - Essere in grado di pubblicare esternamente un sito Web ospitato internamente utilizzando un nome di dominio completo (FQDN).

  - Essere in grado di pubblicare tutti i contenuti del sito Web ospitato. Per impostazione predefinita, è possibile utilizzare la direttiva **/\*** che nella maggior parte dei server Web viene interpretata come una richiesta di pubblicare tutto il contenuto nel server Web. È inoltre possibile modificare la direttiva. **/Uwca/\***, ad esempio, indica di pubblicare tutto il contenuto nella directory virtuale Ucwa.

  - Deve essere configurabile in modo che siano necessarie connessioni SSL (Secure Sockets Layer) e/o TLS (Transport Layer Security) con i client che richiedono contenuto da un sito Web pubblicato.

  - Deve accettare i certificati con voci di nome alternativo soggetto (SAN).

  - Deve consentire il binding di un certificato a un listener o a un'interfaccia tramite cui verrà risolto il nome FQDN dei servizi Web esterni. Le configurazioni listener sono preferibili alle interfacce. È possibile configurare più listener in una sola interfaccia.

  - Deve consentire la configurazione della gestione delle intestazioni host. L'intestazione host originale inviata dal client richiedente deve spesso essere passata in modo trasparente, anziché essere modificata dal proxy inverso.

  - Bridging del traffico SSL e TLS da una porta definita esternamente (ad esempio, TCP 443) a un'altra porta definita (ad esempio, TCP 4443). Il proxy inverso può decrittografare il pacchetto al momento della ricezione e quindi crittografarlo nuovamente al momento dell'invio.

  - Bridging del traffico TCP non crittografato da una porta (ad esempio, TCP 80) a un'altra (ad esempio, TCP 8080).

  - Consentire la configurazione per nessuna autenticazione e per l'autenticazione pass-through.

