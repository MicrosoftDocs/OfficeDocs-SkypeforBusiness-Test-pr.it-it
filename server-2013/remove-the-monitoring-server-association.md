---
title: Rimuovere l'associazione di Monitoring Server
TOCTitle: Rimuovere l'associazione di Monitoring Server
ms:assetid: c45b22ae-fc06-484a-a05b-735bd1bb7448
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721877(v=OCS.15)
ms:contentKeyID: 49887743
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rimuovere l'associazione di Monitoring Server

 

_**Ultima modifica dell'argomento:** 2012-10-04_

Per rimuovere il Monitoring Server, è necessario cambiare o cancellare la dipendenza dal pool Front End, dal Front End Server, dal Survivable Branch Appliance e dal Survivable Branch Server associati. Per rimuovere la dipendenza, è possibile modificare le proprietà del pool Front End, del Front End Server, del Survivable Branch Appliance e del Survivable Branch Server. Dopo avere cancellato la dipendenza e aver eliminato il server in Generatore di topologie, si riceve una notifica che indica che verrà eliminato anche l'oggetto dell'archivio di database associato in Generatore di topologie.

## Per rimuovere l'associazione del Monitoring Server

1.  Aprire Lync Server 2013 Front End Server e quindi Generatore di topologie.

2.  Passare al nodo Lync Server 2010.

3.  In Generatore di topologie espandere **Pool Enterprise Edition Front End** , **Standard Edition Front End Server** o **Siti di succursale** a seconda di dove è definito il Monitoring Server.

4.  Se si dispone di un Survivable Branch Server associato, espandere **Siti di succursale** , espandere il nome del sito di succursale e quindi espandere **Survivable Branch Appliance** .
    

    > [!NOTE]
    > <STRONG>Survivable Branch Appliance</STRONG> nell'interfaccia utente si applica sia al Survivable Branch Server che al Survivable Branch Appliance.



5.  Fare clic con il pulsante destro del mouse sul pool, sul server o sul dispositivo associato al Monitoring Server e quindi scegliere **Modifica proprietà** .

6.  In **Modifica proprietà** , in **Generale** , in **Associazioni** , deselezionare la casella di controllo **Associa Monitoring Server** e quindi fare clic su **OK** .

7.  Ripetere il passaggio precedente per qualsiasi altro pool, server o dispositivo associato al Monitoring Server.

8.  Fare clic con il pulsante destro del mouse sul Monitoring Server e quindi scegliere **Elimina** .

9.  In **Elimina archivi dipendenti** fare clic su **OK** .

10. Pubblicare la topologia, verificare lo stato della replica ed eseguire la Distribuzione guidata di Lync Server in base alle esigenze.

