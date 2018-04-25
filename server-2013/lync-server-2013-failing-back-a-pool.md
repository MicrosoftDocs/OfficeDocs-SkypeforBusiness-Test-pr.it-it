---
title: 'Lync Server 2013: Failback di un pool'
TOCTitle: Failback di un pool
ms:assetid: 6232b644-ef57-4c9c-abec-14ff8ffc9fe7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204945(v=OCS.15)
ms:contentKeyID: 49300767
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Failback di un pool in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Dopo aver riportato online il pool in cui si è verificata la situazione di emergenza (ovvero Pool1 in questo esempio), eseguire le operazioni seguenti per ripristinare uno stato di funzionamento regolare per la distribuzione.

Si noti che per il completamento del processo di failback sono richiesti vari minuti. A titolo di riferimento, sono previsti fino a 60 minuti per un pool di 20.000 utenti.

1.  Eseguire il failback degli utenti ospitati in origine in Pool1 e di cui è stato eseguito il failover in Pool2 digitando il comando di cmdlet seguente:
    
        Invoke-CsPoolFailback -PoolFQDN <Pool1 FQDN> -Verbose

Non sono necessari altri passaggi. Se è stato eseguito il failover del server di gestione centrale, è possibile lasciarlo in in Pool2.

