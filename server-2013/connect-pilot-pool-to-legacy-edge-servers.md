---
title: Connettere il pool pilota ai server perimetrali legacy
TOCTitle: Connettere il pool pilota ai server perimetrali legacy
ms:assetid: c3b67220-5705-47f6-852e-415204f3626c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721875(v=OCS.15)
ms:contentKeyID: 49887742
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Connettere il pool pilota ai server perimetrali legacy

 

_**Ultima modifica dell'argomento:** 2012-09-29_

Dopo aver distribuito Lync Server 2013, è necessario configurare una route di federazione per il sito. Per utilizzare la route federata utilizzata da Lync Server 2010, è necessario configurare Lync Server 2013 per l'utilizzo della route.

Per abilitare il sito di Lync Server 2013 per l'utilizzo del server Director e del server perimetrale della distribuzione di Lync Server 2010, utilizzare Generatore di topologie per associare il pool di server perimetrali legacy.

## Per associare il pool di server perimetrali legacy tramite Generatore di topologie

1.  Aprire **Generatore di topologie**.

2.  Selezionare il sito, disponibile direttamente sotto il nodo **Lync Server**.

3.  Scegliere **Modifica proprietà** dal menu **Azioni** .

4.  Nel riquadro sinistro selezionare **Route di federazione**.

5.  In **Assegnazione route federazione sito** selezionare **Abilita federazione SIP** e quindi selezionare il server Director di Lync Server 2010 o il server perimetrale di Lync Server 2010 qualora non siano elencati server Director.
    
    ![Modifica proprietà - Pagina Route di federazione](images/JJ721875.5f1d04c3-c724-426d-b27d-3fe89c6c5cfb(OCS.15).jpg "Modifica proprietà - Pagina Route di federazione")  

6.  Fare clic su **OK** per chiudere la pagina **Modifica proprietà** .

7.  Nel nodo Lync Server 2013 in Generatore di topologie passare a **Server Standard Edition** o **Pool Enterprise Edition Front End** , fare clic con il pulsante destro del mouse sul pool e quindi scegliere **Modifica proprietà** .

8.  In **Associazioni** selezionare la casella di controllo accanto ad **Associa pool di server perimetrali (per componenti multimediali)** .

9.  Selezionare il server perimetrale legacy nell'elenco.
    
    ![Finestra di dialogo Modifica proprietà - Selezione del server perimetrale legacy](images/JJ721875.feae8156-540e-4804-bb0a-2b5736ec2900(OCS.15).jpg "Finestra di dialogo Modifica proprietà - Selezione del server perimetrale legacy")  

10. Fare clic su **OK** per chiudere la pagina **Modifica proprietà** .

11. In **Generatore di topologie** selezionare il nodo di primo livello **Lync Server**.

12. Scegliere **Pubblica topologia** dal menu **Azione** e quindi fare clic su **Avanti** .

13. Al termine della Pubblicazione guidata fare clic su **Fine** .

