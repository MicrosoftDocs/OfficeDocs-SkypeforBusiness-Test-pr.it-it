---
title: Processo di migrazione
TOCTitle: Processo di migrazione
ms:assetid: b2bd9c76-2f4b-4d14-a5c4-157bbff75de0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205181(v=OCS.15)
ms:contentKeyID: 49301708
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Processo di migrazione

 

_**Ultima modifica dell'argomento:** 2012-09-24_

La procedura di migrazione consigliata e supportata per Lync Server 2013 è la procedura di migrazione side-by-side. In questo argomento vengono illustrati i motivi per cui utilizzare questo tipo di migrazione e vengono inoltre fornite informazioni sulla coesistenza.

## Migrazione side-by-side

In quasi ogni migrazione è consigliabile utilizzare il percorso di migrazione side-by-side. In una migrazione side-by-side è necessario distribuire un nuovo server con Lync Server 2013 insieme a un server corrispondente che esegue Office Communications Server 2007 R2 e quindi trasferire le operazioni nel nuovo server. Se si rende necessario eseguire il rollback a Office Communications Server 2007 R2, è sufficiente spostare nuovamente le operazioni nei server originali. Tenere presente che in questa situazione tutte le nuove riunioni pianificate con client aggiornati non funzioneranno e sarà necessario eseguire anche il downgrade dei client.

## Testing della coesistenza

Dopo avere distribuito Lync Server 2013 in parallelo con Office Communications Server 2007 R2, la topologia rappresenta uno stato di testing della coesistenza di Lync Server 2013 e Office Communications Server 2007 R2. In questo stato è importante testare e verificare che i servizi siano avviati, che sia possibile amministrare ogni sito e che i client siano in grado di comunicare con gli utenti correnti e legacy. Prima di eseguire la migrazione di tutti gli utenti, è molto importante identificare lo stato di ogni distribuzione e assicurarsi che ogni distribuzione sia corretta e funzionante. La fase di testing della coesistenza in genere si estende per tutta la durata del testing pilota di Lync Server 2013. Gli utenti legacy vengono spostati in Lync Server 2013 per un certo periodo di tempo per garantire il corretto funzionamento della compatibilità e delle funzionalità e funzioni delle applicazioni. Dopo il testing pilota, gli utenti e le applicazioni vengono spostati nella versione di produzione di Lync Server 2013 e i pool e le applicazioni legacy di Office Communications Server 2007 R2 vengono disattivati.

