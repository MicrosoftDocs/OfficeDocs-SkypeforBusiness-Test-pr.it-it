---
title: Rimuovere BackCompatSite
TOCTitle: Rimuovere BackCompatSite
ms:assetid: 039650e3-541b-45c2-a682-c4fa08423118
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204637(v=OCS.15)
ms:contentKeyID: 49299524
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rimuovere BackCompatSite

 

_**Ultima modifica dell'argomento:** 2012-09-28_

Dopo avere disattivato tutti i pool e avere disinstallato tutti i server perimetrali, eseguire la procedura di unione guidata del Generatore di topologie per rimuovere **BackCompatSite** .

## Per rimuovere BackCompatSite dal Generatore di topologie

1.  Aprire una distribuzione esistente dal Generatore di topologie.

2.  Scegliere **Unisci topologia 2007 R2** dal menu **Azione** .

3.  Fare clic su **Avanti** per continuare.

4.  Nella pagina **Specifica il server perimetrale legacy** assicurarsi che l'elenco di server perimetrali sia vuoto. Se l'elenco non è vuoto, usare il pulsante **Rimuovi** per rimuovere tutti i server perimetrali legacy e quindi fare clic su **Avanti** .
    
    ![Procedura guidata per l'unione delle topologie - Pagina Specificare installazione server perimetrale](images/JJ204637.fb35a59a-711e-4259-b177-7311df1fed3c(OCS.15).jpg "Procedura guidata per l'unione delle topologie - Pagina Specificare installazione server perimetrale")  

5.  Nella pagina **Specificare la porta SIP interna** fare clic su **Avanti** .

6.  Nella pagina **Riepilogo** fare clic su **Avanti** per iniziare a unire le topologie per rimuovere il sito legacy.

7.  Verificare che nella colonna **Stato** sia visualizzato il valore **Esito positivo** e quindi fare clic su **Fine** per chiudere la procedura guidata.

8.  Nel riquadro sinistro del Generatore di topologie espandere BackCompatSite e verificare che non siano elencati server.

9.  Fare clic con il pulsante destro del mouse su **BackCompatSite** e quindi scegliere **Elimina** .

10. In **Generatore di topologie** selezionare il nodo di primo livello **Lync Server** .

11. Nel menu **Azioni** selezionare **Pubblica topologia** e fare clic su **Avanti** .

12. Al termine della **Pubblicazione guidata** , fare clic su **Fine** per chiudere la procedura guidata.

