---
title: Configurazione del computer Lync Server per la partecipazione all'individuazione di System Center
TOCTitle: Configurazione del computer Lync Server per la partecipazione all'individuazione di System Center
ms:assetid: 2f9c9cb0-3120-4571-9cd2-657c2123fe21
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204776(v=OCS.15)
ms:contentKeyID: 49300064
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione del computer Lync Server per la partecipazione all'individuazione di System Center

 

_**Ultima modifica dell'argomento:** 2012-10-20_

Per assicurarsi che il nuovo agente Lync Server partecipi al processo di individuazione per System Center Operations Manager, è necessario completare la procedura seguente su ogni computer in cui è stata installata la console di System Center Operations Manager:

1.  Nella scheda **Amministrazione** fare clic su **Gestito tramite agente**.

2.  Fare clic con il pulsante destro del mouse sul nome del computer e scegliere **Proprietà**. Nella scheda **Sicurezza** della finestra di dialogo **Proprietà** selezionare **Consenti a questo agente di funzionare come proxy e individuare oggetti gestiti sugli altri computer**, quindi fare clic su **OK**.

Dopo aver completato il passaggio 2, riavviare il servizio Agente integrità. Il riavvio del servizio forzerà il rilevamento del nuovo computer. Se non si riavvia il servizio, potrebbero essere necessarie fino a 4 ore prima che il nuovo computer venga rilevato da System Center Operations Manager. Dopo il riavvio del servizio, verificare che nel registro eventi di Operations Manager del computer in questione non vengano registrati eventi di errore.

