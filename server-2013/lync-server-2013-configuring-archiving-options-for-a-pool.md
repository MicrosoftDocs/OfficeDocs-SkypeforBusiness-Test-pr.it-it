---
title: Configurazione delle opzioni di archiviazione per un pool
TOCTitle: Configurazione delle opzioni di archiviazione per un pool
ms:assetid: b7cb0fd8-3d31-4858-a75c-c66a7742556e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205200(v=OCS.15)
ms:contentKeyID: 49301753
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione delle opzioni di archiviazione per un pool

 

_**Ultima modifica dell'argomento:** 2012-10-10_

È possibile specificare le opzioni di archiviazione da applicare a pool specifici creando e configurando le opzioni in una configurazione di archiviazione per ognuno di tali pool. La configurazione di un pool ha la priorità sulla configurazione globale e sulla configurazione del sito, ma solo per il pool specificato nella relativa configurazione.

Per informazioni dettagliate sul funzionamento delle configurazioni di archiviazione, inclusa la gerarchia delle configurazioni globale, del sito e del pool, vedere [Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md) nella documentazione relativa alla pianificazione, alla distribuzione o alle operazioni.


> [!NOTE]
> Specificare tutte le opzioni appropriate nelle configurazioni di archiviazione prima di abilitare l'archiviazione. Per informazioni dettagliate, vedere <A href="lync-server-2013-configuring-archiving-options.md">Configurazione delle opzioni di archiviazione</A> nella documentazione relativa alla distribuzione.



## Per configurare le opzioni di archiviazione a livello di pool

1.  Da un account utente assegnato al ruolo CsArchivingAdministrator o CsAdministrator, eseguire l'accesso a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server 2013. Per informazioni dettagliate sui diversi metodi che è possibile utilizzare per avviare il Pannello di controllo di Lync Server 2013, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di navigazione di sinistra fare clic su **Monitoraggio e archiviazione**, quindi scegliere **Configurazione archiviazione**.

4.  Nella pagina **Configurazione archiviazione** fare clic su **Nuovo** e quindi su **Configurazione pool**.

5.  In **Seleziona un servizio** selezionare il pool da configurare per l'archiviazione.

6.  In **Nuova impostazione di archiviazione** selezionare una delle opzioni di archiviazione seguenti nell'elenco a discesa **Impostazione di archiviazione**:
    
      - **Disabilita archiviazione**
    
      - **Archivia sessioni di messaggistica istantanea**
    
      - **Archivia sessioni di messaggistica istantanea e Web Conferencing**

7.  Sempre nella pagina **Nuova impostazione di archiviazione** eseguire le operazioni seguenti:
    
      - Per bloccare l'attività quando l'archiviazione non è disponibile, selezionare la casella di controllo **Blocca sessioni di messaggistica istantanea o Web Conferencing se l'archiviazione non riesce**.
    
      - Per archiviare i dati di archiviazione utilizzando Microsoft Exchange Server, selezionare la casella di controllo **Integrazione Microsoft Exchange**.
    
      - Per consentire l'eliminazione dei dati, selezionare la casella di controllo **Abilita eliminazione dei dati di archiviazione** e quindi eseguire una delle operazioni seguenti:
        
          - Per specificare l'eliminazione dopo un numero specifico di giorni, fare clic su **Elimina dati di archiviazione esportati e archiviati dopo durata massima (giorni)** e quindi specificare il numero di giorni.
        
          - Per limitare l'eliminazione ai dati di archiviazione esportati, fare clic su **Elimina solo i dati di archiviazione esportati**.

8.  Fare clic su **Commit**.

