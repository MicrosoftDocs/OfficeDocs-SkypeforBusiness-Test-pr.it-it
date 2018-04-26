---
title: Impedire le sessioni per i servizi in Lync Server 2013
TOCTitle: Impedire le sessioni per i servizi in Lync Server 2013
ms:assetid: 977dcc5c-2aac-48ef-86a1-a8d47b4d9e74
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182553(v=OCS.15)
ms:contentKeyID: 49301419
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Impedire le sessioni per i servizi in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

È possibile utilizzare il Pannello di controllo di Lync Server per evitare che vengano aperte nuove sessioni per tutti i servizi di Lync Server 2013 in esecuzione in un computer specifico o per evitare che vengano aperte nuove sessioni per un servizio di Lync Server 2013 specifico.

## Per impedire nuove sessioni di tutti i servizi di Lync Server in un computer

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsServerAdministrator o CsAdministrator, accedere a un computer nella rete in cui è stato distribuito Lync Server 2013.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Topologia** e quindi su **Stato**.

4.  Nella pagina **Stato** ordinare l'elenco oppure cercare nell'elenco il computer in cui sono in esecuzione i servizi per cui si desidera impedire nuove sessioni, quindi fare clic su di esso.

5.  Fare clic su **Azione**.

6.  Fare clic su **Impedisci nuove sessioni per tutti i servizi**.

## Per impedire nuove sessioni per uno specifico servizio

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsServerAdministrator o CsAdministrator, accedere a un computer nella rete in cui è stato distribuito Lync Server 2013.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Topologia** e quindi su **Stato**.

4.  Nella pagina **Stato** ordinare l'elenco oppure cercare nell'elenco il computer in cui è in esecuzione il servizio da avviare o arrestare, quindi fare clic su di esso.

5.  Fare clic su **Proprietà**.

6.  Ordinare l'elenco dei servizi, se necessario, quindi fare clic sul servizio per cui si desidera impedire nuove sessioni.

7.  Fare clic su **Azione**.

8.  Fare clic su **Impedisci nuove sessioni per il servizio**.

9.  Fare clic su **Chiudi**.

## Vedere anche

#### Ulteriori risorse

[Gestione della topologia di Lync Server 2013](lync-server-2013-managing-the-lync-server-topology.md)

