---
title: 'Lync Server 2013: Supporto del protocollo di rete e IP'
TOCTitle: Supporto del protocollo di rete e IP
ms:assetid: b0cffb10-3478-445c-89c7-8cb8b5027424
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412848(v=OCS.15)
ms:contentKeyID: 49301685
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Supporto del protocollo di rete e IP in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

Lync Server 2013 supporta i protocolli IP e di rete seguenti:

  - **Protocolli IP.**    Lync Server 2013 supporta IP versione 4 (IPv4) o IP versione 6 (IPv6) per la rete di server.
    

    > [!NOTE]
    > Lync Server 2013 può funzionare in una rete con un dual stack IP abilitato.



  - **Protocolli di trasporto SIP.**   In genere, SIP può utilizzare almeno tre tipi di trasporto: UDP (User Datagram Protocol), TCP (Transmission Control Protocol) e TLS (Transport Layer Security). Nella configurazione predefinita del trasporto SIP, TLS viene eseguito su TCP. TLS viene utilizzato all'interno della rete di Lync Server 2013. Nella rete perimetrale Lync Server 2013 può interagire tramite TCP. Lync Server 2013 non supporta UDP per il trasporto SIP perché non soddisfa gli standard minimi per la scalabilità, l'affidabilità e la sicurezza delle comunicazioni aziendali. Per informazioni dettagliate, vedere l'articolo del blog NextHop sulla scelta di utilizzare o meno UDP all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=185369](http://go.microsoft.com/fwlink/p/?linkid=185369).
    

    > [!NOTE]
    > Il contenuto di ogni blog e i relativi URL sono soggetti a modifiche senza preavviso.


