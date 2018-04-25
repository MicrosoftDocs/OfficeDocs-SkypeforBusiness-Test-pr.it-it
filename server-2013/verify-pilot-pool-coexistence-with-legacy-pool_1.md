---
title: Verificare la coesistenza del pool pilota con il pool legacy
TOCTitle: Verificare la coesistenza del pool pilota con il pool legacy
ms:assetid: 597d0fa6-ca04-4521-b1c2-72d7f35ecd08
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204914(v=OCS.15)
ms:contentKeyID: 49300637
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verificare la coesistenza del pool pilota con il pool legacy

 

_**Ultima modifica dell'argomento:** 2012-09-28_

## Verificare il pool nello strumento di amministrazione di Office Communications Server 2007 R2

1.  Aprire lo strumento di amministrazione di Office Communications Server 2007 R2.

2.  Espandere il nodo **Foresta**, il nodo **Server Standard** o **Pool Enterprise** e quindi il nome del pool o del server.

3.  Assicurarsi che nel pool i servizi di Office Communications Server 2007 R2 siano in esecuzione.
    
    ![Console di amministrazione di Office Communications Server 2007 R2](images/JJ721906.76897b6d-f433-47d2-930d-0816fc30a3c2(OCS.15).jpg "Console di amministrazione di Office Communications Server 2007 R2")  

## Verificare il pool pilota nel Pannello di controllo di Lync Server 2013

1.  Con un account utente membro del ruolo CsAdministrator accedere al Front End Server Lync Server 2013.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Fare clic su **Topologia** .

4.  Verificare che i server distribuiti siano presenti nel pool pilota.
    
    ![Pagina della topologia nel Pannello di controllo di Lync Server](images/JJ204914.a3d1ba5f-c1a7-45e8-b9a5-7cb07b01af8c(OCS.15).jpg "Pagina della topologia nel Pannello di controllo di Lync Server")  

## Verificare che i servizi di Lync Server 2013 siano avviati

1.  Nel Front End Server Lync Server 2013 aprire l'applet **Servizi** nel gruppo **Strumenti di amministrazione** .

2.  Verificare che i servizi elencati corrispondano all'elenco mostrato nella figura che segue.
    
    ![Pagina Servizi in cui sono indicati i servizi di Lync avviati](images/JJ204914.fd35d54a-2ab6-4c09-b5e9-fd5bf10f6f51(OCS.15).jpg "Pagina Servizi in cui sono indicati i servizi di Lync avviati")

