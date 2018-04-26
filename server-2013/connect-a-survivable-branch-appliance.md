---
title: Connettere un Survivable Branch Appliance
TOCTitle: Connettere un Survivable Branch Appliance
ms:assetid: fe3167e2-d1b1-4cd4-bf30-262e0e7d14e8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721948(v=OCS.15)
ms:contentKeyID: 49887841
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Connettere un Survivable Branch Appliance

 

_**Ultima modifica dell'argomento:** 2012-10-19_

Ogni Survivable Branch Appliance (SBA) è associato a un pool Front End che opera come Registrazione avanzata di backup per SBA. Quando viene eseguita la migrazione del pool Front End a Lync Server 2013, è necessario annullare la registrazione del Survivable Branch Appliance dal pool Front End di Lync Server 2010 durante l'aggiornamento del pool. Dopo che è stata completata la migrazione del pool a Lync Server 2013, è possibile associare di nuovo il Survivable Branch Appliance al pool Front End aggiornato. Questa operazione implica l'eliminazione del Survivable Branch Appliance dalla topologia legacy di Lync Server 2010 nel Generatore di topologie e l'aggiunta del Survivable Branch Appliance alla topologia di Lync Server 2013. È necessario spostare gli utenti ospitati nel Survivable Branch Appliance legacy di Lync Server 2010 in un altro pool Front End prima di rimuovere il Survivable Branch Appliance dalla topologia. Dopo che il Survivable Branch Appliance è stato aggiunto alla topologia di Lync Server 2013, gli utenti potranno essere spostati di nuovo nel Survivable Branch Appliance. Queste procedure sono riepilogate di seguito:

1.  Spostare gli utenti dei siti di succursale ospitati nel Survivable Branch Appliance legacy di Lync Server 2010 in un altro pool Front End.

2.  Rimuovere il Survivable Branch Appliance dalla topologia legacy di Lync Server 2010 per disconnettere il pool Front End esistente come pool di registrazione di backup.

3.  Aggiungere il Survivable Branch Appliance alla topologia di Lync Server 2013 e configurare il nuovo pool Front End come pool di registrazione di backup.

4.  Spostare gli utenti dei siti di succursale nel nuovo Survivable Branch Appliance di Lync Server 2013.

**Aggiungere il sito di succursale del Survivable Branch Appliance di Lync Server 2010 alla topologia**

1.  Aprire **Generatore di topologie**.

2.  Nel riquadro sinistro fare clic con il pulsante destro del mouse su **Siti di succursale** e quindi fare clic su **Nuovo sito di succursale**.

3.  Nella finestra di dialogo **Definisci nuovo sito di succursale** fare clic su **Nome** e quindi digitare il nome del sito di succursale.

4.  (Facoltativo) Fare clic su **Descrizione** e quindi digitare una descrizione significativa del sito di succursale.

5.  Fare clic su **Avanti**.

6.  (Facoltativo) Nella successiva finestra di dialogo **Definisci nuovo sito di succursale** eseguire una delle operazioni seguenti:
    
    1.  Fare clic su **Città** e quindi digitare il nome della città in cui si trova il sito di succursale.
    
    2.  Fare clic su **Paese** e quindi digitare il nome del paese in cui si trova il sito di succursale.
    
    3.  Fare clic su **Codice paese** e quindi digitare il codice di chiamata in due cifre per il paese/area geografica in cui si trova il sito di succursale.

7.  Fare clic su **Avanti** e quindi eseguire una delle operazioni seguenti:
    
    1.  Se nel sito si utilizza un Survivable Branch Appliance o un Survivable Branch Server di Lync 2010, deselezionare l'opzione **Aprire la procedura guidata Nuovo Survivable Branch Appliance al termine di questa procedura guidata** e quindi fare clic su **Fine**.

8.  Per associare il Survivable Branch Appliance legacy di Lync Server 2010 al pool Front End di Lync Server 2013:
    
    1.  Espandere il sito di succursale che è stato creato.
    
    2.  Fare clic con il pulsante destro del mouse su **Lync Server 2010** e quindi scegliere **Nuovo**.
    
    3.  Fare clic su **Survivable Branch Appliance…**

9.  Seguire le istruzioni nella procedura guidata visualizzata. Per ulteriori informazioni sui passaggi della procedura guidata, vedere [Definire un Survivable Branch Appliance o un Survivable Branch Server in Lync Server 2013](lync-server-2013-define-a-survivable-branch-appliance-or-server.md).
    

    > [!NOTE]
    > Un Survivable Branch Appliance di Lync Server 2010 può essere associato solo a un archivio di monitoraggio di Lync Server 2010.



10. Se nel sito non si utilizza un Survivable Branch Appliance o un Survivable Branch Server, deselezionare la casella di controllo **Aprire la procedura guidata Nuovo Survivable Branch Appliance al termine di questa procedura guidata** e quindi fare clic su **Fine**.

11. Ripetere i passaggi precedenti per ogni sito di succursale che si desidera aggiungere alla topologia.

