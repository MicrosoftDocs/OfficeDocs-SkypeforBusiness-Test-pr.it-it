---
title: Informazioni sui report creati da Best Practices Analyzer
TOCTitle: Informazioni sui report creati da Best Practices Analyzer
ms:assetid: 1386dd6c-7f3e-4da9-905b-cef1468bf14a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg591344(v=OCS.15)
ms:contentKeyID: 49299748
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Informazioni sui report creati da Best Practices Analyzer

 

_**Ultima modifica dell'argomento:** 2012-10-10_

Best Practices Analyzer fornisce diversi tipi di rapporto organizzati in modo da favorire l'analisi e la risoluzione dei problemi tramite l'identificazione di errori, avvisi e altre informazioni.

## Rapporti

È possibile accedere ai risultati di un'analisi visualizzando i seguenti tipi di rapporto:

  - **Rapporti elenco**   I rapporti elenco vengono organizzati in base a specifici criteri. È possibile ordinare i risultati per classe, gravità o problema. Se, ad esempio, si organizzano i risultati per classe, i problemi riguardanti i Director sono riportati nella sezione Directors del rapporto. È possibile visualizzare tutti i problemi o solo gli elementi informativi, nonché cercare uno specifico elemento di un rapporto elenco, ad esempio la memoria. È inoltre possibile stampare o esportare il rapporto.

  - **Rapporti albero**   I rapporti albero vengono organizzati in base alle regole utilizzate per eseguire l'analisi e ad altre opzioni specificate al momento dell'analisi. I problemi relativi alle regole di topologia dei test, ad esempio, sono inclusi nella sezione Test Topology del rapporto. È possibile visualizzare i dettagli di tutti i problemi o solo un riepilogo degli stessi, nonché cercare uno specifico elemento di un rapporto albero, ad esempio la memoria. È inoltre possibile stampare o esportare il rapporto.

  - **Altri rapporti**   In Altri rapporti viene riportato il log delle attività in fase di esecuzione incluse nell'analisi. È possibile cercare specifici elementi contenuti in altri rapporti, ad esempio la memoria. È inoltre possibile stampare o esportare il rapporto.

## Problemi

I rapporti generati da Best Practices Analyzer indicano specifici problemi identificati durante l'analisi dell'ambiente, tra cui i seguenti tipi:

  - **Errori**   Problemi critici che richiedono di apportare modifiche all'ambiente. Se, ad esempio, non sono installati Componenti di base di Lync Server 2013, viene registrato un errore.
    
    I problemi classificati come errore sono identificati dalla presenza di un simbolo X rosso nel rapporto. Gli errori sono visualizzati nella scheda **All Issues** della visualizzazione **List Reports** e nelle schede **Detailed View** e **Summary View** della visualizzazione **Tree Reports**. Qualora non si desideri visualizzare uno specifico errore in un rapporto, è possibile specificare che non venga mostrata una singola istanza o tutte le istanze dell'errore in questione. In tal caso, l'errore sarà visualizzato solo nella scheda **Hidden Items** della visualizzazione **Other Reports** , a meno che non si modifichi l'impostazione e si specifichi di visualizzare l'errore nel rapporto.

  - **Avvisi**   Problemi non coerenti con l'implementazione di una procedura consigliata, che possono segnalare la necessità di apportare una modifica all'ambiente. Potrebbe trattarsi di un problema noto con una specifica impostazione che è necessario modificare. I servizi non avviati in un server, ad esempio, vengono registrati come avvisi.
    
    I problemi classificati come avvisi sono segnalati nel rapporto dalla presenza di un simbolo di avviso triangolare giallo. Gli avvisi vengono visualizzati nella scheda **All Issues** della visualizzazione **List Reports** e nelle schede **Detailed View** e **Summary View** della visualizzazione **Tree Reports**. Qualora non si desideri visualizzare uno specifico errore in un rapporto, è possibile specificare che non venga mostrata una singola istanza o tutte le istanze dell'errore in questione. In tal caso, l'avviso sarà visualizzato solo nella scheda **Hidden Items** della visualizzazione **Other Reports**, a meno che non si modifichi l'impostazione e si specifichi di visualizzare l'errore nel rapporto.

  - **Informazioni**   Include tutti i problemi non classificati come errori o avvisi. Ad esempio, il numero di oggetti server di Lync Server 2013 Standard Edition in Servizi di dominio Active Directory è classificato come un problema di informazione.
    
    I problemi di informazioni sono visualizzati nella scheda **All Issues** della visualizzazione **List Reports** e nella scheda **Detailed View** della visualizzazione **Tree Reports**.

Lync Server 2013 Best Practices Analyzer non apporta modifiche all'ambiente per risolvere i problemi. L'analisi rileva solo i problemi potenziali e fornisce rapporti che contengono informazioni sulla modalità di risoluzione di ogni problema.

Facendo clic su un problema, si visualizzano una spiegazione e alcune opzioni relative a specifici problemi ed è possibile eseguire una delle operazioni seguenti:

  - Trovare informazioni più dettagliate sul problema e sulla modalità di risoluzione.

  - Non visualizzare più problemi nei rapporti:
    
      - Non visualizzare più problemi per l'istanza selezionata.
    
      - Non visualizzare più problemi per tutte le istanze relative a un determinato problema.
    
    Affinché i problemi non siano più visualizzati nei rapporti, accedere alla scheda **Hidden Items** della visualizzazione **Other Reports**. Nello stesso percorso è possibile specificare di mostrare nuovamente i problemi nei rapporti.

Per informazioni dettagliate sulla risoluzione di specifici problemi, vedere [Analisi e risoluzione dei problemi identificati da Best Practices Analyzer](lync-server-2013-analyzing-and-resolving-issues-identified-by-best-practices-analyzer.md).

