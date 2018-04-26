---
title: Installazione dei file dell'agente Operations Manager
TOCTitle: Installazione dei file dell'agente Operations Manager
ms:assetid: e2246c44-0c75-43fc-8b04-26e53c5dd572
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205345(v=OCS.15)
ms:contentKeyID: 49302247
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Installazione dei file dell'agente Operations Manager

 

_**Ultima modifica dell'argomento:** 2012-10-20_

Per installare i file agente di Operations Manager nel computer, eseguire le operazioni seguenti.

1.  Nei supporti di installazione di System Center fare doppio clic su **SetupOM.exe**.

2.  Nell'installazione di System Center Operations Manager fare clic su **Installa agente Operations Manager**.

3.  Nell'Installazione guidata di System Center, nella pagina iniziale dell'installazione diSystem Center Operations Manager fare clic su **Avanti**.

4.  Nella pagina **Cartella di destinazione** selezionare la cartella in cui verranno installati i file dell'agente Operations Manager e quindi fare clic su **Avanti**.

5.  Nella pagina **Configurazione gruppo di gestione** selezionare **Specifica informazioni gruppi di gestione** e quindi fare clic su **Avanti**.

6.  Nella pagina **Configurazione gruppo di gestione** digitare il nome del gruppo di gestione di Operations Manager nella casella **Nome gruppo di gestione** e quindi digitare il nome host del server Operations Manager (ad esempio, atl-scom-001) nella casella **Server di gestione**. Se è stato modificato il numero di porta utilizzato da Operations Manager, digitare il nuovo numero di porta nella casella della porta del server di gestione. In caso contrario lasciare il valore predefinito per la porta 5723 e fare clic su **Avanti**.

7.  Nella pagina **Account azione agente** selezionare **Sistema locale** e quindi fare clic su **Avanti**.

8.  Nella pagina **Microsoft Update** selezionare **Non utilizzare Microsoft Update** e quindi fare clic su **Avanti**.

9.  Nella pagina **Pronto per l'installazione** fare clic su **Installa**.

10. Nella pagina **Completamento dell'Installazione guidata di System Center Operations Manager** fare clic su **Fine**.

11. Fare clic su **Esci**.

Se si utilizza System Center 2007 R2, per verificare che l'agente sia stato creato, fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, fare clic su **System Center Operations Manager 2007 R2** e quindi su **Shell di Operations Manager**. Nella shell di Operations Manager digitare il comando seguente di Windows PowerShell e quindi premere INVIO:

    Get-Agent 

Sullo schermo verrà visualizzato un elenco di tutti gli agenti di Operations Manager.

Se si utilizza System Center 2012, eseguire questo comando dalla shell di Operations 2012 Manager:

    Get-SCOMAgent

