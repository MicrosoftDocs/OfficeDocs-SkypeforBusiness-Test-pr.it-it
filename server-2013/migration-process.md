---
title: Processo di migrazione
TOCTitle: Processo di migrazione
ms:assetid: 13d71f4b-9d5e-4ea3-9e93-29fdad7ac68f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204696(v=OCS.15)
ms:contentKeyID: 49299761
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Processo di migrazione

 

_**Ultima modifica dell'argomento:** 2012-09-17_

La procedura di migrazione consigliata e supportata per Lync Server 2013 è una procedura di migrazione affiancata. In questo argomento vengono illustrati i motivi per cui utilizzare questo tipo di migrazione e fornite informazioni sul test di coesistenza.

## Migrazione affiancata

In pressoché tutte le migrazioni è consigliabile utilizzare il percorso di migrazione affiancata. In una migrazione affiancata è possibile distribuire un nuovo server con Lync Server 2013 insieme al server corrispondente che esegue Lync Server 2010 e quindi trasferire le operazione nel nuovo server. Se si rende necessario eseguire il rollback a Lync Server 2010, è sufficiente spostare nuovamente le operazioni nei server originali. Tenere presente che in questa situazione tutte le nuove riunioni pianificate con client aggiornati non funzioneranno e sarà necessario eseguire anche il downgrade dei client.

## Testing della coesistenza

Dopo aver distribuito Lync Server 2013 in parallelo con Lync Server 2010, la distribuzione rappresenta uno stato del test di coesistenza di Lync Server 2013 e Lync Server 2010. In questo stato è importante testare e verificare che i servizi siano avviati, che sia possibile amministrare ogni sito e che i client siano in grado di comunicare con gli utenti correnti e legacy. Prima di eseguire la migrazione di tutti gli utenti, è estremamente importante conoscere lo stato di ciascuna distribuzione e verificare che ogni distribuzione sia operativa e funzioni correttamente. In genere, la fase del test di coesistenza viene eseguita durante i test pilota di Lync Server 2013. Gli utenti legacy vengono spostati in Lync Server 2013 per un certo periodo di tempo per garantire il corretto funzionamento della compatibilità e delle funzionalità e funzioni delle applicazioni. Al termine dei test pilota, gli utenti e le applicazioni vengono spostati nella versione di produzione di Lync Server 2013 e i pool e le applicazioni legacy di Lync Server 2010 vengono ritirati.

