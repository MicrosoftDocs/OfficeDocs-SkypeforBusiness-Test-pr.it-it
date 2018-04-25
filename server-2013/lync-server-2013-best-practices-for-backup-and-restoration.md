---
title: Procedure consigliate per il backup e il ripristino
TOCTitle: Procedure consigliate per il backup e il ripristino
ms:assetid: abbce0e4-973a-4624-a0c1-e0f22e1d348b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh202184(v=OCS.15)
ms:contentKeyID: 52062290
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Procedure consigliate per il backup e il ripristino

 

_**Ultima modifica dell'argomento:** 2013-02-21_

In questa sezione sono descritti due tipi di procedure consigliate:

  - Procedure consigliate per il backup e il ripristino.

  - Procedure consigliate per ridurre al minimo le conseguenze di un'emergenza.

## Procedure consigliate per il backup e il ripristino

Per semplificare il processo di backup e ripristino, applicare le seguenti procedure consigliate durante il backup o il ripristino dei dati:

  - Eseguire backup regolari a intervalli appropriati. Il piano di rotazione e il tipo di backup più semplici e comunemente utilizzati corrispondono a un backup notturno completo dell'intero database di SQL Server. Se dovesse essere necessario il ripristino, il relativo processo richiederebbe un solo backup e andrebbero persi al massimo i dati di un giorno.

  - Se per apportare modifiche alla configurazione si utilizzano i cmdlet o il Pannello di controllo di Lync Server, eseguire un backup snapshot del file di configurazione della topologia (Xds.mdf) tramite il cmdlet **Export-CsConfiguration** dopo l'esecuzione delle modifiche. In tal modo, in caso di ripristino dei database le modifiche non andranno perse. Il backup di questa configurazione viene eseguito in formato XML e compresso come file ZIP.

  - Verificare che la cartella condivisa che si prevede di utilizzare per il backup di Lync Server disponga di spazio su disco sufficiente per tutti i dati di backup.

  - Per migliori prestazioni dei server e per una migliore esperienza utente, pianificare i backup nei periodi in cui l'utilizzo di Lync Server è generalmente ridotto .

  - Verificare la sicurezza del percorso di backup dei dati. È consigliabile un percorso remoto.

  - Mantenere i file di backup in una posizione disponibile, nel caso in cui sia necessario ripristinare i dati.

  - Pianificare test periodici dei processi di ripristino supportati dall'organizzazione.

  - Convalidare i processi di backup e ripristino in anticipo per garantire che funzionino come previsto.

## Procedure consigliate per ridurre al minimo le conseguenze di un'emergenza

La strategia migliore per gestire le interruzioni più gravi dei servizi, dovute a eventi non gestibili quali interruzioni dell'alimentazione o improvvisi errori hardware, è ipotizzare che accadano e pianificare di conseguenza.

Se i servizi Lync, in caso di interruzioni o problemi anche minimi, sono critici per l'organizzazione, è consigliabile valutare l'implementazione di pool accoppiati di server Front End, come descritto in [Pianificazione per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md). Se quindi si verifica un'emergenza per uno di questi pool, un amministratore può fare in modo che gli utenti di tale pool utilizzino l'altro pool, con un periodo di inattività minimo.

I piani di gestione delle emergenze sviluppati all'interno della strategia di backup e ripristino devono includere quanto segue:

  - Disponibilità immediata dei supporti software e degli aggiornamenti software e firmware.

  - Gestione di record dell'hardware e del software.

  - Backup regolare dei dati e monitoraggio dell'integrità dei backup.

  - Formazione del personale sul ripristino di emergenza e sulla documentazione delle procedure ed esecuzione di esercitazioni di simulazione.

  - Disponibilità di hardware sostitutivo o, se è presente un contratto di servizio, contrattazione con i fornitori di hardware per sostituzioni rapide.

  - Luoghi separati per la conservazione dei file di log delle transazioni (con estensione ldf) e dei file di database (con estensione mdf).

