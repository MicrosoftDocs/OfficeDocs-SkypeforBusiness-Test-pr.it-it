---
title: 'Lync Server 2013: Preparazione della foresta'
TOCTitle: Preparazione della foresta
ms:assetid: 3d188fcb-c64e-46cf-a3a7-9e3ebefed7fd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425898(v=OCS.15)
ms:contentKeyID: 49300282
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Preparazione della foresta per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

Con la preparazione della foresta vengono creati oggetti e impostazioni globali di Active Directory e gruppi universali di Active Directory utilizzabili da Lync Server 2013. Vengono inoltre concesse le autorizzazioni di accesso appropriate per gli oggetti Active Directory. Per una descrizione dei gruppi universali, delle impostazioni globali e degli oggetti creati durante la preparazione della foresta, vedere [Modifiche apportate durante la preparazione della foresta in Lync Server 2013](lync-server-2013-changes-made-by-forest-preparation.md).

Con la preparazione della foresta vengono creati inoltre oggetti contenenti insiemi di proprietà e identificatori di visualizzazione utilizzati da Lync Server 2013. Tali oggetti vengono memorizzati nel contenitore di configurazione.

> [!important]  
> Assicurarsi che le modifiche della preparazione dello schema siano state replicate in tutti i controller di dominio prima di eseguire la procedura di preparazione della foresta. Se la replica non è completa, si verifica un errore.

Se si esegue una nuova distribuzione di Lync Server, è necessario memorizzare le impostazioni globali nel contenitore di configurazione. Se invece si esegue l'aggiornamento da una versione precedente e si memorizzano ancora le impostazioni globali nel contenitore di sistema, è possibile continuare a utilizzare tale contenitore.

Per eseguire questa procedura, è necessario essere membri del gruppo Enterprise Admins o Domain Admins per il dominio radice della foresta.

## Argomenti della sezione

  - [Esecuzione della preparazione della foresta per Lync Server 2013](lync-server-2013-running-forest-preparation.md)

  - [Utilizzo dei cmdlet per annullare la preparazione della foresta per Lync Server 2013](lync-server-2013-using-cmdlets-to-reverse-forest-preparation.md)

