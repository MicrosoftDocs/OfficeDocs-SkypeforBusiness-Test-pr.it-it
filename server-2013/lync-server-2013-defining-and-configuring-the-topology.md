---
title: 'Lync Server 2013: Definizione e configurazione della topologia'
TOCTitle: Definizione e configurazione della topologia
ms:assetid: 51d1601e-4f83-48d4-ad08-3b4d5e2003aa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398339(v=OCS.15)
ms:contentKeyID: 49300549
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definizione e configurazione della topologia in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-14_

È possibile definire e configurare la topologia utilizzando Generatore di topologie. Per poter utilizzare Generatore di topologie, non è necessario essere membri del gruppo Administrators locale o di un gruppo di dominio con privilegi, quale ad esempio Domain Admins. È possibile definire la topologia come utenti standard. Quando si avvia Generatore di topologie al primo utilizzo e nelle sessioni di modifica successive, viene richiesto di specificare il percorso in cui si desidera che Generatore di topologie carichi il documento di configurazione corrente. Le scelte disponibili sono le seguenti:

  - Scarica topologia dalla distribuzione esistente

  - Apri topologia da un file locale

  - Nuova topologia

Se è già stata definita una topologia ed è già stato specificato l' archivio di gestione centrale, è opportuno scegliere di scaricare una topologia da una distribuzione esistente. Generatore di topologie leggerà il database e recupererà la definizione corrente. Se si dispone di un archivio di gestione centrale esistente, è sempre necessario scegliere questa opzione.

Se non è stato specificato un archivio di gestione centrale e si desidera modificare una configurazione salvata in precedenza, è necessario scegliere di aprire la topologia da un file locale. Il file che verrà aperto sarà il file di configurazione salvato in una sessione precedente. È possibile utilizzare questa opzione per modificare la topologia salvata in precedenza.


> [!WARNING]
> Se è già disponibile una topologia pubblicata, è sconsigliabile caricare un file di configurazione locale, ma è preferibile scegliere di scaricare la topologia da una distribuzione esistente.



Scegliere di creare una nuova topologia se si desidera creare una nuova configurazione di Generatore di topologie. Una progettazione salvata in precedenza non viene sovrascritta a meno che non si scelga di salvarla nello stesso file creato in una sessione di progettazione precedente.

Per ognuna di queste opzioni verrà richiesto di specificare un percorso per l'archiviazione del file di configurazione di Generatore di topologie. Il percorso per il file può essere locale, condiviso in una condivisione file specifica oppure su un supporto rimovibile.

## Argomenti della sezione

  - [Definire e configurare una topologia in Generatore di topologie per Lync Server 2013](lync-server-2013-define-and-configure-a-topology-in-topology-builder.md)

  - [Definire e configurare un pool Front End o un server Standard Edition in Lync Server 2013](lync-server-2013-define-and-configure-a-front-end-pool-or-standard-edition-server.md)

  - [Distribuzione di pool Front End abbinati per il ripristino di emergenza in Lync Server 2013](lync-server-2013-deploying-paired-front-end-pools-for-disaster-recovery.md)

  - [Distribuzione del mirroring di SQL per la disponibilità elevata del server back-end in Lync Server 2013](lync-server-2013-deploying-sql-mirroring-for-back-end-server-high-availability.md)

  - [Modificare o configurare URL semplici in Lync Server 2013](lync-server-2013-edit-or-configure-simple-urls.md)

  - [Selezionare il server di gestione centrale in Lync Server 2013](lync-server-2013-select-the-central-management-server.md)

