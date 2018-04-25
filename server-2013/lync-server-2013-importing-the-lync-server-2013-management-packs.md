---
title: Importazione dei Management Pack di Lync Server 2013
TOCTitle: Importazione dei Management Pack di Lync Server 2013
ms:assetid: 846287e1-660f-453f-bdba-b2137b5f0ea1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205052(v=OCS.15)
ms:contentKeyID: 49301190
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Importazione dei Management Pack di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-22_

È possibile estendere le funzionalità di System Center Operations Manager installando pacchetti di gestione, ovvero software che stabilisce quali elementi System Center Operations Manager è in grado di monitorare, in che modo questi devono essere monitorati, e in che modo gli avvisi devono essere attivati e segnalati. Lync Server 2013 include due pacchetti di gestione di System Center Operations Manager che offrono le seguenti funzionalità:

  - Il pacchetto di gestione Component and User (Microsoft.LS.2013.Monitoring.ComponentAndUser.mp) traccia i problemi di Lync Server contenuti nei registri evento, memorizzati dai contatori delle prestazioni o presenti nei database CDR o QoE. Per quanto riguarda i problemi di importanza critica, è possibile configurare System Center Operations Manager affinché notifichi gli amministratori tramite e-mail, messaggistica istantanea o messaggi di testo SMS, la tecnologia utilizzata per l'invio di messaggi di testo da un dispositivo mobile a un altro.
    

    > [!NOTE]
    > Per informazioni dettagliate sulla configurazione delle notifiche di Operations Manager, vedere Configurazione delle notifiche in TechNet Library all'indirizzo <A class=uri href="http://go.microsoft.com/fwlink/?linkid=268785%26clcid=0x410">http://go.microsoft.com/fwlink/?linkid=268785&amp;clcid=0x410</A>.



  - Il pacchetto di gestione Active Monitoring (Microsoft.LS.2013.Monitoring.ActiveMonitoring.mp) testa in modo proattivo componenti chiave di Lync Server quali l'accesso al sistema, lo scambio di messaggi istantanei o l'effettuazione di chiamate a un telefono situato sulla rete PSTN (Public Switched Telephone Network). Questi test sono eseguiti attraverso i cmdlet di transazione sintetica Lync Server. Ad esempio, è possibile utilizzare il cmdlet **Test-CsIM** per simulare una conversazione di messaggistica istantanea tra due utenti. Se la simulazione non ha esito positivo, viene generata un'allerta.

È necessario importare i pacchetti di gestione. In caso contrario, non è possibile utilizzare Operations Manager per monitorare gli eventi di Lync Server o eseguire transazioni sintetiche di Lync Server.

Il pacchetto di gestione Component and User viene utilizzato unicamente per monitorare Lync Server 2013. In uno scenario di coesistenza, in cui sono installati Lync Server 2013 e Lync Server 2010, è necessario continuare a utilizzare i pacchetti di gestione di Lync Server 2010 per i computer con Lync Server 2010.


> [!NOTE]
> Tra i pacchetti di gestione di Lync Server 2010 vi sono Lync Server 2010 Monitoring Management Pack e Lync Server 2010 Group Chat Monitoring Management Pack.



È possibile utilizzare uno degli strumenti per importare i pacchetti di gestione:

  - **System Center Operations Manager**   Con questo metodo, si utilizza Operations Manager per aggiungere il monitoraggio per Lync Server.

  - **Operations Manager Shell**   È possibile utilizzare Operations Manager Shell per l'importazione diretta, o per risolvere eventuali problemi che si verificano durante l'importazione dei pacchetti di gestione attraverso la console System Center Operations Manager.

## Importazione dei pacchetti di gestione attraverso System Center Operations Manager

1.  Scaricare i file Microsoft.LS.2013.Monitoring.ActiveMonitoring.mp e Microsoft.LS.2013.Monitoring.ComponentAndUser.mp.

2.  In System Center Operations Manager, fare clic su **Amministrazione**.

3.  Nel riquadro **Amministrazione**, fare clic con il tasto destro del mouse su **Management Pack**, e quindi su **Importa Management Pack**.

4.  Nella finestra di dialogo **Seleziona Management Pack**, fare clic su **Aggiungi** e quindi su **Aggiungi da disco**.

5.  Nella finestra di dialogo **Catalogo in linea**, fare clic su **Annulla** per evitare che Operations Manager acceda in linea per verificare eventuali dipendenze dei pacchetti di gestione di Lync Server. Se si utilizza System Center Operations Manager 2012, fare clic su **No**.

6.  Nella finestra di dialogo **Selezionare i Management Pack da importare**, localizzare e selezionare i file **Microsoft.LS.2013.Monitoring.ActiveMonitoring.mp** e **Microsoft.LS.2013.Monitoring.ComponentAndUser.mp**, quindi fare clic su **Apri**. Per selezionare più file nella finestra di dialogo, fare clic sul primo file, tenere premuto il tasto Ctrl e quindi fare clic sul secondo file.

7.  Nella finestra di dialogo **Seleziona Management Pack**, fare clic su **Installa**. Se compare un messaggio di errore e l'installazione ha esito negativo, molto probabilmente i file dei pacchetti di gestione si trovano in una cartella protetta da Controllo account utente di Windows. In casi simili, copiare i file in una cartella diversa, quindi riavviare il processo di importazione e installazione.

8.  Nella finestra di dialogo **Seleziona Management Pack**, fare clic su **Chiudi**. Il processo di importazione e installazione potrebbe richiedere diversi minuti per essere completato.

## Importazione dei pacchetti di gestione attraverso Operations Manager Shell

In generale, è più semplice importare i pacchetti di gestione attraverso Operations Manager. Tuttavia, se si verifica un errore e l'importazione ha esito negativo, la console non sempre fornisce rapporti degli errori adeguati. In confronto, Operations Manager Shell fornisce informazioni dettagliate. Se si utilizza Operations Manager e si verificano problemi nell'importazione di un pacchetto di gestione, è possibile importarlo attraverso Operations Manager Shell. Operations Manager Shell fornisce ulteriori informazioni che aiutano a capire i motivi per i quali l'importazione ha avuto esito negativo.

Se si utilizza System Center Operations Manager 2007 R2, completare la procedura seguente:

1.  Fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, fare clic su **System Center Operations Manager 2007 R2**, e quindi su **Operations Manager Shell**.

2.  In Operations Manager Shell, digitare il comando seguente nel prompt dei comandi, utilizzando il percorso effettivo alla copia del file Microsoft.LS.2013.Monitoring.ActiveMonitoring.mp, quindi premere Invio:
    
        MPImport.exe D:\MP\Microsoft.LS.2013.Monitoring.ActiveMonitoring.mp

3.  Dopo avere importato il primo pacchetto di gestione, ripetere il processo utilizzando il percorso della copia del file Microsoft.LS.2013.Monitoring.ComponentAndUser.mp:
    
        MPImport.exe D:\MP\Microsoft.LS.2013.Monitoring.ComponentAndUser.mp

4.  Chiudere Operations Manager Shell.

Se si utilizza System Center Operations Manager 2012, completare la procedura seguente:

1.  Fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, fare clic su **Microsoft System Center 2012**, quindi fare clic su **Operations Manager** e su **Operations Manager Shell**.

2.  In Operations Manager Shell, digitare il comando seguente nel prompt dei comandi, utilizzando il percorso effettivo alla copia del file Microsoft.LS.2013.Monitoring.ActiveMonitoring.mp, quindi premere Invio:
    
        Import-SCOMManagementPack -FullName "D:\MP\ Microsoft.LS.2013.Monitoring.ActiveMonitoring.mp"

3.  Dopo avere importato il primo pacchetto di gestione, ripetere il processo utilizzando il percorso della copia del file Microsoft.LS.2013.Monitoring.ComponentAndUser.mp:
    
        Import-SCOMManagementPack -FullName "D:\MP\ Microsoft.LS.2013.Monitoring.ComponentAndUser.mp"

