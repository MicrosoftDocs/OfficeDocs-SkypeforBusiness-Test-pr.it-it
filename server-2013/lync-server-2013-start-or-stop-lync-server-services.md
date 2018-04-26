---
title: Avviare o arrestare i servizi di Lync Server 2013
TOCTitle: Avviare o arrestare i servizi di Lync Server 2013
ms:assetid: 1c70b4ec-9de5-4f7a-a3c9-c0eb76710505
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520958(v=OCS.15)
ms:contentKeyID: 49299856
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Avviare o arrestare i servizi di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-02-05_

È possibile utilizzare Pannello di controllo di Lync Server per avviare o arrestare tutti i servizi di Lync Server 2013 in esecuzione in un determinato computer oppure per avviare o arrestare un servizio specifico.

## Per avviare o arrestare tutti i servizi di Lync Server in un computer

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsServerAdministrator o CsAdministrator, accedere a un computer nella rete in cui è stato distribuito Lync Server 2013.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Topologia** e quindi su **Stato**.

4.  Nella pagina **Stato** ordinare o scorrere l'elenco per trovare il computer in cui sono in esecuzione i servizi che si desidera avviare o arrestare e quindi fare clic su di esso.

5.  Fare clic su **Azione**.

6.  Fare clic su **Avvia tutti i servizi** o **Arresta tutti i servizi**.

## Per avviare o arrestare un servizio specifico

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Topologia** e quindi su **Stato**.

4.  Nella pagina **Stato** ordinare o scorrere l'elenco per trovare il computer in cui è in esecuzione il servizio che si desidera avviare o arrestare e quindi fare clic su di esso.

5.  Fare clic su **Proprietà**.

6.  Ordinare l'elenco dei servizi, se necessario, e fare clic sul servizio da avviare o arrestare.

7.  Fare clic su **Azione**.

8.  Fare clic su **Avvia servizio** o **Arresta servizio**.

9.  Fare clic su **Chiudi**.

## Vedere anche

#### Attività

[Impedire le sessioni per i servizi in Lync Server 2013](lync-server-2013-prevent-sessions-for-services.md)  

#### Ulteriori risorse

[Gestione della topologia di Lync Server 2013](lync-server-2013-managing-the-lync-server-topology.md)

