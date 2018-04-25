---
title: Considerazioni sulla coesistenza
TOCTitle: Considerazioni sulla coesistenza
ms:assetid: 9d1a3c0f-492a-4e37-bc2f-63509e328785
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205131(v=OCS.15)
ms:contentKeyID: 49301464
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Considerazioni sulla coesistenza

 

_**Ultima modifica dell'argomento:** 2012-10-06_

Dopo la migrazione, esisterà solo un Lync Server 2013, pool di server Chat persistente e sarà possibile rimuovere le autorizzazioni della distribuzione legacy.

Prima del completamento della migrazione e della rimozione delle autorizzazioni della distribuzione Group Chat Server corrente, può essere disponibile una delle distribuzioni seguenti:

  - Lync Server 2013, pool di server Chat persistente, che deve essere ospitato in un pool Lync Server 2013.

  - Pool Lync Server 2010, Group Chat che deve essere ospitato in un pool Lync Server 2010.

  - Pool Office Communications Server 2007 R2Group Chat che deve essere ospitato in un pool Office Communications Server 2007 R2.

Queste distribuzioni possono coesistere in modalità affiancata, tuttavia le categorie, le chat room e i componenti aggiuntivi di una distribuzione non interagiscono con quelli nelle distribuzioni complementari.

Con la configurazione manuale, un client legacy (client Group Chat) può connettersi a un pool alla volta per Office Communications Server 2007 R2, Lync Server 2010, Group Chat, o Lync Server 2013.

Lync 2013 (client) può interagire solo con Lync Server 2013, pool di server Chat persistente, non con pool Group Chat Server legacy. Per usare Chat persistente in Lync 2013 (client), l'utente deve essere ospitato in Lync 2013 e abilitato mediante criteri.

