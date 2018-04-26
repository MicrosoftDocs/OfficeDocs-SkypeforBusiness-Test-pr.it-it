---
title: 'Lync Server 2013: Nuove funzionalità di archiviazione'
TOCTitle: Nuove funzionalità di archiviazione
ms:assetid: c002e367-41ad-498d-9d23-8b117ac435b2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205225(v=OCS.15)
ms:contentKeyID: 49301867
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Nuove funzionalità di archiviazione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-09_

L'archiviazione in Lync Server 2013 consente di archiviare i tipi di contenuto seguenti:

  - Messaggi istantanei peer-to-peer

  - Conferenze (riunioni) costituite da messaggi istantanei tra più parti

  - Contenuto di conferenze, compreso il contenuto caricato (ad esempio, stampati) e correlato agli eventi (ad esempio, accesso, uscita, caricamento in condivisione e modifiche della visibilità)

L'archiviazione in Lync Server 2013 inoltre offre nuove funzionalità che rendono più efficienti la distribuzione e le operazioni. Queste nuove funzionalità sono le seguenti:

  - **Collocazione dell'archiviazione nei Front End Server.**    Lync Server 2013 non dispone di un ruolo Server di archiviazione separato. L'archiviazione infatti è una funzionalità facoltativa, disponibile in tutti i Front End Server di una distribuzione Enterprise Edition e nei server Standard Edition, che può essere implementata e configurata per un pool o un sito.

  - **Integrazione di Microsoft Exchange.**   Quando si distribuisce l'archiviazione, è possibile integrare l'archivio dati per l'archiviazione con l'archivio di Exchange 2013 esistente per tutti gli utenti ospitati in Exchange 2013 e che hanno le cassette postali in archiviazione sul posto. Non è pertanto necessario distribuire database di SQL Server separati per archiviare i dati di Lync. Se non si dispone di una distribuzione di Exchange 2013 o se si preferisce non effettuare l'integrazione con essa oppure se vi sono utenti di Lync 2013 che non si trovano in Exchange 2013 con le cassette postali in archiviazione sul posto, è possibile distribuire database di archiviazione separati utilizzando SQL Server per archiviare i dati archiviati dalle comunicazioni Lync. È possibile utilizzare sia l'integrazione di Microsoft Exchange che database di archiviazione di Lync Server 2013 se si desidera utilizzare l'integrazione di Microsoft Exchange solo per alcuni utenti della distribuzione. Per informazioni dettagliate sull'archiviazione sul posto, vedere la relativa pagina Web all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=267500](http://go.microsoft.com/fwlink/p/?linkid=267500).

  - **Mirroring dell'archivio SQL.**   Quando si distribuisce l'archiviazione, è possibile abilitare il mirroring del database di SQL Server per il database di archiviazione.

  - **Archiviazione delle lavagne e dei sondaggi.**   Nel contenuto archiviato per le conferenze ora sono inclusi le lavagne e i sondaggi condivisi durante la riunione.

Non vengono archiviati i tipi di contenuto seguenti:

  - Trasferimenti di file peer-to-peer

  - Audio e video per messaggi istantanei peer-to-peer e conferenze

  - Condivisione di applicazioni per conferenze e messaggi istantanei peer-to-peer

## Vedere anche

#### Ulteriori risorse

[Pianificazione dell'archiviazione in Lync Server 2013](lync-server-2013-planning-for-archiving.md)

