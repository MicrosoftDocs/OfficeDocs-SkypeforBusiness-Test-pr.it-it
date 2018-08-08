---
title: "Lync Server 2013: Best Practices Analyzer analizza potenz. problemi della distribuz."
TOCTitle: "Lync Server 2013: Best Practices Analyzer analizza potenz. problemi della distribuz."
ms:assetid: 09c84509-dc91-4e7b-882b-3c467b6b026d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg591343(v=OCS.15)
ms:contentKeyID: 49299618
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Utilizzo di Best Practices Analyzer per analizzare i potenziali problemi della distribuzione

 

_**Ultima modifica dell'argomento:** 2012-10-21_

Per eseguire un'analisi di Best Practices Analyzer è necessario specificare quanto segue:

  - **Credenziali**   Per eseguire un'analisi è necessario accedere a un computer in cui è installato Best Practices Analyzer con un account membro del gruppo Administrators locale. L'account deve inoltre disporre dei diritti e delle autorizzazioni utente richieste per l'esecuzione di Best Practices Analyzer. Per informazioni dettagliate, vedere [Requisiti di appartenenze ai gruppi e diritti utente per Best Practices Analyzer](lync-server-2013-group-memberships-and-user-rights-requirements-for-best-practices-analyzer.md).

  - **Ambito dell'analisi**   Per specificare l'ambito dell'analisi, selezionare le categorie e i server da sottoporre ad analisi. È possibile selezionare tutte le categorie, una o più categorie oppure uno o più server all'interno di una specifica categoria dell'ambiente Lync Server.

  - **Tipo di analisi**   Attualmente l'unico tipo di analisi disponibile è la verifica dell'integrità, selezionata per impostazione predefinita. Quest'analisi genera un rapporto che include errori, avvisi e altre informazioni relative a tutti i server specificati nell'ambito.

  - **Velocità di rete**   Le opzioni relative alla velocità di rete includono Fast LAN (100 Mbps o superiore), LAN (10 Mbps), Fast WAN (1,5 Mbps) o WAN (64 kbps). Il tempo stimato per il completamento dell'analisi è basato su questa impostazione, che viene anche utilizzata per impostare il periodo di timeout. Durante l'analisi, Best Practices Analyzer attende una risposta da ciascun server per un tempo specifico. Se non riceve una risposta entro il periodo di timeout specificato, passa al server successivo nell'analisi. Su reti più lente il timeout è più lungo perché tiene conto di latenze di rete più estese. È consigliabile selezionare il collegamento più lento nella topologia per questo parametro, in modo tale che il timeout non venga eseguito troppo velocemente.

## Per analizzare la distribuzione di Lync Server 2013

1.  Accedere a un computer in cui è installato Best Practices Analyzer utilizzando un account membro del gruppo Administrators locale e che disponga di tutti i diritti e le autorizzazioni necessarie.

2.  Fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Best Practices Analyzer**.

3.  Nella schermata inizialescegliere **Seleziona le opzioni per una nuova analisi**.

4.  Nella pagina **Connessione a Active Directory** verificare il nome specificato in **Server Active Directory** e quindi eseguire una delle operazioni seguenti:
    
      - Per eseguire un'analisi con le stesse credenziali utilizzate per accedere al computer, fare clic su **Connessione al server Active Directory**.
    
      - Per specificare credenziali diverse da utilizzare per Servizi di dominio Active Directory, server perimetrali o server Exchange, fare clic su **Mostra opzioni di accesso avanzate**, selezionare le caselle di controllo per cui sono necessarie credenziali separate, specificare le credenziali per ogni casella di controllo selezionata e quindi fare clic su **Connessione al server Active Directory**.
    

    > [!NOTE]
    > Prima di iniziare l'analisi, Best Practices Analyzer esegue un controllo della rete e delle autorizzazioni, per verificare che le credenziali dell'account specificate siano valide e che lo strumento sia in grado connettersi a Servizi di dominio Active Directory. Se lo strumento è in esecuzione in un server Workgroup, verifica inoltre che sia possibile eseguire la connessione ai server perimetrali presenti nella rete perimetrale (se sono inclusi nell'analisi).



5.  Nella pagina **Avvia una nuova analisi Best Practices** selezionare le opzioni da includere nell'analisi, specificare la velocità di rete e quindi fare clic su **Avvia l'analisi**.

6.  Nella pagina **Analisi completata** fare clic su **Visualizza un rapporto di questa analisi Best Practices**.

7.  Nella pagina **Visualizza rapporto Best Practices** eseguire una delle operazioni seguenti:
    
      - Per visualizzare i rapporti in un elenco organizzato per componenti server, fare clic su **Elenca rapporti** e quindi sulla scheda **Tutti i problemi** o sulla scheda **Elementi informativi**.
    
      - Per visualizzare i rapporti in un elenco gerarchico organizzato per tipi di risultato, fare clic su **Rapporti albero** e quindi sulla scheda **Visualizzazione Dettagli** o sulla scheda **Visualizzazione Riepilogo**.
    
      - Per visualizzare altri rapporti, fare clic su **Altri rapporti**.
    

    > [!NOTE]
    > Per informazioni dettagliate sui rapporti di Best Practices Analyzer e sui problemi identificati, vedere <A href="lync-server-2013-viewing-and-working-with-reports-created-by-best-practices-analyzer.md">Visualizzazione e utilizzo dei rapporti creati da Best Practices Analyzer</A> e <A href="lync-server-2013-analyzing-and-resolving-issues-identified-by-best-practices-analyzer.md">Analisi e risoluzione dei problemi identificati da Best Practices Analyzer</A>.


