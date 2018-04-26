---
title: Associare subnet a siti di rete per bypass multimediale
TOCTitle: Associare subnet a siti di rete per bypass multimediale
ms:assetid: 5bc632b7-1446-470f-b332-48ea0ca4d1fd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398401(v=OCS.15)
ms:contentKeyID: 49300660
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Associare subnet a siti di rete per bypass multimediale

 

_**Ultima modifica dell'argomento:** 2012-09-12_


> [!NOTE]
> In questo argomento si presuppone che siano state configurate impostazioni globali per la funzionalità Media Bypass e che siano stati configurati l'area di rete e i siti di rete per tale funzionalità.



Ogni subnet della rete deve essere associata a un sito di rete specifico. Le informazioni della subnet, infatti, vengono utilizzate per determinare il sito di rete in cui si trova un endpoint. Quando sono note le posizioni di entrambe le parti di una sessione, il bypass multimediale consente di determinare dove inviare gli elementi multimediali per l'elaborazione.

Per il bypass multimediale non esistono requisiti speciali per l'associazione di subnet a siti di rete. Per creare un'associazione tra le subnet e i siti di rete nella topologia, seguire le procedure in [Associare una subnet a un sito di rete in Lync Server 2013](lync-server-2013-associate-a-subnet-with-a-network-site.md).

## Passaggi successivi: creare profili di criteri di larghezza di banda

Dopo aver associato le subnet ai siti di rete per il bypass multimediale, è necessario creare uno o più profili di criteri di larghezza di banda per suddividere le subnet tra quelle con connettività di buon livello e quelle senza, ai fini del bypass multimediale. Tutte le subnet in un'area di rete con siti di rete che non hanno limiti di larghezza di banda dispongono di connettività di buon livello e possono pertanto utilizzare il bypass multimediale.

Per informazioni sulle procedure per la configurazione dei profili di criteri di larghezza di banda, vedere [Creare profili di criteri di larghezza di banda](lync-server-2013-create-bandwidth-policy-profiles.md).

