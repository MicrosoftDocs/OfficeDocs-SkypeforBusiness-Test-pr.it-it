---
title: Visualizzazione dei rapporti di Best Practices Analyzer
TOCTitle: Visualizzazione dei rapporti di Best Practices Analyzer
ms:assetid: 7217a47b-36b1-4923-81ea-df754cff29bb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg607690(v=OCS.15)
ms:contentKeyID: 49300951
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzazione dei rapporti di Best Practices Analyzer

 

_**Ultima modifica dell'argomento:** 2012-09-21_

Quando si utilizza lo strumento Best Practices Analyzer per l'analisi del proprio ambiente, è necessario specificare un nome per l'analisi. Al termine di questa, Best Practices Analyzer archivia i risultati all'interno di rapporti e li salva con il nome dell'analisi. Al termine dell'analisi, è possibile visualizzare i rapporti generati sull'analisi stessa, facendo clic su **Visualizza un rapporto di questa analisi Best Practices** direttamente dalla pagina **Analisi completata**. I rapporti delle analisi possono essere visualizzati in qualunque momento dal computer locale sul quale è stata eseguita l'analisi, o importarli da un altro computer. È inoltre possibile esportare i risultati delle analisi per visualizzare i rapporti da un altro computer sul quale è installato lo strumento Best Practices Analyzer.

I risultati dell'analisi sono presentati all'interno dei seguenti tipi di rapporto:

  - Rapporti a elenco

  - Rapporti a albero

  - Altri rapporti

I rapporti includono errori, avvertenze e altre informazioni. Per maggiori dettagli su ciascuno dei tipi di rapporto e sui problemi, vedere [Informazioni sui report creati da Best Practices Analyzer](lync-server-2013-understanding-reports-created-by-best-practices-analyzer.md).

Per visualizzare i risultati delle analisi generate in precedenza attraverso lo strumento Best Practices Analyzer, seguire questa procedura.

## Per visualizzare i rapporti di un'analisi precedente

1.  Accedere a un computer sul quale è installato lo strumento Best Practices Analyzer, utilizzando un account membro dell'account dell'utente locale.
    

    > [!NOTE]
    > È possibile visualizzare i risultati di un'analisi utilizzando un account membro del gruppo degli amministratori locali, ma è possibile eseguire un'analisi solo se si dispone dei diritti e delle autorizzazioni appropriate. Per ulteriori dettagli, vedere <A href="lync-server-2013-group-memberships-and-user-rights-requirements-for-best-practices-analyzer.md">Requisiti di appartenenze ai gruppi e diritti utente per Best Practices Analyzer</A>.



2.  Fare clic su **Start**, scegliere **Tutti i programmi**, fare clic su **Microsoft Lync Server 2013** e quindi su **Best Practices Analyzer**.

3.  Nella schermata di **Benvenuto**, fare clic su **Selezionare i risultati dell'analisi da visualizzare**.

4.  Nella pagina **Selezionare un'analisi Best Practices da visualizzare**, eseguire una delle seguenti operazioni:
    
      - Per visualizzare rapporti dall'elenco dei risultati archiviati localmente, fare clic sul nome dell'analisi e quindi su **Visualizza un rapporto di questa analisi**.
        

        > [!NOTE]
        > Best Practices Analyzer crea un elenco di file locali dalla cartella <EM>&lt;UnitàSistema&gt;</EM>\Documents and Settings\\<EM>&lt;utente&gt;</EM>\Application Data\Microsoft\RtcBPA.

    
      - Per visualizzare rapporti dei risultati di un'analisi, memorizzati in un altro percorso, fare clic su **Importa analisi**, localizzare il file contenente i risultati dell'analisi, quindi fare clic su **Apri**.
        

        > [!NOTE]
        > Se la versione di Best Practices Analyzer del computer non corrisponde a quella utilizzata per la raccolta dei dati nel file importato, lo strumento nel computer potrebbe analizzare nuovamente il file dopo l'importazione.



5.  Nella pagina **Visualizza rapporto Best Practices** effettuare una delle seguenti operazioni:
    
      - Per visualizzare i rapporti in un elenco organizzato per componente server, fare clic su **Elenca rapporti**, quindi fare clic sulla scheda **Tutti i problemi** o **Elementi informativi**.
    
      - Per visualizzare i rapporti in un elenco gerarchico organizzato per tipo di risultato, fare clic su **Rapporti albero**, quindi fare clic sulla scheda **Visualizzazione Dettagli** o **Visualizzazione riepilogo**.
    
      - Per visualizzare altri rapporti, fare clic su **Altri rapporti**.
    

    > [!NOTE]
    > Per informazioni dettagliate sui rapporti di Best Practices Analyzer e le problematiche che è in grado di identificare, vedere <A href="lync-server-2013-viewing-and-working-with-reports-created-by-best-practices-analyzer.md">Visualizzazione e utilizzo dei rapporti creati da Best Practices Analyzer</A> e <A href="lync-server-2013-analyzing-and-resolving-issues-identified-by-best-practices-analyzer.md">Analisi e risoluzione dei problemi identificati da Best Practices Analyzer</A>.


