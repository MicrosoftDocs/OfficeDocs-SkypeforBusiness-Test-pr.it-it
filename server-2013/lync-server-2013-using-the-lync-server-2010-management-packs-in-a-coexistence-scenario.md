---
title: "Lync Server 2013: Usa Management Pack di LS 2010 in scenario di coesistenza"
TOCTitle: "Lync Server 2013: Usa Management Pack di LS 2010 in scenario di coesistenza"
ms:assetid: 8b792503-bd88-47fe-9d97-b071e8d429a5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205078(v=OCS.15)
ms:contentKeyID: 49301261
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Utilizzo dei Management Pack di Lync Server 2010 in uno scenario di coesistenza

 

_**Ultima modifica dell'argomento:** 2012-10-22_

Molti clienti adottano un programma di implementazione all'interno delle organizzazioni che prevede la migrazione progressiva degli utenti da Microsoft Lync Server 2010 a Lync Server 2013. Gli amministratori di queste società si occupano di monitorare entrambe le versioni di Lync Server per accertarsi che tutti gli utenti finali usufruiscano della migliore esperienza di comunicazione possibile. Per questo scenario, Lync Server 2013 Management Pack supporta un percorso di migrazione affiancata con Lync Server 2010 Management Pack.

In Lync Server 2010, i computer Lync Server vengono individuati tramite il documento di topologia memorizzato con l'archivio di gestione centrale. In questa configurazione, un singolo computer segnala l'esistenza di tutti gli altri computer Lync Server.

I Management Pack per Lync Server 2013 usano ora l'individuazione a livello di computer invece del meccanismo di individuazione centrale adottato in Lync Server 2010. Ciò significa che ogni agente System Center individua se stesso e segnala la sua esistenza a System Center Operations Manager. L'uso dell'individuazione a livello di computer semplifica l'amministrazione dell'infrastruttura di System Center e agevola la coesistenza di diverse versioni dei Management Pack di Lync Server (ad esempio quelli per Lync Server 2010 e per Lync Server 2013).

Per supportare questa migrazione, sarà innanzitutto necessario aggiornare il monitoraggio esistente di Lync Server 2010 per evitare lacune nella copertura. A tale scopo, selezionare un computer Lync Server 2010 esistente per servire lo script di individuazione centrale per Lync Server 2010 prima di aggiornare l'archivio di gestione centrale a Lync Server 2013. Questo processo si articola in quattro passaggi:

1.  Aggiornare Lync Server 2010 Management Pack con l'aggiornamento cumulativo 7.

2.  Impostare un computer Lync Server 2010 per l'esecuzione dello script di individuazione centrale.

3.  Eseguire l'override del candidato di individuazione centrale in Microsoft Lync Server 2010 Management Pack.

4.  Verificare che il nuovo candidato di individuazione centrale sia stato individuato.

## Impostazione di un computer Lync Server 2010 per l'esecuzione dello script di individuazione centrale

Per designare un computer non dell'archivio di gestione centrale (ad esempio un server Front End Lync Server) per la gestione dell'individuazione centrale, è necessario creare la chiave del Registro di sistema seguente nel server in questione:

HKLM\\Software\\Microsoft\\Real-Time Communications\\Health\\CentralDiscoveryCandidate

È possibile creare questa chiave del Registro di sistema completando la procedura seguente:

1.  Fare clic sul pulsante **Start**, quindi scegliere **Esegui**.

2.  Nella finestra di dialogo **Esegui** digitare **regedit** e quindi premere INVIO.

3.  Nell'editor del Registro di sistema espandere **HKEY\_LOCAL\_MACHINE**, **SOFTWARE**, **Microsoft** e quindi **Real-Time Communications**.

4.  Fare clic con il pulsante destro del mouse su **Health**, scegliere **Nuovo** e quindi **Chiave**. Se la chiave **Health** non esiste, fare clic con il pulsante destro del mouse su **Real-Time Communications**, scegliere **Nuovo** e quindi **Chiave**. Dopo aver creato la nuova chiave, digitare Health e premere INVIO.
    
    Dopo aver creato la nuova chiave, digitare **CentralDiscoveryCandidate** e quindi premere INVIO per rinominarla.

L'acquisizione di questa modifica da parte del computer può richiedere diverse ore. Per fare in modo che la modifica venga applicata immediatamente, arrestare e quindi riavviare il servizio Agente integrità. Per riavviare il servizio Agente integrità, completare la procedura seguente nel computer Lync Server 2010:

1.  Fare clic su **Start**, scegliere **Tutti i programmi** e **Accessori**, fare clic con il pulsante destro del mouse su **Prompt dei comandi** e quindi scegliere **Esegui come amministratore**.

2.  Nella finestra della console digitare il comando seguente e premere INVIO:
    
        Net stop HealthService

3.  Verrà visualizzato un messaggio indicante che il servizio System Center Management è in fase di arresto, seguito da un secondo messaggio di conferma dell'avvenuto arresto. Dopo che il servizio è stato arrestato, è possibile riavviarlo digitando il comando seguente e premendo INVIO:
    
        Net start HealthService

## Sostituzione del candidato di individuazione centrale in Lync Server 2010 Management Pack

Dopo aver impostato un computer Lync Server 2010 per segnalare computer Lync Server 2010, è necessario indicare tale modifica anche a Lync Server 2010 Management Pack. A tale scopo, sarà necessario creare una sostituzione in Management Pack. A tale scopo, effettuare la procedura seguente:

1.  Nella console di Operations Manager fare clic su **Creazione e modifica**.

2.  Nella scheda Creazione e modifica espandere **Oggetti Management Pack**, fare clic su **Individuazioni oggetti** e quindi fare clic su **Ambito**.

3.  Nella finestra di dialogo **Crea ambito oggetti Management Pack in base a destinazioni** selezionare l'elemento con destinazione il **candidato di individuazione LS** e fare clic su **OK**. Tenere presente che il candidato individuazione LS viene visualizzato solo se è installato Lync Server 2010 Management Pack.

4.  Nella console di Operations Manager fare clic con il pulsante destro del mouse sul **candidato individuazione LS**, scegliere **Sostituzione**, **Sostituzione individuazione oggetto** e fare clic su **Per tutti gli oggetti della classe: candidato individuazione LS**.

5.  Nella finestra di dialogo **Proprietà di sostituzione** selezionare la casella di controllo **Sostituzione** accanto al parametro **FQDN WatcherNode individuazione centrale**. Digitare il nome di dominio completo del computer Lync Server 2010 in **Valore sostituzione** e **Valore corrente**. Selezionare la casella di controllo **Imposto** e fare clic su **OK**.

Dopo aver creato la sostituzione, è necessario riavviare il servizio di integrità nel server di gestione radice. Per riavviare il servizio di integrità, completare la procedura seguente nel server di gestione radice:

1.  Fare clic su **Start**, scegliere **Tutti i programmi** e **Accessori**, fare clic con il pulsante destro del mouse su **Prompt dei comandi** e quindi scegliere **Esegui come amministratore**.

2.  Nella finestra della console digitare il comando seguente e premere INVIO:
    
        Net stop HealthService

3.  Verrà visualizzato un messaggio indicante che il servizio System Center Management è in fase di arresto, seguito da un secondo messaggio di conferma dell'avvenuto arresto. Dopo che il servizio è stato arrestato, è possibile riavviarlo digitando il comando seguente e premendo INVIO:
    
        Net start HealthService

## Verifica dell'individuazione del nuovo candidato di individuazione centrale

Il passaggio finale prima di aggiornare l'archivio di gestione centrale consiste nel verificare che il nuovo candidato di individuazione centrale sia stato individuato da Lync Server 2010 Management Pack. A tale scopo, aprire la console di Operations Manager e quindi fare clic su Monitoraggio. Nella scheda Monitoraggio espandere **Integrità Microsoft Lync Server 2010**, **Individuazione topologia** e quindi la **vista dello stato di individuazione**. Verificare che una riga nella vista presenti un **percorso** indicante il nome di dominio completo del candidato di individuazione centrale. È inoltre necessario verificare che lo stato del computer risulti **integro**.

