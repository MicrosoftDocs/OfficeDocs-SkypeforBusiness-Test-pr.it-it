---
title: 'Lync Server 2013: Modifica del pool di server perimetrali associato a un pool Front End'
TOCTitle: Modifica del pool di server perimetrali associato a un pool Front End
ms:assetid: 369468c7-2c0b-48cc-bbc3-825dad7b85aa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688023(v=OCS.15)
ms:contentKeyID: 49887520
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modifica del pool di server perimetrali associato a un pool Front End in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

Se si verifica un'interruzione di un pool di server perimetrali di un sito, ma il pool Front End dello stesso sito è ancora in esecuzione, sarà necessario impostare il pool Front End in modo che venga utilizzato un pool di server perimetrali di un altro sito fino a quando il pool di server perimetrali non viene ripristinato.

## Modifica del pool di server perimetrali associato a un pool Front End

1.  Nel Generatore di topologie individuare il nome del pool Front End che si vuole modificare.

2.  Fare clic con il pulsante destro del mouse sul pool e quindi scegliere **Modifica proprietà** .

3.  Nella sezione **Associazioni** , in **Associa pool di server perimetrali (per componenti multimediali)** , usare la casella di riepilogo a discesa per selezionare il pool di server perimetrali a cui si vuole associare il pool Front End.

4.  Fare clic su **OK** .

## Vedere anche

#### Concetti

[Ripristino di emergenza dei server perimetrali in Lync Server 2013](lync-server-2013-edge-server-disaster-recovery.md)

