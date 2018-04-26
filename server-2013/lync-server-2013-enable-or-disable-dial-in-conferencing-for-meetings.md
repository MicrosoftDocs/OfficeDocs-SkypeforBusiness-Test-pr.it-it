---
title: Abilitare o disabilitare le conferenze telefoniche con accesso esterno per le riunioni
TOCTitle: Abilitare o disabilitare le conferenze telefoniche con accesso esterno per le riunioni
ms:assetid: 418dcf2d-c8d6-4b2c-b1ab-8723c7ef53e0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688036(v=OCS.15)
ms:contentKeyID: 49887535
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare o disabilitare le conferenze telefoniche con accesso esterno per le riunioni

 

_**Ultima modifica dell'argomento:** 2012-11-01_

La procedura seguente descrive come consentire all'utente di partecipare a una riunione utilizzando l'accesso esterno.

## Per abilitare o disabilitare le conferenze telefoniche con accesso esterno

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Servizio di conferenza** e quindi su **Criteri conferenza**.

4.  Nell'elenco dei criteri conferenza selezionare il criterio per il quale abilitare il servizio di conferenza con accesso esterno e quindi fare clic su **Modifica** e su **Mostra dettagli**.

5.  Per consentire agli utenti la partecipazione a una riunione mediante accesso esterno, selezionare la casella di controllo **Consenti conferenza telefonica con accesso esterno PSTN**. Per impostazione predefinita, gli utenti possono connettersi alle riunioni utilizzando la rete PSTN (Public Switched Telephone Network).

6.  Fare clic su **Commit**.

