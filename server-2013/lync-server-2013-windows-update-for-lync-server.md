---
title: 'Lync Server 2013: Windows Update per Lync Server'
TOCTitle: Windows Update per Lync Server 2013
ms:assetid: fe26ab32-b1a9-421d-9227-506703d4b834
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn518337(v=OCS.15)
ms:contentKeyID: 60490921
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Windows Update per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-12-05_

Usare Windows Update Services per controllare di frequente se sono disponibili aggiornamenti e aggiornamenti della sicurezza da applicare. In questo modo si evitano vulnerabilità in altri componenti del sistema che potrebbero consentire agli autori di attacchi di ottenere l'accesso ai server che eseguono Microsoft Lync Server 2013 con diritti di amministratore, per poi compromettere Lync Server 2013.

Applicare gli aggiornamenti per Microsoft SQL Server 2008 Express (edizione a 64 bit) in ogni server Standard Edition di Lync Server 2013 (per il database back-end) e in tutti gli altri ruoli del server di Lync Server 2013 (per l'archivio di configurazione locale), a meno che tali database non siano stati aggiornati a SQL Server 2008 R2 Express. Questi database dovrebbero essere considerati parte integrante delle attività di manutenzione per gli aggiornamenti di sicurezza di routine, così come SQL Server nel database back-end di un pool Front End, il database di monitoraggio e il database di archiviazione.

## Procedura consigliata

  - Mantenersi aggiornati con Windows Update.

