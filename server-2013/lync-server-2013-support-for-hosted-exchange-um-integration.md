---
title: "Lync Server 2013: Supporta integraz. di messaggistica di Exchange ospitata"
TOCTitle: Supporto per l'integrazione di messaggistica unificata di Exchange ospitata
ms:assetid: c7573ec3-013c-48d9-b59b-2a5427e6da35
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398821(v=OCS.15)
ms:contentKeyID: 49301954
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Supporto per l'integrazione di messaggistica unificata di Exchange ospitata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

L'applicazione di routing della messaggistica unificata di Exchange di Lync Server 2013 supporta l'integrazione con il servizio Messaggistica unificata di Exchange in un ambiente locale, dove Lync Server 2013 e il servizio Messaggistica unificata di Exchange sono entrambi installati in locale nell'organizzazione oppure con il servizio Messaggistica unificata di Exchange ospitato da un provider di servizi, come illustrato nella figura seguente.

![Distribuzione della messaggistica unificata di Exchange con Lync Server in locale](images/Gg398821.d6498eb9-87ee-40f3-8ecd-852f91546590(OCS.15).jpg "Distribuzione della messaggistica unificata di Exchange con Lync Server in locale")

Sono supportate le modalità seguenti:

  - **Modalità locale**    Lync Server 2013 e Messaggistica unificata di Exchange sono entrambi distribuiti in server locali all'interno dell'azienda.

  - **Modalità cross-premise**    Lync Server 2013 viene distribuito nei server locali all'interno dell'azienda e il servizio Messaggistica unificata di Exchange viene ospitato in una struttura di un provider di servizi online, ad esempio un data center di Microsoft Exchange Online.

  - **Modalità mista**   La distribuzione di Lync Server 2013 dispone di alcune cassette postali utente nei server locali che eseguono Microsoft Exchange Server all'interno dell'azienda e di alcune cassette postali in un data center di un servizio di Exchange ospitato.
    

    > [!NOTE]
    > È possibile utilizzare la modalità mista come soluzione di transizione durante la valutazione e la migrazione graduale degli utenti al servizio Messaggistica unificata di Exchange ospitato oppure come soluzione permanente se si decide di mantenere i servizi Messaggistica unificata di Exchange di alcuni utenti in locale dopo aver eseguito la migrazione di altri.



Per integrare Lync Server 2013 con il servizio Messaggistica unificata di Exchange ospitato, è necessario configurare uno *spazio di indirizzi SIP condiviso* , denominato anche *dominio diviso* . In questa configurazione sia Lync Server 2013 che il provider di servizi Messaggistica unificata di Exchange ospitati di terze parti possono accedere allo stesso spazio di indirizzi del dominio SIP. Per informazioni dettagliate, vedere [Architettura dell'integrazione della messaggistica unificata di Exchange ospitata in Lync Server 2013](lync-server-2013-hosted-exchange-um-integration-architecture.md) nella documentazione relativa alla pianificazione.

