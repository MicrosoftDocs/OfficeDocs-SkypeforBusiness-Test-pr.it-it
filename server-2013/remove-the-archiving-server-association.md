---
title: Rimuovere l'associazione del server di archiviazione
TOCTitle: Rimuovere l'associazione del server di archiviazione
ms:assetid: dabac157-71ee-4afe-b0b6-4a083d165ffb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721903(v=OCS.15)
ms:contentKeyID: 49887780
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rimuovere l'associazione del server di archiviazione

 

_**Ultima modifica dell'argomento:** 2012-10-04_

Per rimuovere un server di archiviazione, è necessario modificare o eliminare la dipendenza dal pool Front End, dal Front End Server, dal Survivable Branch Appliance e dal Survivable Branch Server associati. Per rimuovere la dipendenza, è necessario modificare le proprietà del pool Front End, del Front End Server, del Survivable Branch Appliance e del Survivable Branch Server. Dopo aver eliminato la dipendenza e il server in Generatore di topologie, si riceve una notifica in cui viene indicato che verrà eliminato anche l'oggetto archivio di database associato in Generatore di topologie.

## Per rimuovere l'associazione a un server di archiviazione

1.  Aprire Lync Server 2013 Front End Server e quindi Generatore di topologie.

2.  Passare al nodo Lync Server 2010.

3.  In Generatore di topologie espandere **Pool Enterprise Edition Front End**, **Standard Edition Front End Server** o **Siti di succursale** a seconda di dove è definito il server di archiviazione.

4.  Se si dispone di un Survivable Branch Server associato, espandere **Siti di succursale** , espandere il nome del sito di succursale e quindi espandere **Survivable Branch Appliance** .
    

    > [!NOTE]
    > <STRONG>Survivable Branch Appliance</STRONG> nell'interfaccia utente si applica sia al Survivable Branch Server che al Survivable Branch Appliance.



5.  Fare clic con il pulsante destro del mouse sul pool, sul server o sul dispositivo associato al server di archiviazione e quindi scegliere **Modifica proprietà**.

6.  In **Modifica proprietà** , **Generale** , **Associazioni** deselezionare la casella di controllo **Associa server di archiviazione** e quindi fare clic su **OK** .

7.  Ripetere il passaggio precedente per gli altri eventuali pool, server o dispositivi associati al server di archiviazione che si desidera rimuovere.

8.  Fare clic con il pulsante destro del mouse sul server di archiviazione e quindi scegliere **Elimina**.

9.  In **Elimina archivi dipendenti** fare clic su **OK** .

10. Pubblicare la topologia, controllare lo stato di replica e quindi eseguire la Distribuzione guidata di Lync Server secondo le esigenze.

