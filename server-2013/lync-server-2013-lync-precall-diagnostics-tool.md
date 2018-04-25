---
title: Strumento Lync PreCall Diagnostics in Lync Server 2013
TOCTitle: Strumento Lync PreCall Diagnostics in Lync Server 2013
ms:assetid: 0ff291ec-cfb4-43eb-b5d6-a7a325681e3f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn451255(v=OCS.15)
ms:contentKeyID: 59602745
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Strumento Lync PreCall Diagnostics in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-01-14_

Lo strumento Lync PreCall Diagnostics (PCD) è un'applicazione basata su client che consente di verificare l'impatto dello stato corrente della rete sulla qualità audio di una chiamata VoIP aziendale imminente.

PCD è utile soprattutto nelle situazioni in cui l'ultimo hop di una rete potrebbe risultare il più debole, ad esempio nel caso di computer portatili su una rete Wi-Fi pubblica o di utenti privati. PCD crea un piccolo flusso di pacchetti che attraversa questo tratto finale della rete, analizza il flusso di pacchetti per stimare l'impatto che l'instabilità e la perdita di pacchetti in questo tratto possono avere sulla qualità audio e quindi genera un report. PCD può essere eseguito continuamente sul client anche mentre vengono effettuate le chiamate. Il flusso di pacchetti non incide in modo significativo sulla larghezza di banda.

**La versione più recente di PCD, ovvero la 1.1, include i seguenti miglioramenti:**

  - Supporto per password più lunghe, fino a 127 caratteri

  - Opzioni di diagnostica aggiuntive per i problemi di accesso e autenticazione

  - Supporto ottimizzato per le distribuzioni ibride di Lync

  - Aggiornamenti per la selezione credenziali

  - Stabilità ottimizzata

Commenti e suggerimenti ed eventuali problemi o richieste di supporto possono essere inviati all'alias [PCD Feedback](mailto:pcdfb@microsoft.com) all'indirizzo <pcdfb@microsoft.com>.

Questo argomento include le sezioni seguenti:

  - Versioni di Lync PCD

  - Requisiti di sistema di Lync PCD

  - Funzionalità di Lync PCD

  - Esecuzione di Lync PCD

  - Disinstallazione di Lync PCD

## Versioni di Lync PCD

In questa sezione vengono descritte le versioni seguenti dello strumento disponibili in download gratuitamente:

  - App desktop di Windows ([http://go.microsoft.com/fwlink/?LinkId=327914](http://go.microsoft.com/fwlink/p/?linkid=327914))

  - App moderna di Windows 8 ([http://go.microsoft.com/fwlink/?LinkId=322110](http://go.microsoft.com/fwlink/p/?linkid=322110))


> [!NOTE]
> Gli utenti di Office 365 Lync possono usare entrambe le versioni di PCD.



Se si desidera usare una versione precedente di PCD, considerare quanto segue:

  - La versione a 32 bit di PCD può essere scaricata gratuitamente dalla pagina [Office Communications Server 2007 R2, PreCallDiagnostic Resource Kit Tool (32 Bit)](http://go.microsoft.com/fwlink/p/?linkid=164769) nell'Area download Microsoft.

  - La versione a 64 bit di PCD è inclusa in Office Communications Server 2007 R2 Resource Kit Tools, un set di informazioni disponibile in download gratuitamente dalla pagina [Office Communications Server 2007 R2 Resource Kit Tools](http://go.microsoft.com/fwlink/p/?linkid=145159) nell'Area download Microsoft.

## Requisiti di sistema di Lync PCD


> [!NOTE]
> PCD richiede l'installazione e la configurazione dell'API Unified Communications Web (UCWA) per supportare i client mobili nella distribuzione di Lync Server. UCWA viene installata con Lync Server.



## Requisiti dell'app desktop di Windows

  - Qualsiasi edizione del sistema operativo Windows 7 o Windows 8

  - Microsoft .NET Framework 4.5 disponibile all'indirizzo [http://go.microsoft.com/fwlink/?LinkId=327790](http://go.microsoft.com/fwlink/p/?linkid=327790)

## Requisiti dell'app moderna di Windows 8

  - Qualsiasi edizione del sistema operativo Windows 8

  - Microsoft .NET Framework 4.5 disponibile all'indirizzo [http://go.microsoft.com/fwlink/?LinkId=327790](http://go.microsoft.com/fwlink/p/?linkid=327790)

## Funzionalità di Lync PCD

Lync PCD include le funzionalità seguenti:

  - Esecuzione in modalità On Demand predefinita (burst di 2 minuti)

  - Esecuzione in modalità Always On (fino a 24 ore in visualizzazione ancorata)

  - Visualizzazione cronologica delle esecuzioni dei test

  - Diagnostica degli errori di accesso (solo Lync PCD per Windows 8)

![Cattura di schermata di accesso in corso alle funzionalità di Lync PCD](images/Dn451255.7e0eb891-1481-47ae-8d63-164468f69c96(OCS.15).png "Cattura di schermata di accesso in corso alle funzionalità di Lync PCD")

  - Visualizzazione grafica della metrica di rete: Network MOS, perdita di pacchetti e instabilità media nel tempo di arrivo tra i pacchetti a schermo intero e in visualizzazione ancorata.

**Visualizzazione a schermo intero**

![Grafici dei risultati del test eseguito con lo strumento PreCall Diagnostic](images/Dn451255.5d01fd94-9e59-4823-96c7-7a1c83dd7d31(OCS.15).png "Grafici dei risultati del test eseguito con lo strumento PreCall Diagnostic")

**Visualizzazione ancorata**

![Risultati del test di utilizzo dello strumento PreCall Diagnostic](images/Dn451255.30501ba7-22d1-4db1-9297-56cf7dc6721c(OCS.15).png "Risultati del test di utilizzo dello strumento PreCall Diagnostic")

## Esecuzione di Lync PCD

## Esecuzione dell'app desktop di Windows

1.  Per avviare PCD in un sistema Windows 7, scegliere **PreCall Diagnostics** dal menu **Start**.
    
    Per avviare PCD in un sistema Windows 8, fare clic sull'icona nella schermata Start o cercare “PreCall Diagnostics”.
    
    ![Icona dello strumento PreCall Diagnostic](images/Dn451255.c9800fde-54f6-4efe-bb35-1a38064ec380(OCS.15).png "Icona dello strumento PreCall Diagnostic")

2.  All'avvio dello strumento, selezionare il metodo preferito per fornire le credenziali e la modalità operativa di rete nella finestra di dialogo **PreCall Diagnostics Tool Options**, quindi scegliere **OK**:

3.  Fare clic sul pulsante **Start Test** per avviare l'esecuzione della diagnostica.
    
    Se è stata selezionata l'opzione **Use network credentials**, il test inizierà immediatamente.
    
    Se è stata selezionata l'opzione **Let me enter my credentials**, verrà visualizzata la finestra di dialogo **Windows Security**. Il test verrà avviato dopo avere immesso le credenziali.

## Esecuzione dell'app moderna di Windows 8


1.  Per avviare PCD, selezionare l'icona nella schermata Start o cercare “PreCall Diagnostics.”
    
    ![Icona dello strumento PreCall Diagnostic](images/Dn451255.c9800fde-54f6-4efe-bb35-1a38064ec380(OCS.15).png "Icona dello strumento PreCall Diagnostic")

2.  All'avvio dello strumento fornire le credenziali di Lync e quindi scegliere **OK**.
    
    ![Accesso allo strumento Lync PreCall Diagnostics](images/Dn451255.88039914-4c68-48f6-a9fa-58cb4e3f3488(OCS.15).jpg "Accesso allo strumento Lync PreCall Diagnostics")

3.  Fare clic sul pulsante **Start test** per avviare l'esecuzione della diagnostica.

## Disinstallazione di Lync PCD

Per rimuovere Lync PCD, seguire la procedura in base al sistema operativo:

  - In un sistema Windows 7 aprire **Pannello di controllo**, selezionare **Programmi e funzionalità** e fare doppio clic su **Lync 2013 PreCall Diagnostics**.

  - In un sistema Windows 8 fare clic con il pulsante destro del mouse sul riquadro PCD e scegliere **Disinstalla** sulla barra dell'app nella parte inferiore della schermata Start.

