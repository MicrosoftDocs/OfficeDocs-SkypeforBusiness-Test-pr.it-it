---
title: 'Lync Server 2013: Implementazione della connettività PSTN in un sito di succursale'
TOCTitle: Implementazione della connettività PSTN in un sito di succursale
ms:assetid: d78d76fb-2dd1-42cb-b25a-bfaff9650a70
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398945(v=OCS.15)
ms:contentKeyID: 49302125
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Implementazione della connettività PSTN in un sito di succursale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-05_

È consigliabile utilizzare Microsoft Lync Server 2013, Strumento di pianificazione per aggiungere siti di succursale alla topologia e impostare l'infrastruttura vocale nei siti di succursale.

Se non si utilizza lo Strumento di pianificazione, eseguire le procedure descritte negli argomenti di questa sezione per aggiungere innanzitutto i siti di succursale e quindi per impostare l'infrastruttura vocale definendo il gateway IP/PSTN (Public Switched Telephone Network) e/o configurando il trunk SIP (con o senza bypass multimediale). Un'altra opzione consiste nel connettere un PBX (Private Branch Exchange, centralino) al sito di succursale.


> [!NOTE]
> Se si desidera fornire resilienza dei siti di succursale, è necessario distribuire un Survivable Branch Appliance, un Survivable Branch Server o un server Standard Edition nel sito di succursale. Per informazioni dettagliate, vedere <A href="lync-server-2013-deploying-a-survivable-branch-appliance-or-server.md">Distribuzione di Survivable Branch Appliance o Survivable Branch Server con Lync Server 2013</A> o <A href="lync-server-2013-deploying-lync-server.md">Distribuzione di Lync Server 2013</A> a seconda dei casi nella documentazione relativa alla distribuzione.



## Argomenti della sezione

  - [Aggiungere siti di succursale alla topologia in Lync Server 2013](lync-server-2013-add-branch-sites-to-your-topology.md)

  - [Definire un gateway PSTN per un sito di succursale in Lync Server 2013](lync-server-2013-define-a-pstn-gateway-for-a-branch-site.md)

  - [Configurare un trunk con bypass multimediale in Lync Server 2013](lync-server-2013-configure-a-trunk-with-media-bypass.md)

  - [Configurare un trunk senza bypass multimediale in Lync Server 2013](lync-server-2013-configure-a-trunk-without-media-bypass.md)

## Vedere anche

#### Ulteriori risorse

[Pianificazione del bypass multimediale in Lync Server 2013](lync-server-2013-planning-for-media-bypass.md)  
[Pianificazione per la connettività PSTN in Lync Server 2013](lync-server-2013-planning-for-pstn-connectivity.md)

