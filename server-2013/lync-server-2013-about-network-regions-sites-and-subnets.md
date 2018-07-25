---
title: 'Lync Server 2013: Informazioni su aree di rete, siti e subnet'
TOCTitle: Informazioni su aree di rete, siti e subnet
ms:assetid: 6662123a-d011-408c-a290-92b2a8589943
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398467(v=OCS.15)
ms:contentKeyID: 49300817
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Informazioni su aree di rete, siti e subnet in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-24_

Le funzionalità di VoIP aziendale avanzate illustrate in questa sezione hanno in comune alcuni requisiti di configurazione per le aree di rete, i siti di rete e le subnet. Ad esempio, tutte e tre le funzionalità avanzate richiedono che ogni subnet della topologia sia associata a un *sito di rete* specifico e che ogni sito di rete debba essere associato a un' *area di rete* .

> [!important]  
> Prima di iniziare a configurare la rete per il controllo di ammissione di chiamata, il servizio E9-1-1 o il bypass multimediale, assicurarsi di aver consultato le informazioni aggiuntive sulle impostazioni di rete nell'argomento <a href="lync-server-2013-network-settings-for-the-advanced-enterprise-voice-features.md">Impostazioni di rete per le funzionalità di VoIP aziendale avanzate in Lync Server 2013</a> nella documentazione relativa alla pianificazione. Per informazioni dettagliate sulla configurazione di rete in particolare per il controllo di ammissione di chiamata, vedere anche <a href="lync-server-2013-defining-your-requirements-for-call-admission-control.md">Definizione dei requisiti dell'organizzazione per il controllo di ammissione di chiamata in Lync Server 2013</a> nella documentazione relativa alla pianificazione.

Per il controllo di ammissione di chiamata e il servizio E9-1-1 sono previsti ulteriori requisiti di configurazione per i siti di rete:

  - Per il controllo di ammissione di chiamata è necessario specificare un *profilo di criteri di larghezza di banda* per ogni sito vincolato da limitazioni della larghezza di banda WAN. Se si prevede di distribuire il controllo di ammissione di chiamata, è necessario [Creare profili di criteri di larghezza di banda](lync-server-2013-create-bandwidth-policy-profiles.md) prima di configurare i siti di rete.

  - Per il servizio E9-1-1 è necessario specificare *criteri di percorso* per ogni sito. Se si prevede di distribuire il servizio E9-1-1, è necessario [Creare criteri percorso in Lync Server 2013](lync-server-2013-create-location-policies.md) prima di configurare i siti di rete.

## Creare o modificare aree di rete, siti di rete e subnet

Gli argomenti seguenti descrivono le procedure per creare e modificare aree di rete e siti di rete, nonché per associare subnet a siti di rete. Questi argomenti non sono specifici per alcuna funzionalità VoIP aziendale avanzata particolare.

  - [Creare o modificare un'area di rete in Lync Server 2013](lync-server-2013-create-or-modify-a-network-region.md)

  - [Creare o modificare un sito di rete in Lync Server 2013](lync-server-2013-create-or-modify-a-network-site.md)

  - [Associare una subnet a un sito di rete in Lync Server 2013](lync-server-2013-associate-a-subnet-with-a-network-site.md)

