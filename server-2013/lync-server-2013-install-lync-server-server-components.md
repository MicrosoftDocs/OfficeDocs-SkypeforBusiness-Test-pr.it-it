---
title: 'Lync Server 2013: Installazione dei componenti server di Lync Server'
TOCTitle: Installazione dei componenti server di Lync Server
ms:assetid: 186aed6e-7adf-4a92-9f2e-f9a4de5ff202
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398239(v=OCS.15)
ms:contentKeyID: 49299816
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Installazione dei componenti server per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-05-05_

Prima di eseguire i passaggi seguenti, assicurarsi di avere eseguito l'accesso al server con un account utente di dominio sia amministratore locale che membro del gruppo RTCUniversalReadOnlyAdmins in Active Directory.

La Distribuzione guidata di Lync Server consente di installare i componenti necessari per ogni ruolo del server Lync e di attivare il server. In questo articolo sono illustrati i passaggi da eseguire per distribuire il server Standard Edition o il Front End Server nell'infrastruttura di Lync.

## Per installare i componenti di Lync Server

1.  Se la Distribuzione guidata di Lync Server non è in esecuzione, avviarla nel server in cui si desidera installare Lync.

2.  Fare clic su **Installa o aggiorna il sistema Lync Server**.

3.  Nella Distribuzione guidata verificare che accanto a **Passaggio 1: Installazione dell'archivio di configurazione locale** sia visualizzato un segno di spunta verde, che indica che nel server è installata correttamente una copia locale dell'archivio. Se il segno di spunta non è presente, è necessario installare l'archivio di configurazione locale nel server. Eseguire la procedura in [Installare l'archivio di configurazione locale in Lync Server 2013](lync-server-2013-install-the-local-configuration-store.md) e tornare qui.

4.  Quando si è pronti per installare i componenti di Lync Server 2013 nel server, fare clic su **Esegui** accanto a **Passaggio 2: Installazione o rimozione componenti di Lync Server**.

5.  Nella pagina **Installazione componenti di Lync Server** fare clic su **Avanti** per installare i componenti secondo quanto definito nella topologia pubblicata.

6.  Nella pagina **Comandi in esecuzione** verrà visualizzato un riepilogo dei comandi e delle informazioni sull'installazione durante l'esecuzione. Al termine, è possibile utilizzare l'elenco per selezionare un log da esaminare e quindi fare clic su **Visualizza log**.

7.  Al termine dell'installazione dei componenti di Lync Server 2013 e dopo aver verificato i log in base alle necessità, fare clic su **Fine** per completare questo passaggio nell'installazione.
    

    > [!NOTE]
    > Eseguire il riavvio del computer se viene richiesto, operazione che potrebbe essere necessaria se occorre installare Windows Desktop Experience nel computer. Quando il computer è di nuovo operativo, ripetere questa procedura partendo dal passaggio 3 elencato sopra, ovvero eseguire un'altra volta il passaggio 2 della Distribuzione guidata.


