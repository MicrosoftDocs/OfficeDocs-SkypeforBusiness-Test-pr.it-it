---
title: Verificare il completamento della replica utente
TOCTitle: Verificare il completamento della replica utente
ms:assetid: 199dc9de-b555-468f-a42a-9e92ea6c9053
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204712(v=OCS.15)
ms:contentKeyID: 49299829
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verificare il completamento della replica utente

 

_**Ultima modifica dell'argomento:** 2012-09-28_

Durante l'esecuzione del cmdlet **Move-CsLegacyUser** , è possibile che la replica iniziale delle informazioni utente tra Servizi di dominio Active Directory e i database di Lync Server 2013 non sia sincronizzata e che si verifichi pertanto un errore. Il tempo impiegato per il completamento della sincronizzazione iniziale del servizio User Replicator di Lync Server 2013 dipende dal numero di controller di dominio ospitati nella foresta di Active Directory che ospita il pool Lync Server 2013. Il processo di sincronizzazione iniziale del servizio User Replicator di Lync Server 2013 si verifica quando Lync Server 2013 Front End Server viene avviato per la prima volta. Successivamente la sincronizzazione viene basata sull'intervallo di User Replicator. Eseguire la procedura seguente per verificare che la replica degli utenti sia completata prima di eseguire il cmdlet **Move-CsLegacyUser** .

## Per verificare che la replica degli utenti sia stata completata

1.  In Lync Server 2013 Front End Server fare clic sul menu **Start** e scegliere **Esegui** .

2.  Digitare **eventvwr.exe** , quindi fare clic su **OK** .

3.  Nel Visualizzatore eventi fare clic su **Registri applicazioni e servizi** per espanderlo e quindi selezionare Lync Server.

4.  Nel riquadro **Azioni** fare clic su **Filtro registro corrente** .

5.  Nell'elenco **Origini eventi** fare clic su **LS User Replicator** .

6.  In **\<Tutti gli ID evento\>** digitare **30024** e quindi fare clic su **OK** .

7.  Nell'elenco degli eventi filtrati cercare nella scheda **Generale** una voce che indica che la replica degli utenti è stata completata correttamente.

