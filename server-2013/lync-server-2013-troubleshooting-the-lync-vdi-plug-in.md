---
title: Risoluzione dei problemi del plug-in VDI di Lync e Lync Server 2013
TOCTitle: Risoluzione dei problemi del plug-in VDI di Lync e Lync Server 2013
ms:assetid: 183c9449-b907-409c-b5ed-b02af3bd93ee
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204713(v=OCS.15)
ms:contentKeyID: 49299813
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Risoluzione dei problemi del plug-in VDI di Lync e Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-10_

## Risoluzione dei problemi di installazione del plug-in di Lync VDI in un thin client

In caso di problemi durante l'installazione del plug-in VDI in un thin client, controllare quanto segue:

  - Verificare che nella cartella specificata vi sia sufficiente spazio per le variabili di sistema TEMP e TMP.

  - Verificare che la protezione dalla scrittura sia disattivata. Per istruzioni, consultare la documentazione del produttore del dispositivo.

## Risoluzione dei problemi di abbinamento

Quando l'abbinamento del plug-in VDI non riesce, nell'icona in basso a destra viene visualizzata una "X" rossa come mostrato di seguito:

![Icona di VDI di Lync che indica la corretta associazione](images/JJ204948.303d618c-4bc8-41c4-8553-2475de0d395e(OCS.15).png "Icona di VDI di Lync che indica la corretta associazione")

Di seguito vengono elencate le possibili cause degli errori e le azioni correttive che è possibile intraprendere.

  - **Sono state inserite credenziali non corrette durante l'accesso.**
    
    È necessario uscire da Lync e riaccedere utilizzando le credenziali corrette. Verrà visualizzata di nuovo la finestra di dialogo di abbinamento che segnalerà se l'abbinamento è andato a buon fine.

  - **È in esecuzione un'altra istanza del client desktop remoto.**
    
    Gli utenti che utilizzano Connessione desktop remoto di Windows devono eseguire le operazioni seguenti:
    
    1.  Avviare Gestione attività: premere **Alt+Ctrl+Canc** e quindi fare clic su **Avvia Gestione attività**.
    
    2.  Fare clic sulla scheda **Processi** e cercare tutti i processi denominati **mstsc.exe** nell'elenco.
    
    3.  Selezionare ogni processo **mstsc.exe** e fare clic su **Termina processo**.
    
    4.  Avviare una nuova sessione di desktop remoto e riprovare a connettersi.

  - **I file necessari non sono installati correttamente.**
    
    Dopo l'installazione del plug-in nel computer locale, è necessario che nel percorso C:\\Programmi\\Microsoft Office\\Office15 (o lettera di unità appropriata) siano presenti i seguenti file:
    
      - LyncVdiPlugin.dll
    
      - UcVdi.dll
    
    In caso di problemi di abbinamento VDI, controllare che questi file siano presenti nel computer locale.

  - **Il client Lync è in esecuzione nel computer locale.**
    
    Per utilizzare il plug-in di Lync VDI, è necessario che nel computer locale non sia in esecuzione un client Lync; in caso contrario, l'abbinamento non riesce. Come procedura consigliata, è opportuno non installare un client Lync nel computer locale.

