---
title: Configurazione delle opzioni di archiviazione a livello globale
TOCTitle: Configurazione delle opzioni di archiviazione a livello globale
ms:assetid: bfe415f7-2abf-41ee-a1cb-cf48b2d59c0c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205233(v=OCS.15)
ms:contentKeyID: 49301842
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione delle opzioni di archiviazione a livello globale

 

_**Ultima modifica dell'argomento:** 2012-10-10_

Quando si aggiunge l'archiviazione alla topologia e si pubblica quest'ultima, Lync Server crea una configurazione globale per l'archiviazione. Per impostazione predefinita, nella configurazione globale non è abilitata alcuna opzione di archiviazione. La configurazione globale controlla le opzioni abilitate per l'intera distribuzione, a meno che non si impostino configurazioni a livello di sito o di pool, le quali hanno la priorità sulla configurazione globale.

Per informazioni dettagliate sul funzionamento delle configurazioni di archiviazione, inclusa la gerarchia delle configurazioni globale, del sito e del pool, vedere [Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md) nella documentazione relativa alla pianificazione, alla distribuzione o alle operazioni.


> [!NOTE]
> Specificare tutte le opzioni appropriate nelle configurazioni di archiviazione prima di abilitare l'archiviazione.



## Per configurare le opzioni di archiviazione a livello globale

1.  Da un account utente assegnato al ruolo CsArchivingAdministrator o CsAdministrator, eseguire l'accesso a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server 2013. Per informazioni dettagliate sui diversi metodi che è possibile utilizzare per avviare il Pannello di controllo di Lync Server 2013, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di navigazione di sinistra fare clic su **Monitoraggio e archiviazione**, quindi scegliere **Configurazione archiviazione**.

4.  Nella pagina **Configurazione archiviazione** fare clic su **Globale**, su **Modifica** e quindi su **Mostra dettagli**.

5.  In **Modifica Impostazione di archiviazione - Globale** selezionare una delle opzioni di archiviazione seguenti nell'elenco a discesa **Impostazione di archiviazione**:
    
      - **Disabilita archiviazione**
    
      - **Archivia sessioni di messaggistica istantanea**
    
      - **Archivia sessioni di messaggistica istantanea e Web Conferencing**

6.  Sempre nella pagina **Modifica Impostazione di archiviazione - Globale** eseguire le operazioni seguenti:
    
      - Per bloccare l'attività quando l'archiviazione non è disponibile, selezionare la casella di controllo **Blocca sessioni di messaggistica istantanea o Web Conferencing se l'archiviazione non riesce**.
    
      - Per archiviare i dati di archiviazione utilizzando Microsoft Exchange Server, selezionare la casella di controllo **Integrazione Microsoft Exchange**.
    
      - Per consentire l'eliminazione dei dati, selezionare la casella di controllo **Abilita eliminazione dei dati di archiviazione** e quindi eseguire una delle operazioni seguenti:
        
          - Per specificare l'eliminazione dopo un numero specifico di giorni, fare clic su **Elimina dati di archiviazione esportati e archiviati dopo durata massima (giorni)** e quindi specificare il numero di giorni.
        
          - Per limitare l'eliminazione ai dati di archiviazione esportati, fare clic su **Elimina solo i dati di archiviazione esportati**.

7.  Fare clic su **Commit**.

