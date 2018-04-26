---
title: Configurare i server applicazioni attendibili
TOCTitle: Configurare i server applicazioni attendibili
ms:assetid: 20c3815f-3048-4940-8c0f-cdfcd0801d5d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204735(v=OCS.15)
ms:contentKeyID: 49299904
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare i server applicazioni attendibili

 

_**Ultima modifica dell'argomento:** 2014-11-05_

In un ambiente misto, se si crea un nuovo server applicazioni attendibili, è necessario impostare il pool hop successivo come pool di Lync Server 2013. In un ambiente misto, sia il pool di Lync Server 2010 legacy sia il pool di Lync Server 2013 figurano nell'elenco a discesa. La selezione del pool legacy non è supportata.

**Selezionare Lync Server 2013 come hop successivo quando si crea un server applicazioni attendibili**

1.  Apre lo strumento di generazione topologia

2.  Nel riquadro di sinistra fare clic con il pulsante destro del mouse su **Server applicazioni attendibili** e quindi scegliere **Nuovo pool di applicazioni attendibili** .

3.  Immettere il nome FQDN del pool di applicazioni attendibili in **FQDN pool** e specificare se sarà un pool a server singolo o a più server.

4.  Fare clic su **Avanti** .

5.  Nella pagina **Selezionare l'hop successivo** selezionare il pool Front End Lync Server 2013 dall'elenco.

6.  Fare clic su **Fine** .

7.  Selezionare il nodo principale **Lync Server** e nel menu **Azioni** selezionare **Pubblica** .
    
    Verificare che il **Pool di applicazioni attendibili** sia stato creato correttamente e sia associato al pool Front End corretto.

