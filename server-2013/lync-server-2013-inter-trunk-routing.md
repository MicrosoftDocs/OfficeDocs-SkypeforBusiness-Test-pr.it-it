---
title: 'Lync Server 2013: Routing tra trunk'
TOCTitle: Routing tra trunk
ms:assetid: f687a548-1f2e-48ed-9745-a13dc1f3698f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721940(v=OCS.15)
ms:contentKeyID: 49887830
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Routing tra trunk in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-08_

Lync Server 2013 fornisce la gestione di base delle sessioni mediante il supporto del routing tra trunk. Questa nuova funzionalità consente a Lync Server di offrire le funzionalità di controllo delle chiamate ai sistemi di telefonia downstream. Il routing tra trunk può collegare un IP-PBX a un gateway PSTN (Public Switched Telephone Network) in modo che le chiamate da un telefono PBX (Private Branch Exchange) possano essere instradate verso la rete PSTN e le chiamate in entrata alla rete PSTN possano essere instradate verso un telefono PBX. Analogamente, Lync Server può collegare due o più sistemi IP-PBX in modo da consentire di effettuare e ricevere chiamate tra telefoni PBX dai diversi sistemi IP-PBX.

Nella figura seguente è illustrata la modalità di interconnettività offerta da Lync Server 2013 tra un gateway PSTN e un IP-PBX.

![Diagramma delle connessioni tra Lync Server e gateway PSTN/IP-PBX](images/JJ721940.cc3858ca-2ee3-4d51-8a51-db078366b50b(OCS.15).jpg "Diagramma delle connessioni tra Lync Server e gateway PSTN/IP-PBX")

Nella figura seguente è illustrata la connessione di due sistemi IP-PBX mediante Lync Server 2013.

![Diagramma delle interconnessioni tra Lync Server e sistemi IP-PAX](images/JJ721940.6ba18ec9-df70-498a-9cf7-7fc41e5ec432(OCS.15).jpg "Diagramma delle interconnessioni tra Lync Server e sistemi IP-PAX")

