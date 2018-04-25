---
title: Verificare l'ambiente Office Communications Server 2007 R2
TOCTitle: Verificare l'ambiente Office Communications Server 2007 R2
ms:assetid: e051bdd5-e7ef-4754-8705-900b2c57f37c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721906(v=OCS.15)
ms:contentKeyID: 49887785
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verificare l'ambiente Office Communications Server 2007 R2

 

_**Ultima modifica dell'argomento:** 2012-10-16_

Prima di distribuire Lync Server 2013 in uno stato di coesistenza con Office Communications Server 2007 R2, è necessario verificare che i servizi di Office Communications Server 2007 R2 siano configurati e avviati.

**Verificare che il pool sia avviato con lo strumento di amministrazione di Office Communications Server 2007 R2**

1.  Aprire lo strumento di amministrazione di Office Communications Server 2007 R2.

2.  Espandere il nodo **Foresta**, il nodo **Server Standard** o **Pool Enterprise** e quindi il nome del pool o del server.

3.  Verificare che i servizi siano in esecuzione nel server Standard Edition o nel pool Enterprise.
    
    ![Console di amministrazione di Office Communications Server 2007 R2](images/JJ721906.76897b6d-f433-47d2-930d-0816fc30a3c2(OCS.15).jpg "Console di amministrazione di Office Communications Server 2007 R2")

**Controllare gli utenti configurati per Office Communications Server 2007 R2**

1.  Aprire lo strumento di amministrazione di Office Communications Server 2007 R2.

2.  Espandere il nodo **Foresta**, il nodo **Server Standard** o **Pool Enterprise** e quindi il nome del pool o del server.

3.  Fare clic su **Utenti**.

4.  Verificare l'elenco degli utenti di Office Communications Server 2007 R2.
    
    ![Elenco di utenti nello strumento di amministrazione di OCS](images/JJ721906.f6bb7c4f-cbed-4389-8d0a-69a28577f17a(OCS.15).jpg "Elenco di utenti nello strumento di amministrazione di OCS")

**Verificare la configurazione del partner federato XMPP legacy**

1.  Dal server XMPP legacy passare all'applet Strumenti di amministrazione\\Servizi.

2.  Verificare che il servizio gateway XMPP di Office Communications Server sia avviato.
    
    ![Servizio gateway XMPP di Office Communications Server](images/JJ721906.23223724-3c4b-4cb9-ace2-1cab2c3c91c3(OCS.15).jpg "Servizio gateway XMPP di Office Communications Server")

