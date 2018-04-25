---
title: Eliminare un flusso di lavoro
TOCTitle: Eliminare un flusso di lavoro
ms:assetid: 0469a6b8-ce1e-459b-bc3d-4c8adf2d97d5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520944(v=OCS.15)
ms:contentKeyID: 49299536
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminare un flusso di lavoro

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Utilizzare una delle procedure seguenti per eliminare un flusso di lavoro.

## Per eliminare un flusso di lavoro utilizzando Pannello di controllo di Lync Server

1.  Accedere come membro del gruppo RTCUniversalServerAdmins oppure come membro di uno dei ruoli amministrativi predefiniti che supportano Response Group.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Response Group** e quindi su **Flusso di lavoro**.

4.  Nella pagina **Flusso di lavoro** fare clic su **Crea o modifica un flusso di lavoro**.

5.  Nel campo di ricerca **Seleziona un servizio** digitare parte o tutto il nome del servizio **ApplicationServer** in cui è ospitato il flusso di lavoro che si desidera eliminare.

6.  Nell'elenco dei servizi fare clic sul servizio desiderato e quindi fare clic su **OK**.
    

    > [!NOTE]
    > Verrà aperta la pagina Web Strumento di configurazione di Response Group. È inoltre possibile aprire la pagina Web Strumento di configurazione di Response Group direttamente da un Web browser connettendosi a <STRONG>https://<EM>&lt;FqdnPoolWeb&gt;</EM>/RgsConfig</STRONG>.



7.  In **Gestisci un flusso di lavoro esistente** individuare il flusso di lavoro da eliminare e quindi in **Azione** fare clic su **Elimina**.

8.  Fare clic su **Sì**.

## Per eliminare un flusso di lavoro utilizzando i cmdlet

1.  Accedere come membro del gruppo RTCUniversalServerAdmins oppure come membro di uno dei ruoli amministrativi predefiniti che supportano Response Group.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Nella riga di comando digitare il comando seguente:
    
        Get-CsRgsWorkflow -Identity <Application Server service> -Name "<name of workflow>" | Remove-CsRgsWorkflow
    
    Ad esempio:
    
        Get-CsRgsWorkflow -Identity service:ApplicationServer:redmond.contoso.com -Name "Help Desk" | Remove-CsRgsWorkflow

