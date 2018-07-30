---
title: Configurazione delle opzioni di archiviazione per un sito
TOCTitle: Configurazione delle opzioni di archiviazione per un sito
ms:assetid: 59b48fd9-d5fc-40b4-abae-e9cf89ee5573
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204930(v=OCS.15)
ms:contentKeyID: 49300671
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione delle opzioni di archiviazione per un sito

 

_**Ultima modifica dell'argomento:** 2012-10-09_

È possibile specificare le opzioni di archiviazione da applicare a siti specifici tramite la creazione e configurazione delle opzioni in una configurazione di archiviazione per ognuno dei siti. Una configurazione di sito ha la priorità rispetto alla configurazione globale, ma solo per il sito specificato. Le configurazioni di pool sono prioritarie rispetto alle configurazioni di sito.

Per informazioni dettagliate sul funzionamento delle configurazioni di archiviazione, inclusa la gerarchia per le configurazioni globale, di sito e di pool, vedere [Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md) nella documentazione relativa alla pianificazione, alla distribuzione o alle operazioni.


> [!NOTE]
> Prima di abilitare l'archiviazione, è consigliabile specificare tutte le opzioni appropriate nelle configurazioni di archiviazione.



> [!IMPORTANT]  
> Per abilitare l'archiviazione, è necessario specificare i relativi criteri allo scopo di controllare l'archiviazione delle comunicazioni interne ed esterne a livello globale e, se appropriato, a livello di sito e utente. Se si configurano i criteri a livello utente, è necessario assegnare i criteri utente a utenti specifici. Per informazioni dettagliate sulla creazione e la configurazione dei criteri di archiviazione, vedere <a href="lync-server-2013-managing-the-archiving-of-internal-and-external-communications.md">Gestione dell'archiviazione delle comunicazioni interne ed esterne in Lync Server 2013</a> nella documentazione relativa alle operazioni.

## Per configurare le opzioni di archiviazione a livello del sito

1.  Da un account utente assegnato al ruolo CsArchivingAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server 2013. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server 2013, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di navigazione di sinistra fare clic su **Monitoraggio e archiviazione**, quindi scegliere **Configurazione archiviazione**.

4.  Nella pagina **Configurazione archiviazione** fare clic su **Nuovo** e quindi su **Configurazione sito**.

5.  In **Seleziona un sito** selezionare il sito da configurare per l'archiviazione.

6.  In **Nuova impostazione di archiviazione** eseguire una delle operazioni seguenti nella casella di riepilogo a discesa **Impostazione di archiviazione**:
    
      - Per abilitare l'archiviazione solo per le sessioni di messaggistica istantanea, fare clic su **Archivia sessioni di messaggistica istantanea**.
    
      - Per abilitare l'archiviazione per le sessioni di messaggistica istantanea e le conferenze, fare clic su **Archivia sessioni di messaggistica istantanea e Web Conferencing**.
    
      - Per disabilitare l'archiviazione dei criteri, fare clic su **Disabilita archiviazione**.

7.  Ancora in **Nuova impostazione di archiviazione** eseguire le operazioni seguenti:
    
      - Per bloccare l'attività quando l'archiviazione non è disponibile, selezionare la casella di controllo **Blocca sessioni di messaggistica istantanea o Web Conferencing se l'archiviazione non riesce**.
    
      - Per utilizzare Microsoft Exchange Server per memorizzare i dati di archiviazione, fare clic sulla casella di controllo **Integrazione Microsoft Exchange**.
    
      - Per abilitare l'eliminazione dei dati, selezionare la casella di controllo **Abilita eliminazione dei dati di archiviazione** e quindi eseguire una delle operazioni seguenti:
        
          - Per specificare l'eliminazione dopo un numero specifico di giorni, fare clic su **Elimina dati di archiviazione esportati e archiviati dopo durata massima (giorni)** e quindi specificare il numero di giorni.
        
          - Per limitare l'eliminazione ai dati di archiviazione esportati, fare clic su **Elimina solo i dati di archiviazione esportati**.

8.  Fare clic su **Commit**.

