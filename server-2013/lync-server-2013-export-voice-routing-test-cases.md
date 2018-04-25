---
title: 'Lync Server 2013: Esportare test case di routing vocale'
TOCTitle: Esportare test case di routing vocale
ms:assetid: 489ac472-1a35-4755-b390-48f7cdf31e94
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425957(v=OCS.15)
ms:contentKeyID: 49300408
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Esportare test case di routing vocale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

I test case rappresentano un modo per verificare le route vocali nell'organizzazione. È possibile definire elementi come il numero da chiamare e i criteri dial plan e vocali da utilizzare, quindi Lync Server può verificare che in tali condizioni il numero specificato possa essere correttamente instradato alla rete PSTN.

I test case, che possono essere creati con il Pannello di controllo di Lync Server, vengono in genere salvati solo nel server in cui il test case viene creato ed eseguito in origine. È comunque possibile esportarli come file XML (con estensione vtest) per poi importarli in altri server. Ciò consente di eseguire gli stessi test in computer diversi in punti diversi della topologia.

## Per esportare un test case di routing vocale

1.  Nel Pannello di controllo di Lync Server fare clic su **Routing vocale** e quindi su **Test routing vocale** .

2.  Nella scheda **Test routing vocale** selezionare il test case (o i test case) da esportare. Per selezionare più test case, fare clic sul primo che si desidera esportare e quindi tenere premuto CTRL e selezionare eventuali altri case da esportare.

3.  Fare clic su **Azione** e quindi su **Esporta test case** .

4.  Nella finestra di dialogo **Salva con nome** selezionare una cartella in cui memorizzare i test case esportati e digitare un nome per il file XML risultante nella casella **Nome file** . Se si esportano più test case, verranno tutti salvati in un unico file XML.

5.  Per salvare i test case, fare clic su **Salva** .

## Vedere anche

#### Attività

[Importare test case di routing vocale in Lync Server 2013](lync-server-2013-import-voice-routing-test-cases.md)

