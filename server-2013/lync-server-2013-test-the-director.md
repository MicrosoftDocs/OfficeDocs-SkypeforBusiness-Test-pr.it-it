---
title: 'Lync Server 2013: Testare il server Director'
TOCTitle: Testare il server Director
ms:assetid: 9627a7e2-28cc-429c-b79b-7c7a27573bb7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398767(v=OCS.15)
ms:contentKeyID: 49301382
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Testare il server Director in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-08_

A questo punto si dispone di un server Director o di un pool di server Director configurato, ma le voci SRV DNS (Domain Name System) continuano a puntare ai client per eseguire l'accesso utilizzando un pool o un server Standard Edition. Prima di modificare il record DNS affinché i client Lync 2013 accedano automaticamente utilizzando il server Director, testare un client facendo in modo che punti manualmente al server Director.

## Per testare la distribuzione

1.  Accedere al computer in cui è installato il Pannello di controllo di Lync Server con un account di dominio che faccia parte del gruppo **CSAdministrator** .

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nel riquadro di spostamento fare clic su **Topologia** e verificare che nella colonna **Stato** sia presente un server con una freccia verde ( ![Icona del server con la freccia verde](images/Gg398767.2263cdb7-7e60-457a-a528-a3a082bd051b(OCS.15).jpg "Icona del server con la freccia verde")) per il Director o il pool di Director.

4.  Connettere due computer client in cui è installato il client Lync Server 2013 e accedere con un account utente diverso abilitato per Lync Server 2013 in entrambi i computer.

5.  In uno dei computer client fare clic sul menu **Opzioni** , selezionare il gruppo di impostazioni **Personale** , fare clic su **Avanzate** , fare clic su **Configurazione manuale** e quindi impostare **Nome server interno o indirizzo IP** sul nome di dominio completo (FQDN) del nuovo Director o pool di Director.

6.  Accedere ad entrambi i client e verificare che il client che si connette utilizzando il Director sia in grado di eseguire correttamente l'accesso, visualizzare lo stato di presenza dell'altro utente e scambiare messaggi istantanei.

