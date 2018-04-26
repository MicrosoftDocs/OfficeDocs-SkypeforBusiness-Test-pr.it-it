---
title: "Lync Server 2013: Requisiti dell'infrastruttura di Active Directory"
TOCTitle: Requisiti dell'infrastruttura di Active Directory
ms:assetid: c2086f7b-662f-4179-ab99-2c0311ebd903
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412955(v=OCS.15)
ms:contentKeyID: 49301891
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti dell'infrastruttura di Active Directory per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-11-07_

Prima di avviare il processo di preparazione di Servizi di dominio Active Directory per Lync Server 2013, verificare che l'infrastruttura di Active Directory soddisfi i prerequisiti seguenti:

  - In tutti i controller di dominio (inclusi tutti i server di catalogo globale) nella foresta in cui si distribuisce Lync Server viene eseguito uno dei sistemi operativi seguenti:
    
      - Sistema operativo Windows Server 2012 R2
    
      - Sistema operativo Windows Server 2012
    
      - sistema operativo Windows Server 2008 R2
    
      - sistema operativo Windows Server 2008
    
      - Windows Server 2008 Enterprise a 32 bit
    
      - Versioni a 32 bit o a 64 bit del sistema operativo Windows Server 2003 R2
    
      - Versioni a 32 bit o a 64 bit di sistema operativo Windows Server 2003

  - Tutti i domini in cui si distribuisce Lync Server vengono elevati a un livello funzionale di dominio corrispondente a Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008 o almeno a Windows Server 2003.

  - La foresta in cui si distribuisce Lync Server viene elevata a un livello funzionale di foresta corrispondente a Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008 o almeno a Windows Server 2003.
    

    > [!NOTE]
    > Per modificare il livello funzionale di dominio o di foresta, vedere "Aumento dei livelli di funzionalità del dominio e dell'insieme di strutture" nella Libreria TechNet all'indirizzo <A class=uri href="http://go.microsoft.com/fwlink/?linkid=263775">http://go.microsoft.com/fwlink/?linkid=263775</A>.



  - Viene distribuito un catalogo globale in ogni dominio in cui si distribuiscono computer o utenti di Lync Server.

Lync Server 2013 supporta i gruppi universali nei sistemi operativi Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008 e Windows Server 2003. Ai membri dei gruppi universali, che possono includere altri gruppi e account di qualsiasi dominio della foresta o dell'albero del dominio, è possibile assegnare autorizzazioni in qualsiasi dominio della foresta o dell'albero del dominio. Il supporto dei gruppi universali, insieme alla delega dell'amministratore, semplifica la gestione di una distribuzione di Lync Server. Non è più necessario ad esempio aggiungere un dominio a un altro per consentire a un amministratore di gestirli entrambi.

