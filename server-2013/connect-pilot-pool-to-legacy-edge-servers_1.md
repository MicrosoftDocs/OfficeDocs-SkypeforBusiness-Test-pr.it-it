---
title: Connettere il pool pilota ai server perimetrali legacy
TOCTitle: Connettere il pool pilota ai server perimetrali legacy
ms:assetid: 9ed13c41-f3ab-4e1d-beb6-a00152c541e2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205136(v=OCS.15)
ms:contentKeyID: 49301483
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Connettere il pool pilota ai server perimetrali legacy

 

_**Ultima modifica dell'argomento:** 2012-10-02_

Dopo la distribuzione di Lync Server 2013, non è configurata alcuna route di federazione per questo sito. Per utilizzare la route federata utilizzata da Office Communications Server 2007 R2, è necessario configurare Lync Server 2013 per l'utilizzo di tale route.

Per consentire al sito Lync Server 2013 di usare il server Director e il server perimetrale di BackCompatSite, usare il Generatore di topologie per associare il pool perimetrale legacy.

## Per associare il pool di server perimetrali legacy tramite Generatore di topologie

1.  Aprire la topologia del pool pilota in Generatore tipologie

2.  Selezionare il sito di Lync Server 2013.

3.  Scegliere **Modifica proprietà** dal menu **Azioni** .

4.  In **Assegnazione route federazione sito** selezionare **Abilita federazione SIP** e quindi selezionare il server Director di Office Communications Server 2007 R2 o il server perimetrale di Office Communications Server 2007 R2 qualora non siano elencati server Director.
    
    ![Finestra di dialogo Modifica proprietà - Pagina Route di federazione](images/JJ205136.bc13014b-3578-4d9e-9ff7-bdd09130b676(OCS.15).jpg "Finestra di dialogo Modifica proprietà - Pagina Route di federazione")  

5.  Fare clic su **OK** per chiudere la pagina **Modifica proprietà** .

6.  Nel nodo Lync Server 2013 in Generatore di topologie passare a **Server Standard Edition** o **Pool Enterprise Edition Front End** , fare clic con il pulsante destro del mouse sul pool e quindi scegliere **Modifica proprietà** .

7.  In **Associazioni** selezionare la casella di controllo accanto ad **Associa pool di server perimetrali (per componenti multimediali)** .

8.  Nell'elenco, selezionare l'interfaccia del server perimetrale per BackCompatSite.
    
    ![Finestra di dialogo Modifica proprietà - Pagina Generale](images/JJ205136.75045212-03ca-4b82-8337-5dacb487094f(OCS.15).jpg "Finestra di dialogo Modifica proprietà - Pagina Generale")  

9.  Fare clic su **OK** per chiudere la pagina **Modifica proprietà** .

10. In **Generatore di topologie** selezionare il nodo di primo livello **Lync Server**.

11. Scegliere **Pubblica topologia** dal menu **Azione** e quindi fare clic su **Avanti** .

12. Al termine della Pubblicazione guidata fare clic su **Fine** .

