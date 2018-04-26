---
title: Configurazione di un nodo Watcher per la partecipazione all'individuazione di System Center
TOCTitle: Configurazione di un nodo Watcher per la partecipazione all'individuazione di System Center
ms:assetid: 15c5dcfd-603b-47ea-af1b-8714c2ec08af
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204704(v=OCS.15)
ms:contentKeyID: 49299786
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione di un nodo Watcher per la partecipazione all'individuazione di System Center

 

_**Ultima modifica dell'argomento:** 2012-10-22_

Per verificare che il nodo Watcher participi al processo di individuazione per System Center Operations Manager, è necessario completare la seguente procedura nel computer in cui è stata installata la console di System Center Operations Manager:

1.  Nella scheda **Amministrazione** fare clic su **Gestito tramite agente**.

2.  Fare clic con il pulsante destro del mouse sul nome del computer del nodo Watcher e scegliere **Proprietà**. Nella scheda **Sicurezza** della finestra di dialogo **Proprietà** selezionare **Consenti a questo agente di funzionare come proxy e individuare oggetti gestiti sugli altri computer**, quindi fare clic su **OK**.

Dopo aver configurato il nodo Watcher affinché funga da proxy, riavviare il computer. Al termine del riavvio, verificare che nel registro errori di Operations Manager non sia stato registrato alcun evento di errore. Dopo che il computer è stato in esecuzione per circa 15 minuti, utilizzare la console di Operations Manager per accertarsi che i computer di Lync Server siano elencati nella categoria **Lync**.

