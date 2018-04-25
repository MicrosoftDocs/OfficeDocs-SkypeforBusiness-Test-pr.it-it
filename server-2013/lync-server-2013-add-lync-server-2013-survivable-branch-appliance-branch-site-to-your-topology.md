---
title: 'Lync Server 2013: Aggiungere un sito di succursale Survivable Branch Appliance di Lync Server 2013 alla topologia'
TOCTitle: Aggiungere un sito di succursale Survivable Branch Appliance di Lync Server 2013 alla topologia
ms:assetid: d3142a37-4606-456d-8ea9-6cc0e51e55f3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721896(v=OCS.15)
ms:contentKeyID: 49887770
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Aggiungere un sito di succursale Survivable Branch Appliance di Lync Server 2013 alla topologia

 

_**Ultima modifica dell'argomento:** 2012-10-07_

Non è possibile associare Survivable Branch Appliance (SBA) di Microsoft Lync Server 2013 a un pool Front End di Microsoft Lync Server 2010 come funzione di registrazione di backup. L'SBA deve essere associato a un pool Front End di Microsoft Lync Server 2013. In questi passaggi si presuppone che venga utilizzato un SBA di Microsoft Lync Server 2013. Eseguire questa procedura nel sito centrale.

## Per aggiungere siti di succursale con SBA di Microsoft Lync Server 2013 alla topologia

1.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.

2.  Nell'albero della console espandere il sito centrale, espandere **Siti di succursale** e quindi fare clic su **Nuovo sito di succursale** .

3.  Nella finestra di dialogo **Definisci nuovo sito di succursale** fare clic su **Nome** e quindi digitare un nome per il nuovo sito di succursale.

4.  (Facoltativo) Fare clic su **Descrizione** e quindi digitare una descrizione significativa del sito di succursale.

5.  Fare clic su **Avanti** .

6.  (Facoltativo) Nella successiva finestra di dialogo **Definisci nuovo sito di succursale** eseguire una delle operazioni seguenti:
    
      - Fare clic su **Città** e quindi digitare il nome della città in cui si trova il sito di succursale.
    
      - Fare clic su **Paese** e quindi digitare il nome del paese in cui si trova il sito di succursale.
    
      - Fare clic su **Codice paese** e quindi digitare il codice di chiamata in due cifre per il paese/area geografica in cui si trova il sito di succursale.

7.  Fare clic su **Avanti** e quindi eseguire una delle operazioni seguenti:
    
      - Se si utilizza un Survivable Branch Appliance o un Survivable Branch Server in questo sito, verificare che la casella di controllo **Aprire la procedura guidata Nuovo Survivable Branch Appliance al termine di questa procedura guidata** sia selezionata.
    
      - Se non si utilizza un Survivable Branch Appliance o un Survivable Branch Server in questo sito, deselezionare la casella di controllo **Aprire la procedura guidata Nuovo Survivable Branch Appliance al termine di questa procedura guidata** .
    
      - Fare clic su **Fine** e quindi seguire le indicazioni fornite nella procedura guidata che verrà visualizzata. Per informazioni sulle opzioni della procedura guidata, vedere [Definire un Survivable Branch Appliance o un Survivable Branch Server in Lync Server 2013](lync-server-2013-define-a-survivable-branch-appliance-or-server.md).

8.  Ripetere i passaggi precedenti per ogni sito di succursale che si desidera aggiungere alla topologia.

## Vedere anche

#### Attività

[Definire un Survivable Branch Appliance o un Survivable Branch Server in Lync Server 2013](lync-server-2013-define-a-survivable-branch-appliance-or-server.md)  
[Definire un gateway PSTN per un sito di succursale in Lync Server 2013](lync-server-2013-define-a-pstn-gateway-for-a-branch-site.md)  
[Configurare un trunk con bypass multimediale in Lync Server 2013](lync-server-2013-configure-a-trunk-with-media-bypass.md)  
[Configurare un trunk senza bypass multimediale in Lync Server 2013](lync-server-2013-configure-a-trunk-without-media-bypass.md)

