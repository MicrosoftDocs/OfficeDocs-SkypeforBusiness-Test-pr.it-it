---
title: Verificare il completamento della replica utente
TOCTitle: Verificare il completamento della replica utente
ms:assetid: 119e9896-45e5-4f8b-af43-7b09360ada0b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204680(v=OCS.15)
ms:contentKeyID: 49299730
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verificare il completamento della replica utente

 

_**Ultima modifica dell'argomento:** 2012-09-17_

Quando si esegue il cmdlet **Move-CsUser** è possibile che si verifichi un errore di mancata sincronizzazione delle informazioni utente tra Servizi di dominio Active Directory e i database di Lync Server 2013 poiché la replica iniziale non è completa. Il tempo impiegato per il completamento della sincronizzazione iniziale del servizio User Replicator di Lync Server 2013 dipende dal numero di controller di dominio ospitati nella foresta di Active Directory che ospita il pool di Lync Server 2013. Il processo di sincronizzazione iniziale del servizio User Replicator di Lync Server 2013 si verifica quando il Front End Server Lync Server 2013 viene avviato per la prima volta. Successivamente la sincronizzazione viene basata sull'intervallo di User Replicator. Eseguire la procedura seguente per verificare che la replica degli utenti sia completata prima di eseguire il cmdlet **Move-CsUser** .

## Per verificare che la replica degli utenti sia stata completata

1.  Accedere al computer in cui è installato Generatore di topologie come membro del gruppo Domain Admins e del gruppo RTCUniversalServerAdmins.

2.  Fare clic su **Start** e scegliere **Esegui** .

3.  Digitare **eventvwr.exe** , quindi fare clic su **OK** .

4.  Nel Visualizzatore eventi fare clic su **Registri applicazioni e servizi** per espanderlo, quindi selezionare Lync Server

5.  Nel riquadro **Azioni** fare clic su **Filtro registro corrente** .

6.  Nell'elenco **Origini eventi** fare clic su **LS User Replicator** .

7.  In **\<Tutti gli ID evento\>** digitare **30024** e quindi fare clic su **OK** .

8.  Nell'elenco degli eventi filtrati cercare nella scheda **Generale** una voce che indica che la replica degli utenti è stata completata correttamente.

