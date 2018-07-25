---
title: Utilizzo del dashboard di monitoraggio in Lync Server 2013
TOCTitle: Utilizzo del dashboard di monitoraggio in Lync Server 2013
ms:assetid: e00e5783-116f-481f-ad17-3af847d6769a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721905(v=OCS.15)
ms:contentKeyID: 49887784
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Utilizzo del dashboard di monitoraggio in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-02-05_

Il Dashboard di monitoraggio offre agli amministratori una veloce panoramica dello stato del sistema Microsoft Lync Server 2013 e del suo utilizzo. Il dashboard è progettato per mostrare una visualizzazione aggregata delle principali metriche di sistema tramite la visualizzazione delle informazioni seguenti:

  - Totali del giorno corrente. Si noti che i valori visualizzati per il giorno corrente rappresentano dati registrati dalla mezzanotte fino all'ora corrente (in base all'ora locale del server di report). Ciò significa che in genere verranno visualizzati i dati per un giorno parziale e non per un periodo di 24 ore. Se l'ora locale del server sono le 8.00, ad esempio, saranno visualizzati dati per otto ore, perché sono trascorse otto ore dalla mezzanotte.

  - Totali per la settimana e totali tendenziali per le sei settimane precedenti.

  - Totali per il mese e totali tendenziali per i sei mesi precedenti (solo per l'utilizzo del sistema).

Si noti che è possibile usare il cmdlet [Get-CsReportingConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsReportingConfiguration) per restituire l'URL per accedere a Relazioni monitoraggio di Lync Server 2013:

    Get-CsReportingConfiguration

Per impostazione predefinita, il Dashboard di monitoraggio visualizza i dati per le metriche seguenti per la settimana corrente (e i totali tendenziali per le sei settimane precedenti):

## Metriche di utilizzo del sistema

**Registrazione**

  - Accessi utente univoci

**Peer-to-peer**

  - Totale sessioni

  - Sessioni di messaggistica istantanea

  - Sessioni audio

  - Sessioni video

  - Condivisione applicazioni

  - Totale minuti sessioni audio

  - Media minuti sessioni audio

**Conferenza**

  - Totale conferenze

  - Conferenze di messaggistica istantanea

  - Conferenze audio e video

  - Conferenze di condivisione applicazioni

  - Conferenze Web

  - Totale organizzatori

  - Totale minuti di conferenza audio/video

  - Media minuti di conferenza audio/video

  - Totale conferenze PSTN

  - Totale partecipanti PSTN

  - Totale minuti partecipante PSTN

Oltre alle metriche di utilizzo del sistema, le metriche seguenti visualizzano i totali per il giorno corrente e i sei giorni precedenti (se si seleziona **Visualizzazione settimanale**) o per la settimana corrente e le sei settimane precedenti se si seleziona **Visualizzazione mensile**.

## Diagnostica chiamate per utente

**Utenti con errori di chiamata**

  - Totale utenti con errori di chiamata

  - Organizzatori conferenza con errori di chiamata

**Utenti con chiamate con qualità insufficiente**

  - Totale utenti con chiamate con qualità insufficiente

## Diagnostica chiamate

Peer-to-peer

  - Totale errori

  - Frequenza generale errori

  - Frequenza errori messaggistica istantanea

  - Frequenza errori audio

  - Frequenza errori condivisione applicazioni

Conferenza

  - Totale errori

  - Frequenza generale errori

  - Frequenza errori messaggistica istantanea

  - Frequenza errori audio/video

  - Frequenza errori condivisione applicazioni

Primi 5 server per sessioni non riuscite

## Diagnostica qualità multimediale

Peer-to-peer

  - Totale chiamate con qualità insufficiente

  - Percentuale chiamate con qualità insufficiente

  - Chiamate PSTN con qualità insufficiente

Conferenza

  - Totale chiamate con qualità insufficiente

  - Percentuale chiamate con qualità insufficiente

  - Chiamate PSTN con qualità insufficiente

Server peggiori in base alla percentuale di chiamate con qualità insufficiente

## Utilizzo del Dashboard di monitoraggio

Come accennato, vengono visualizzati per impostazione predefinita i totali per la settimana corrente e i valori tendenziali per le sei settimane precedenti. Se si preferisce visualizzare i totali per il mese corrente e i valori tendenziali per i sei mesi precedenti, fare clic sul collegamento **Visualizzazione mensile** nell'angolo in alto a destra del dashboard. Se si decide di visualizzare i totali mensili, il testo del collegamento diventerà **Visualizzazione settimanale** e sarà possibile fare clic su tale collegamento per tornare alla visualizzazione settimanale.

> [!tip]  
> Il Dashboard di monitoraggio consente esclusivamente di esaminare i totali per la settimana o il mese corrente e i valori tendenziali per le sei settimane o i sei mesi precedenti. Non è possibile modificare queste date e ore. Non è possibile, ad esempio, utilizzare il Dashboard per visualizzare i totali dei rapporti per un periodo di nove mesi.

I valori indicati nelle colonne **Questa settimana**, **Questo mese** o **Oggi** sono collegati a informazioni più dettagliate sull'elemento. Tenere presente che il nome della colonna e i valori visualizzati in tale colonna spesso variano a seconda della metrica scelta e della visualizzazione selezionata, ovvero settimanale o mensile. Se si fa clic sui totali visualizzati per la metrica **Accessi utente univoci**, ad esempio, verrà visualizzato il **Rapporto registrazione utenti** per il periodo di tempo specificato. È possibile tornare al Dashboard di monitoraggio in qualsiasi momento facendo clic su **Dashboard**.

> [!tip]  
> È inoltre possibile accedere alla home page dei rapporti di Monitoring Server facendo clic sul collegamento <strong>Rapporti</strong> nell'angolo in alto a destra del Dashboard.

Nella colonna **Tendenza** viene visualizzato un semplice grafico a linee che mostra i totali per le sei settimane precedenti (oppure, a seconda della metrica e dell'intervallo di tempo, per i sei giorni o i sei mesi precedenti). Questi semplici grafici a linee visualizzano un punto dati senza etichetta per ogni periodo di tempo, ad esempio un punto dati per ognuna delle sei settimane precedenti. È comunque possibile recuperare i valori effettivi per questi grafici posizionando il puntatore del mouse sul grafico. In questo modo, i valori massimo e minimo nel grafico vengono visualizzati in una descrizione comandi.

## Esportazione dei dati dal Dashboard di monitoraggio

Il Dashboard di monitoraggio offre vari modi per esportare la visualizzazione corrente. Sulla barra degli strumenti del dashboard è disponibile un'icona a forma di disco floppy con una freccia verde. Se si fa clic su questa icona, viene visualizzato un elenco a discesa con i formati di esportazione dei dati seguenti:

  - File XML con dati del rapporto

  - CSV (delimitato da virgole)

  - PDF

  - MHTML (archivio Web)

  - Excel

  - File TIFF

  - Word

Per esportare la visualizzazione corrente del dashboard e i relativi valori, fare clic sull'opzione di esportazione desiderata. Lync Server 2013 genera un rapporto nel formato specificato e consente di aprirlo o salvarlo. Si noti che per impostazione predefinita Lync Server assegna al rapporto il titolo **Dashboard di monitoraggio** e lo salva nella cartella Download. Per assegnare al rapporto un nome diverso o archiviarlo in una cartella diversa, fare clic sulla freccia accanto al pulsante **Salva** e quindi su **Salva con nome**. Se il nome **Dashboard di monitoraggio** e il salvataggio nella cartella Download sono accettabili, è sufficiente fare clic sul pulsante **Salva**.

È possibile che durante il tentativo di esportazione dei dati del dashboard venga visualizzata una finestra di dialogo **Avviso di sicurezza** con il messaggio "Le impostazioni correnti non consentono il download del file". In questo caso, eseguire le operazioni seguenti:

  - In Internet Explorer selezionare **Opzioni Internet**.

  - Nella finestra di dialogo **Opzioni Internet** fare clic su **Siti attendibili** nella scheda **Sicurezza** e quindi fare clic su **Siti**.

  - Nella finestra di dialogo **Siti attendibili** fare clic su **Aggiungi** per aggiungere l'istanza di Lync Server 2013 che esegue i rapporti di Lync Server 2013 alla raccolta di siti Web attendibili.

  - Fare clic su **Chiudi** e quindi su **OK**.

Sarà poi necessario aggiornare il Dashboard di monitoraggio prima che le modifiche diventino effettive. A tale scopo, premere F5 oppure fare clic sull'icona **Aggiorna** sulla barra degli strumenti del dashboard. (L'icona **Aggiorna** è un cerchio che contiene due frecce verdi.)

È inoltre possibile creare un foglio di calcolo di Excel con feed di dati dinamici, che include collegamenti ai dati più aggiornati del Dashboard di monitoraggio. Per creare un file di feed di dati dinamico, fare clic sull'icona arancione **Esporta in feed di dati** sulla barra degli strumenti.

Se si preferisce stampare il dashboard corrente, fare clic sull'icona a forma di stampante sulla barra degli strumenti.

