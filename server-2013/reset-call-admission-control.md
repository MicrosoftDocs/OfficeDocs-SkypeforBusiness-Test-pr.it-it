---
title: Reimpostare il controllo di ammissione di chiamata
TOCTitle: Reimpostare il controllo di ammissione di chiamata
ms:assetid: 5873f56c-f3d6-4d73-beea-c9f37d5077f6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688064(v=OCS.15)
ms:contentKeyID: 49887572
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Reimpostare il controllo di ammissione di chiamata

 

_**Ultima modifica dell'argomento:** 2012-10-11_

Se il servizio Controllo di ammissione di chiamata (CAC) è ospitato da un pool Front EndLync Server 2010, è necessario spostarlo in un pool Lync Server 2013 prima di rimuovere il pool Front EndLync Server 2010.

## Per reimpostare il servizio Controllo di ammissione di chiamata

1.  Aprire il Generatore di topologie.

2.  Fare clic con il pulsante destro del mouse sul nodo del sito e quindi scegliere **Modifica proprietà** .

3.  In **Impostazione controllo di ammissione di chiamata** assicurarsi che l'opzione **Abilita il controllo di ammissione di chiamata** sia selezionata.

4.  In **Pool Front End per eseguire il servizio Controllo di ammissione di chiamata (CAC)** , selezionare il pool Lync Server 2013 che deve ospitare il servizio e quindi fare clic su **OK** .

5.  Pubblicare la topologia.

