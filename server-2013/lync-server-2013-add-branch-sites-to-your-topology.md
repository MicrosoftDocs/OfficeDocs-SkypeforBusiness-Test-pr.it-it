---
title: 'Lync Server 2013: Aggiungere siti di succursale alla topologia'
TOCTitle: Aggiungere siti di succursale alla topologia
ms:assetid: b9c35fb0-0081-4aeb-8f95-ac2fcc6c3335
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412905(v=OCS.15)
ms:contentKeyID: 49301772
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Aggiungere siti di succursale alla topologia in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-05_

I siti di succursale rappresentano le succursali fisiche connesse alle sedi principali tramite un collegamento WAN. Per aggiungere un sito di succursale alla topologia di Lync, eseguire questa procedura nel sito centrale.

## Per aggiungere siti di succursale alla topologia

1.  Fare clic sul pulsante **Start** , scegliere **Tutti i programmi** , **Microsoft Lync Server** e quindi **Generatore di topologie di Lync Server** .

2.  Nell'albero della console espandere il sito centrale, fare clic con il pulsante destro del mouse su **Siti di succursale** e quindi scegliere **Nuovo sito di succursale** .

3.  Nella finestra di dialogo **Definisci nuovo sito di succursale** fare clic su **Nome** e quindi digitare il nome del sito di succursale.

4.  (Facoltativo) Fare clic su **Descrizione** e quindi digitare una descrizione significativa del sito di succursale.

5.  Fare clic su **Avanti** .

6.  (Facoltativo) Nella successiva finestra di dialogo **Definisci nuovo sito di succursale** eseguire una delle operazioni seguenti:
    
      - Fare clic su **Città** e quindi digitare il nome della città in cui si trova il sito di succursale.
    
      - Fare clic su **Paese** e quindi digitare il nome del paese in cui si trova il sito di succursale.
    
      - Fare clic su **Codice paese** e quindi digitare il codice di chiamata in due cifre per il paese/area geografica in cui si trova il sito di succursale.

7.  Fare clic su **Avanti** e quindi eseguire una delle operazioni seguenti:
    
      - Se nel sito si utilizza un Survivable Branch Appliance o un Survivable Branch Server, assicurarsi che la casella di controllo **Aprire la procedura guidata Nuovo Survivable Branch Appliance al termine di questa procedura guidata** sia selezionata, fare clic su **Fine** e quindi seguire le istruzioni nella procedura guidata visualizzata. Per informazioni sui passaggi della procedura guidata, vedere [Definire un Survivable Branch Appliance o un Survivable Branch Server in Lync Server 2013](lync-server-2013-define-a-survivable-branch-appliance-or-server.md).
    
      - Se nel sito non si utilizza un Survivable Branch Appliance o un Survivable Branch Server, deselezionare la casella di controllo **Aprire la procedura guidata Nuovo Survivable Branch Appliance al termine di questa procedura guidata** e quindi fare clic su **Fine** .

8.  Ripetere i passaggi precedenti per ogni sito di succursale che si desidera aggiungere alla topologia.

**Passaggio successivo:**

Per Survivable Branch Appliance o Survivable Branch Server: [Definire un Survivable Branch Appliance o un Survivable Branch Server in Lync Server 2013](lync-server-2013-define-a-survivable-branch-appliance-or-server.md)

Per connettività PSTN non resiliente: [Definire un gateway PSTN per un sito di succursale in Lync Server 2013](lync-server-2013-define-a-pstn-gateway-for-a-branch-site.md), [Configurare un trunk con bypass multimediale in Lync Server 2013](lync-server-2013-configure-a-trunk-with-media-bypass.md) o [Configurare un trunk senza bypass multimediale in Lync Server 2013](lync-server-2013-configure-a-trunk-without-media-bypass.md)

