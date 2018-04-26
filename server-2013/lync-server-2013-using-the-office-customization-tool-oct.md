---
title: Utilizzo dello Strumento di personalizzazione di Office
TOCTitle: Utilizzo dello Strumento di personalizzazione di Office
ms:assetid: 26647cb6-ba84-4ba7-8b6f-2cf86818e530
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204748(v=OCS.15)
ms:contentKeyID: 49299973
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Utilizzo dello Strumento di personalizzazione di Office

 

_**Ultima modifica dell'argomento:** 2012-10-02_

Lo Strumento di personalizzazione di Office fa parte del programma di installazione ed è lo strumento consigliato per molte personalizzazioni. Tramite questo strumento, è possibile personalizzare Office e salvare le personalizzazioni in un file di configurazione dell'installazione con estensione msp. Il file viene inserito nella cartella Aggiornamenti nella posizione di installazione dalla rete. Quando si installa Office, il programma di installazione cerca un file di configurazione dell'installazione nella cartella Aggiornamenti e applica le personalizzazioni. È possibile utilizzare la cartella Aggiornamenti solo per distribuire aggiornamenti software durante un'installazione iniziale di Office 2013.

Lo Strumento di personalizzazione di Office fa parte dell'installazione ed è incluso nelle versioni multilicenza del prodotto. Per eseguirlo, digitare `setup.exe /admin` nella riga di comando dalla radice della posizione di installazione dalla rete che contiene i file di origine di Office 2013. Ad esempio, utilizzare quanto segue:

`\\server\share\Office15\setup.exe /admin`

Gli amministratori utilizzano questo strumento per creare un file di configurazione dell'installazione con estensione msp. Come con lo Strumento di personalizzazione di Office Microsoft Office 2010, gli amministratori possono personalizzare le aree seguenti:

  - **Installazione** Consente di specificare la posizione di installazione predefinita sul client e il nome organizzazione predefinito, origini di installazione di rete aggiuntive, codice Product Key, contratto di licenza con l'utente finale, livello visualizzazione, versioni precedenti di Office da rimuovere, programmi personalizzati da eseguire durante l'installazione, impostazioni di sicurezza e proprietà di installazione.

  - **Funzionalità** Consente di configurare le impostazioni utente e personalizzare la modalità di installazione delle funzionalità di Office. Gli amministratori possono utilizzare lo Strumento di personalizzazione di Office per specificare valori predefiniti iniziali delle impostazioni delle applicazioni Office per gli utenti. Gli utenti possono modificare la maggior parte delle impostazioni dopo l'installazione.

  - **Contenuto aggiuntivo** Consente di aggiungere o rimuovere file, aggiungere o rimuovere voci del Registro di sistema e configurare collegamenti.

  - **Outlook** Consente di personalizzare il profilo Outlook predefinito di un utente, specificare le impostazioni di Exchange, aggiungere account, rimuovere account ed esportare impostazioni, nonché specificare gruppi di invio/ricezione.

Per informazioni sullo Strumento di personalizzazione di Office, vedere [http://go.microsoft.com/fwlink/?linkid=267516\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=267516%26clcid=0x410).

