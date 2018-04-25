---
title: Definizione di un piano di backup e ripristino
TOCTitle: Definizione di un piano di backup e ripristino
ms:assetid: 9f562ef1-3804-41e2-b3e4-d45b2e8c63c9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh202183(v=OCS.15)
ms:contentKeyID: 52062206
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definizione di un piano di backup e ripristino

 

_**Ultima modifica dell'argomento:** 2013-02-17_

La creazione di un piano di backup e ripristino prevede i passaggi seguenti:

  - Sviluppo del piano.

  - Implementazione del piano.

  - Gestione del piano.

## Sviluppo di un piano di backup e ripristino

Dopo aver sviluppato la strategia di backup e ripristino per Lync Server, utilizzarla per documentare un piano di backup e ripristino dettagliato. Il piano deve comunicare chiaramente le priorità e i requisiti per il backup di dati e impostazioni. Per documentare la strategia con maggiore semplicità, è possibile utilizzare le informazioni in [Definizione di una strategia di backup e ripristino](lync-server-2013-establishing-a-backup-and-restoration-strategy.md) e i fogli di lavoro in [Fogli di lavoro per il backup e il ripristino](lync-server-2013-backup-and-restoration-worksheets.md). Il piano deve inoltre contenere criteri in base ai quali stabilire quando e come ripristinare il servizio.

Durante lo sviluppo del piano è necessario considerare i punti seguenti e tenerne conto:

  - La modalità di recupero dei server nel nuovo hardware.

  - La modalità di recupero dei servizi per i quali è necessario l'intervento di più aree aziendali o reparti.

  - La modalità di acquisizione rapida di server di riserva.

  - Il tempo necessario per il ripristino secondo la strategia in questione. Considerare i requisiti dell'organizzazione per l'obiettivo del tempo di ripristino (RTO).

Modificare le procedure di backup e ripristino in questo argomento, aggiungendole ed eliminandole opportunamente a seconda dei server e dei componenti della distribuzione. È inoltre possibile aggiungere dettagli pertinenti, ad esempio la pianificazione dei backup, alle procedure appropriate, per garantire che non venga trascurata alcuna informazione.


> [!NOTE]
> È buona norma creare script per il numero massimo di passaggi possibile, per garantire la qualità e la riproducibilità delle procedure.



Specificare nel piano il responsabile della revisione del piano stesso, il responsabile del test e della convalida di nuove procedure e nuovi strumenti e chi deve approvare eventuali modifiche al piano e alle relative procedure.

Per assicurarsi che il piano di backup e ripristino soddisfi interamente tutti gli obiettivi e tutte le priorità, prima di implementare il piano ottenere l'approvazione da parte dei decisori aziendali e tecnici all'interno dell'organizzazione.

## Implementazione del piano di backup e ripristino

L'implementazione di un piano di backup e ripristino prevede i passaggi seguenti:

  - Test e convalida del piano.

  - Comunicazione del piano.

  - Convalida delle operazioni di backup e ripristino.

## Test e convalida del piano

Le procedure qui descritte sono state sottoposte a test e convalidate in un ambiente lab. Per garantire il funzionamento di queste e altre procedure all'interno dell'ambiente dell'organizzazione, è necessario sottoporre a test e convalidare queste procedure o qualsiasi altra procedura che si desidera implementare. Completare i test e la convalida prima di sottoporre il piano all'approvazione finale.

## Comunicazione del piano

Nel piano di backup e ripristino deve essere descritto chiaramente chi ha il compito di implementare le procedure e le istruzioni dettagliate per l'esecuzione delle procedure stesse. È necessario verificare che tutti i responsabili dei diversi aspetti delle operazioni di backup e ripristino abbiano compreso il piano, la modalità di implementazione di questo e il proprio ruolo all'interno di esso, nonché tutti i requisiti di implementazione relativi agli aspetti seguenti:

  - Backup di pool e server.

  - Ripristino del servizio.

**Backup di pool e server**

Nel piano di backup e ripristino devono essere disponibili tutte le informazioni necessarie per l'esecuzione delle procedure di backup con regolarità costante. Le informazioni principali da comunicare ai membri del team dei responsabili sono le seguenti:

  - Team o persona (individuo o ruolo) responsabile dell'esecuzione del backup di ogni server.

  - Pianificazione specifica del backup per ogni server.

  - Percorsi di backup per ogni tipo di dati (impostazioni, database e condivisioni file).

  - Procedure di backup da seguire e strumenti necessari per l'esecuzione di ogni procedura.

  - Informazioni necessarie per l'esecuzione dei backup, come descritte in [Fogli di lavoro per il backup e il ripristino](lync-server-2013-backup-and-restoration-worksheets.md).

  - Metodi di convalida da utilizzare per verificare la correttezza del backup di dati e impostazioni e la disponibilità di questi per il ripristino. Tali metodi possono comprendere controlli periodici e operazioni di ripristino di prova.

**Ripristino del servizio**

Nel piano di backup e ripristino devono essere disponibili tutte le informazioni necessarie per il ripristino del servizio, nel caso in cui la perdita di dati in uno o più server provochi l'interruzione del servizio. Le informazioni principali da comunicare ai membri del team responsabile sono le seguenti:

  - Team o persona (individuo o ruolo) responsabile di determinare quando è necessario il ripristino del servizio e le procedure da utilizzare per il ripristino, nonché il team o la persona responsabile dell'implementazione delle procedure per ogni scenario di ripristino.

  - Criteri per stabilire le procedure di ripristino più appropriate per una situazione specifica.

  - Stima del tempo necessario per il ripristino del servizio e obiettivo del tempo di ripristino (RTO) in ogni scenario di ripristino.

  - Procedure di ripristino da seguire e strumenti necessari per l'esecuzione di ogni procedura.

  - Informazioni necessarie per il ripristino di dati e impostazioni. I fogli di lavoro sono disponibili in [Fogli di lavoro per il backup e il ripristino](lync-server-2013-backup-and-restoration-worksheets.md).

## Convalida delle operazioni di backup e ripristino

Dopo aver eseguito le operazioni di backup iniziali nell'ambiente di produzione a intervalli specifici, secondo quanto indicato nel piano di backup e ripristino, è necessario verificare che:

  - Il backup venga eseguito come richiesto.

  - I dati e le impostazioni di backup siano accessibili.

  - Sia possibile eseguire le procedure di ripristino entro i tempi dell'obiettivo del tempo di ripristino (RTO) specificati nel piano di backup e ripristino e i risultati soddisfino tutti i requisiti aziendali.

  - I fogli di lavoro di backup siano stati compilati, verificati e archiviati in un luogo sicuro. I fogli di lavoro sono disponibili in [Fogli di lavoro per il backup e il ripristino](lync-server-2013-backup-and-restoration-worksheets.md).

  - Il funzionamento delle procedure di ripristino sia stato sottoposto a test e verificato come previsto, in base a quanto specificato nel piano di backup e ripristino.

## Gestione del piano di backup e ripristino

Una topologia Lync Server è un ambiente dinamico che cambia di pari passo con l'organizzazione. Man mano che l'organizzazione cambia, rivedere il piano di backup e ripristino, sottoponendolo a revisione periodica per verificare che continui a soddisfare le necessità aziendali.

