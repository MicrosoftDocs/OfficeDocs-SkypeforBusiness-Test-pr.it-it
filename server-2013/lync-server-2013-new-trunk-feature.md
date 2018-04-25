---
title: 'Lync Server 2013: Nuova funzionalità trunk'
TOCTitle: Nuova funzionalità trunk
ms:assetid: 9b398bc8-2760-4218-b1a4-89b9694b1171
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688152(v=OCS.15)
ms:contentKeyID: 49887674
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Nuova funzionalità trunk in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

In Microsoft Lync Server 2013, è possibile definire più trunk tra un Mediation Server e un gateway. Microsoft Lync Server 2010 consente di disporre di un singolo trunk tra un Mediation Server e un gateway PSTN. Questa funzionalità offre la flessibilità per definire trunk aggiuntivi. Un trunk è un'associazione logica tra un FQDN e una porta di ascolto del Mediation Server e un FQDN e una porta di ascolto del gateway PSTN. Questa nuova capacità consente di definire in modo semplice i trunk per garantire la resilienza (per i casi in cui si possono usare più Mediation Servers per instradare le chiamate allo stesso gateway PSTN), per l'interoperabilità PBX, nei casi in cui più trunk a cui sono associati diversi criteri possono essere usati tra un IP-PBX e un Mediation Server e per la configurazione i di trunk SIP nei casi in cui i Mediation Server in diversi siti hanno trunk SIP all'operatore a cui viene fatto riferimento mediante l'FQDN dell'operatore stesso.

## Vedere anche

#### Concetti

[Nuove funzionalità di VoIP aziendale in Lync Server 2013](lync-server-2013-new-enterprise-voice-features.md)

