---
title: Eliminare una coda di Response Group
TOCTitle: Eliminare una coda di Response Group
ms:assetid: 67c7a489-8c5f-4c6b-9387-9d4c11d43695
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg521008(v=OCS.15)
ms:contentKeyID: 49300831
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminare una coda di Response Group

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Utilizzare una delle procedure seguenti per eliminare una coda.

## Per utilizzare il Pannello di controllo di Lync Server per eliminare una coda

1.  Accedere come membro del gruppo RTCUniversalServerAdmins oppure come membro di uno dei ruoli amministrativi predefiniti che supportano Response Group.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Response Group** e quindi su **Coda**.

4.  Nel campo di ricerca digitare tutto o parte del nome della coda che si desidera eliminare.

5.  Nell'elenco delle code fare clic sulla coda desiderata, fare clic su **Modifica** e quindi su **Elimina**.

6.  Fare clic su **OK**.

## Per eliminare una coda utilizzando i cmdlet

1.  Accedere come membro del gruppo RTCUniversalServerAdmins oppure come membro di uno dei ruoli amministrativi predefiniti che supportano Response Group.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Nella riga di comando digitare il comando seguente:
    
        Get-CsRgsQueue -Identity <Application Server service> -Name "<name of queue>" | Remove-CsRgsQueue
    
    Ad esempio:
    
        Get-CsRgsQueue -Identity service:ApplicationServer:redmond.contoso.com -Name "Help Desk" | Remove-CsRgsQueue

