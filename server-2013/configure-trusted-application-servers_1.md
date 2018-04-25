---
title: Configurare i server applicazioni attendibili
TOCTitle: Configurare i server applicazioni attendibili
ms:assetid: 47a9e72e-566c-4c23-bec2-760a3098a974
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204865(v=OCS.15)
ms:contentKeyID: 49300400
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare i server applicazioni attendibili

 

_**Ultima modifica dell'argomento:** 2012-10-04_

Se in un ambiente misto si crea un nuovo server applicazioni attendibile dopo aver unito la topologia legacy di Office Communications Server con Lync Server 2013 e si definisce un nuovo server applicazioni attendibile utilizzando il Generatore di topologie, è necessario impostare il pool hop successivo come pool di Lync Server 2013. In un ambiente misto verranno visualizzati nell'elenco a discesa sia il pool legacy Office Communications Server che il pool Lync Server 2013. La selezione del pool legacy *non* è supportata.

## Per selezionare Lync Server 2013 come hop successivo durante la creazione di un server applicazioni attendibile

1.  Aprire una topologia esistente dal Generatore di topologie.

2.  Nel riquadro di sinistra fare clic con il pulsante destro del mouse su **Server applicazioni attendibili** e quindi scegliere **Nuovo pool di applicazioni attendibili** .

3.  Immettere il nome FQDN del pool di applicazioni attendibili in **FQDN pool** e specificare se sarà una distribuzione a server singolo o a più server.

4.  Fare clic su **Avanti** .

5.  Nella pagina **Selezionare l'hop successivo** selezionare il pool Front End Lync Server 2013 dall'elenco.
    
    ![Finestra di dialogo Definisci nuovo pool di applicazioni attendibili](images/JJ204865.ecfe2bb8-758b-4b36-8146-573005c4ab09(OCS.15).jpg "Finestra di dialogo Definisci nuovo pool di applicazioni attendibili")  

6.  Fare clic su **Fine** .

7.  Selezionare il nodo principale **Lync Server** e nel riquadro **Azioni** selezionare **Pubblica** .

8.  Verificare che il **Pool di applicazioni attendibili** sia stato creato e sia associato al pool Front End corretto.

