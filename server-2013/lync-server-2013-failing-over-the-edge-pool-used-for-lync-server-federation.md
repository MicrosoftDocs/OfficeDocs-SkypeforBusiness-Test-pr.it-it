---
title: "Lync Server 2013: Failover pool di server perimetr. usato per federaz di LS"
TOCTitle: Failover del pool di server perimetrali utilizzato per la federazione di Lync Server
ms:assetid: 5c9da0f2-7429-40bb-bb3c-5cc4ecb5a13d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688071(v=OCS.15)
ms:contentKeyID: 49887581
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Failover del pool di server perimetrali utilizzato per la federazione di Lync Server in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-17_

Se il pool di server perimetrali in cui è stato configurata la federazione di Lync Server diventa non disponibile, è necessario modificare la federazione in modo da utilizzare un pool di server perimetrali diverso, affinché la federazione funzioni.

## Failover del pool di server perimetrali utilizzato per la federazione di Lync Server

1.  In un server Front End aprire Generatore di topologie. Espandere **Pool di server perimetrali** e quindi fare clic con il pulsante destro del mouse sul server perimetrale o sul pool di server perimetrali attualmente configurato per la federazione. Scegliere **Modifica proprietà** .

2.  In **Generale** in **Modifica proprietà** deselezionare **Abilita federazione per pool di server perimetrali (porta 5061)** . Fare clic su **OK** .

3.  Espandere **Pool di server perimetrali** e quindi fare clic con il pulsante destro del mouse sul server perimetrale o sul pool di server perimetrali che si desidera utilizzare per la federazione. Scegliere **Modifica proprietà**

4.  In **Generale** in **Modifica proprietà** selezionare **Abilita federazione per pool di server perimetrali (porta 5061)** . Fare clic su **OK** .

5.  Fare clic su **Azione** , selezionare **Topologia** e quindi fare clic su **Pubblica** . Quando richiesto in **Pubblicare la topologia** fare clic su **Avanti** . Al termine della pubblicazione, fare clic su **Fine** .

6.  Nel server perimetrale aprire la Distribuzione guidata di Lync Server. Fare clic su **Installa o aggiorna il sistema Lync Server** e quindi su **Installazione o rimozione componenti di Lync Server** . Fare clic su **Riesegui** .

7.  In Installazione componenti di Lync Server fare clic su **Avanti** . Nella schermata di riepilogo verranno mostrate le azioni man mano che vengono eseguite. Al termine della distribuzione, fare clic su **Visualizza log** per visualizzare i file di log disponibili. Fare clic su **Fine** per completare la distribuzione.
    
    Se il sito che contiene il pool di server perimetrali in errore contiene Front End Server ancora in esecuzione, è necessario aggiornare il servizio Web Conferencing e il servizio A/V Conferencing in questi pool Front End per l'utilizzo di un pool di server perimetrali in un sito remoto ancora funzionante. Per ulteriori informazioni, vedere [Modifica del pool di server perimetrali associato a un pool Front End in Lync Server 2013](lync-server-2013-changing-the-edge-pool-associated-with-a-front-end-pool.md).

## Vedere anche

#### Attività

[Failover del pool di server perimetrali utilizzato per la federazione di XMPP in Lync Server 2013](lync-server-2013-failing-over-the-edge-pool-used-for-xmpp-federation.md)  
[Failback del pool di server perimetrali utilizzato per la federazione di Lync Server o di XMPP in Lync Server 2013](lync-server-2013-failing-back-the-edge-pool-used-for-lync-server-federation-or-xmpp-federation.md)  

#### Concetti

[Ripristino di emergenza dei server perimetrali in Lync Server 2013](lync-server-2013-edge-server-disaster-recovery.md)

