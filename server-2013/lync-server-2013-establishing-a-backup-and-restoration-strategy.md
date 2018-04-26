---
title: Definizione di una strategia di backup e ripristino
TOCTitle: Definizione di una strategia di backup e ripristino
ms:assetid: f545a75f-bbc4-4968-b510-8f6f3920112b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh202195(v=OCS.15)
ms:contentKeyID: 52062480
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definizione di una strategia di backup e ripristino

 

_**Ultima modifica dell'argomento:** 2013-03-26_

Prima di poter sviluppare un piano di backup e ripristino per Lync Server, è necessario sviluppare una strategia adeguata agli obiettivi della propria organizzazione. Lo sviluppo di una strategia di backup e ripristino efficace include le operazioni seguenti:

  - Stabilire le priorità aziendali.

  - Individuare i requisiti di backup e ripristino.

## Stabilire le priorità aziendali

Valutare le priorità aziendali dell'organizzazione. In genere, le principali priorità aziendali che incidono sulla strategia di backup e ripristino sono le seguenti:

  - Requisiti di continuità aziendale

  - Completezza dei dati

  - Criticità dei dati

  - Requisiti di portabilità

  - Vincoli dei costi

Questo tipo di esigenze aziendali aiutano a definire i contratti di servizio sviluppati con i clienti. I contratti di servizio influenzano enormemente la strategia di backup e ripristino.

## Individuare i requisiti di backup e ripristino

Le priorità aziendali e i contratti di servizio contribuiscono a definire i requisiti di backup e ripristino di Lync Server dell'organizzazione. Individuare e documentare i requisiti per i seguenti fattori:

  - **Frequenza di backup** Tenere presente che, ad eccezione dei pool Front End in relazioni di abbinamento, come illustrato in [Pianificazione per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md), Lync Server supporta solo il modello di recupero con registrazione minima in basa a cui viene ripristinato l'ultimo backup completo. Pianificare attentamente la frequenza con cui occorre effettuare un backup completo. Per dettagli sulle procedure consigliate per la frequenza di backup, vedere [Procedure consigliate per il backup e il ripristino](lync-server-2013-best-practices-for-backup-and-restoration.md).

  - **Strumenti di backup e ripristino** Includere chi utilizzerà gli strumenti e in quali computer. Per dettagli sugli strumenti illustrati in questo argomento e sulle autorizzazioni necessarie, vedere [Requisiti di backup e ripristino: strumenti e autorizzazioni](lync-server-2013-backup-and-restoration-requirements-tools-and-permissions.md).

  - **Percorso di backup**   Determinare se i backup vengono mantenuti localmente o in remoto, tenendo conto della sicurezza e dell'accessibilità. Specificare i supporti da utilizzare per i backup.

  - **Requisiti hardware e software**   Individuare e documentare l'hardware per l'archiviazione di backup e il ripristino di componenti specifici, nonché software e connettività di rete richiesti per supportare backup e ripristino. Nello sviluppo dei requisiti hardware e software, valutare i diversi scenari di ripristino illustrati di seguito.

  - **Scenari di ripristino** Viene descritto il processo di ripristino per i seguenti scenari:
    
      - Errore di un pool di Lync Server. Questo scenario richiede la ricostruzione di ogni server nel pool.
    
      - Errore di un server Standard Edition. Questo scenario richiede la ricostruzione del server in un computer nuovo o sottoposto a pulizia e il ripristino dei database.
    
      - Perdita dell'archivio di gestione centrale. Questo scenario richiede, come minimo, il ripristino e la pubblicazione dell'archivio di gestione centrale.
    
      - Perdita di un server back-end mentre l'archivio di gestione centrale funziona normalmente. Questo scenario richiede la ricostruzione del server in un computer nuovo o sottoposto a pulizia e il ripristino dei database.
    
      - Errore di un server membro di un pool di Lync Server. Questo scenario richiede la ricostruzione del server in un computer nuovo o sottoposto a pulizia e il ripristino dei database.
    
      - Errore di un Archivio file. Questo scenario richiede il ripristino del file server o del file cluster.
    
      - Errore di un database di archiviazione, di monitoraggio o di Chat persistente. Questo scenario richiede la ricostruzione dei database e il ripristino dei dati, se questi sono critici per l'organizzazione. I dati di archiviazione, monitoraggio e Chat persistente non sono necessari per ripristinare l'esecuzione di Lync Server.

