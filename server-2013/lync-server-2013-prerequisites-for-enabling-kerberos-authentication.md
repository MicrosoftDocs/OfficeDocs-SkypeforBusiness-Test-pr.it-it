---
title: "Lync Server 2013: Prerequisiti per abilitare l'autenticazione Kerberos"
TOCTitle: Prerequisiti per abilitare l'autenticazione Kerberos
ms:assetid: 3f276a21-7476-4bc0-9fd1-59e844d2e9c1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425909(v=OCS.15)
ms:contentKeyID: 49300303
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Prerequisiti per abilitare l'autenticazione Kerberos in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

Prima di abilitare l'autenticazione Kerberos, verificare che siano state completate tutte le attività di preparazione indispensabili per la configurazione e l'infrastruttura:

  - Estensione dello schema di Active Directory per Lync Server 2013.

  - Completamento della preparazione della foresta di Active Directory per Lync Server 2013.

  - Completamento della preparazione del dominio di Active Directory per Lync Server 2013.

  - Installazione e disponibilità dell' archivio di gestione centrale.

  - Creazione e pubblicazione della topologia tramite Generatore di topologie.

  - Definizione e distribuzione dei server e dei ruoli che richiedono i servizi Web, inclusi Front End Server, server Standard Edition e Director.

  - Configurazione e distribuzione di Internet Information Services (IIS) con i servizi ruolo consigliati per supportare i servizi Web in Lync Server 2013.

Dopo aver soddisfatto tutti i prerequisiti, si è pronti per creare uno o più account utilizzabili dai servizi Web per l'autenticazione Kerberos per la distribuzione. È necessario creare come minimo un account di autenticazione Kerberos per ogni distribuzione. È tuttavia possibile creare un account per ogni sito per fornire l'autenticazione Kerberos locale nel sito. È possibile specificare un solo account di autenticazione Kerberos per sito.

