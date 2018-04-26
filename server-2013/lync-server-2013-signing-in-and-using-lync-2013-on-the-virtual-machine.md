---
title: 'Lync Server 2013: Accesso e utilizzo di Lync 2013 nella macchina virtuale'
TOCTitle: Accesso e utilizzo di Lync 2013 nella macchina virtuale
ms:assetid: 6140fc19-5bef-4b58-9b0f-19112b5ecd00
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204948(v=OCS.15)
ms:contentKeyID: 49300744
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Accesso e utilizzo di Lync 2013 nella macchina virtuale

 

_**Ultima modifica dell'argomento:** 2012-10-03_

Dopo aver abilitato il plug-in VDI, si verificano i passaggi seguenti quando l'utente accede a Lync 2013.

1.  L'utente digita le proprie credenziali nel client Lync 2013 in esecuzione nella macchina virtuale.

2.  Quando Lync rileva la disponibilità del plug-in VDI, Lync richiede all'utente di reimmettere le credenziali. In questa finestra di dialogo è consigliabile che l'utente selezioni la casella di controllo **Salva la password** in modo che non venga richiesta di nuovo l'immissione delle credenziali per gli accessi successivi.

3.  Viene avviata l'associazione di Lync con il plug-in VDI. Prima del completamento dell'associazione, nel client vengono visualizzate due icone nella barra di stato di Lync. L'icona in basso a sinistra indica che non sono disponibili dispositivi audio e l'icona intermittente in basso a destra indica che l'associazione VDI è in corso, come illustrato di seguito:
    
    ![Icona di VDI di Lync che indica la corretta associazione](images/JJ204948.303d618c-4bc8-41c4-8553-2475de0d395e(OCS.15).png "Icona di VDI di Lync che indica la corretta associazione")  

4.  Dopo il completamento dell'associazione VDI, le icone cambiano per indicare il dispositivo audio che verrà utilizzato per le chiamate e indicare il corretto completamento dell'associazione VDI:
    
    ![Icona di associazione VDI di Lync che indica la riuscita dell'operazione](images/JJ204948.57be3387-a3e5-4949-831e-f5ff9fcc5598(OCS.15).png "Icona di associazione VDI di Lync che indica la riuscita dell'operazione")  

5.  Dopo l'associazione di Lync con il plug-in VDI, l'utente potrà visualizzare la propria presenza in dispositivi compatibili con Lync connessi al computer locale e potrà effettuare chiamate e rispondere alle chiamate come di consueto.

