---
title: 'Lync Server 2013: Routing tra trunk'
TOCTitle: Routing tra trunk
ms:assetid: d3a33b4a-8bf4-4a8c-a371-8ef79e740780
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205272(v=OCS.15)
ms:contentKeyID: 49302068
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Routing tra trunk in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-20_

Lync Server 2013 può interconnettere un sistema IP-PBX e un gateway PSTN (Public Switched Telephone Network) in modo che le chiamate da un telefono PBX possano essere instradate alla rete PSTN e le chiamate PSTN in arrivo possano essere instradate a un telefono PBX. Analogamente, Lync Server 2013 può interconnettere due o più sistemi IP-PBX in modo che sia possibile effettuare e ricevere chiamate tra i telefoni PBX dei diversi sistemi IP-PBX.

Questa funzionalità di routing tra trunk può essere configurata utilizzando il cmdlet **set-cstrunkconfiguration** di Lync Server Management Shell con il nuovo parametro PstnUsages. Questo parametro specifica l'insieme di record di utilizzo PSTN da applicare. Un trunk si basa su questo utilizzo PSTN per determinare una route e per instradare tutte le chiamate in arrivo di conseguenza.

    set-cstrunkconfiguration -Identity <TrunkId> -PstnUsages @{add="<UsageString>"}

Nella figura seguente viene illustrato Lync Server 2013 che interconnette un gateway PSTN e un sistema IP-PBX.

**Routing tra trunk tra gateway e IP-PBX**

![Diagramma delle connessioni tra Lync Server e gateway PSTN/IP-PBX](images/JJ721940.cc3858ca-2ee3-4d51-8a51-db078366b50b(OCS.15).jpg "Diagramma delle connessioni tra Lync Server e gateway PSTN/IP-PBX")

Nella figura seguente viene illustrato Lync Server 2013 che interconnette due sistemi IP-PBX.

**Routing tra trunk tra due sistemi IP-PBX**

![Diagramma delle interconnessioni tra Lync Server e sistemi IP-PAX](images/JJ721940.6ba18ec9-df70-498a-9cf7-7fc41e5ec432(OCS.15).jpg "Diagramma delle interconnessioni tra Lync Server e sistemi IP-PAX")

