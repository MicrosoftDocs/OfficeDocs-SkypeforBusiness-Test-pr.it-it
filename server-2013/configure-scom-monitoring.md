---
title: Configurare il monitoraggio di SCOM
TOCTitle: Configurare il monitoraggio di SCOM
ms:assetid: 4003d225-2a33-448c-abd9-571750661140
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688033(v=OCS.15)
ms:contentKeyID: 49887532
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare il monitoraggio di SCOM

 

_**Ultima modifica dell'argomento:** 2012-10-04_

Dopo aver eseguito la migrazione a Microsoft Lync Server 2013, è necessario completare alcune attività per configurare Lync Server 2013 in modo che funzioni con System Center Operations Manager.

  - Applicare gli aggiornamenti di Lync Server 2010 a un server scelto per gestire la logica di individuazione centrale.

  - Aggiornare la chiave del Registro di sistema del server candidato all'individuazione centrale.

  - Configurare il server di gestione di System Center Operations Manager principale per sostituire il nodo di individuazione centrale candidato.

Di seguito sono riportate le istruzioni per l'esecuzione di ognuna di tali attività.

**Applicare gli aggiornamenti di Lync Server 2010 a un server scelto per gestire la logica di individuazione centrale.**

1.  Scegliere un server in cui siano installati i file dell'agente System Center Operations Manager e che sia configurato come nodo di individuazione candidato.

2.  Applicare gli aggiornamenti di Lync Server 2010 a questo server. Vedere l'argomento [Applicare gli aggiornamenti di Lync Server 2010](apply-lync-server-2010-updates.md).

**Aggiornare la chiave del Registro di sistema del server candidato all'individuazione centrale.**

1.  Nel server scelto per gestire la logica di individuazione centrale aprire una finestra di comando di Windows PowerShell.

2.  Nella riga di comando digitare quanto segue:
    
    ```
    New-Item -Path "HKLM:\Software\Microsoft\Real-Time Communications\Health"
    ```
    ```
    New-Item -Path "HKLM:\Software\Microsoft\Real-Time Communications\Health\CentralDiscoveryCandidate"
    ```
    

    > [!NOTE]
    > Quando si modifica il Registro di sistema, è possibile che si verifichi un errore dovuto alla mancata riuscita del comando se la chiave del Registro di sistema già esiste. In tal caso, è possibile ignorare l'errore.



**Configurare il server di gestione di System Center Operations Manager principale per sostituire il nodo Watcher di individuazione centrale candidato.**

1.  In un computer in cui è stata installata la console System Center Operations Manager espandere **Oggetti Management Pack** e selezionare **Individuazioni oggetti**.

2.  Fare clic su **Cambia ambito**

3.  Nella pagina **Crea ambito oggetti Management Pack** selezionare **Candidato individuazione LS**.

4.  Sostituire il **Valore effettivo candidato individuazione LS** con il nome del server candidato scelto nella procedura precedente.

Infine, per finalizzare le modifiche, riavviare il servizio di integrità nel server di gestione radice di System Center Operations Manager.

