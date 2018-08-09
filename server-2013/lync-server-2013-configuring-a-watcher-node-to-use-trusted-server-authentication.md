---
title: "Lync Server 2013: Configura nodo Watcher per uso autenticaz. server trusted"
TOCTitle: "Lync Server 2013: Configura nodo Watcher per uso autenticaz. server trusted"
ms:assetid: 42d879ac-aa90-4ed6-b5e2-1e208711672a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204852(v=OCS.15)
ms:contentKeyID: 49300347
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione di un nodo Watcher per l'utilizzo dell'autenticazione dei server trusted

 

_**Ultima modifica dell'argomento:** 2012-10-22_

Se il computer del nodo Watcher si trova all'interno della rete perimetrale, l'uso dell'autenticazione Server attendibile può ridurre notevolmente le attività di amministrazione richieste dal momento che implica il mantenimento di un singolo certificato anziché di numerose password per i vari account utente.

Il primo passaggio per la configurazione dell'autenticazione Server attendibile consiste nel creare un pool di applicazioni attendibili in cui ospitare il computer del nodo Watcher. Dopo aver creato il pool, è necessario configurare l'esecuzione delle transazioni sintetiche sul nodo Watcher come applicazione attendibile.


> [!NOTE]
> Per applicazione attendibile si intende un'applicazione cui viene assegnato lo stato attendibile in modo che venga eseguita come parte di Lync Server 2013, ma non si intende una parte predefinita del prodotto. Lo stato attendibile indica che all'applicazione non verrà richiesta l'autenticazione a ogni esecuzione.



Per creare un pool di applicazioni attendibili, aprire Lync Server 2013 Management Shell ed eseguire un comando simile al seguente:

    New-CsTrustedApplicationPool -Identity atl-watcher-001.litwareinc.com -Registrar atl-cs-001.litwareinc.com -ThrottleAsServer $True -TreatAsAuthenticated $True -OutboundOnly $False -RequiresReplication $True -ComputerFqdn atl-watcher-001.litwareinc.com -Site Redmond


> [!NOTE]
> Per informazioni dettagliate sui parametri utilizzati nel comando precedente, digitare il comando seguente al prompt di Lync Server Management Shell:<BR>Get-Help New-CsTrustedApplicationPool -Full | more



Dopo aver creato il pool di applicazioni attendibili, configurare il computer del nodo Watcher per l'esecuzione delle transazioni sintetiche come applicazione attendibile. A tale scopo, utilizzare il cmdlet **New-CsTrustedApplication** e un comando simile al seguente:

    New-CsTrustedApplication -ApplicationId STWatcherNode -TrustedApplicationPoolFqdn atl-watcher-001.litwareinc.com -Port 5061

Al termine del comando precedente e della creazione dell'applicazione attendibile, eseguire Enable-CsTopology per in modo che le modifiche diventino effettive:

    Enable-CsTopology

Dopo aver eseguito Enable-CsTopology, si consiglia di riavviare il computer.

Per verificare che la nuova applicazione attendibile sia stata creata, digitare il comando seguente al prompt di Lync Server Management Shell:

    Get-CsTrustedApplication -Identity "atl-watcher-001.litwareinc.com/urn:application:STWatcherNode"

## Configurazione di un certificato predefinito sul nodo Watcher

A ogni nodo Watcher deve essere assegnato un certificato predefinito utilizzando la Distribuzione guidata di Lync Server.

**Per assegnare un certificato predefinito**

1.  Fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Lync Server** e quindi **Distribuzione guidata di Lync Server**.

2.  Nella Distribuzione guidata di Lync Server fare clic su **Installa o aggiorna il sistema Lync Server** e quindi su **Esegui** al di sotto dell'intestazione **Richiesta, installazione o assegnazione dei certificati**.
    

    > [!NOTE]
    > Se il pulsante <STRONG>Esegui</STRONG> è disabilitato, può essere necessario prima fare clic su <STRONG>Esegui</STRONG> al di sotto di <STRONG>Installazione dell'archivio di configurazione locale</STRONG>.



3.  Eseguire una delle operazioni seguenti:
    
      - Se è già disponibile un certificato da poter utilizzare come predefinito, fare clic su **Predefinito** nella Configurazione guidata certificati e quindi fare clic su **Assegna**. Seguire i passaggi indicati nella procedura guidata Assegnazione certificato per assegnarlo.
    
      - Se è necessario richiedere un certificato da utilizzare come predefinito, fare clic su **Richiesta** e quindi seguire i passaggi indicati dalla procedura guidata Richiesta di certificato. Se si utilizzano i valori predefiniti per il certificato del server Web, si ottiene un certificato che può essere assegnato come predefinito.

## Installazione e configurazione di un nodo Watcher

Dopo aver riavviato il computer del nodo Watcher e aver configurato un certificato, è necessario eseguire il file Watchernode.msi. L'esecuzione deve essere effettuata in un computer in cui siano installati sia i file dell'agente Operations Manager che i componenti principali di Lync Server 2013.

**Per installare e configurare un nodo Watcher**

1.  Aprire Lync Server Management Shell facendo clic sul pulsante **Start**, scegliendo **Tutti i programmi**, **Lync Server** e quindi **Lync Server Management Shell**.

2.  In Lync Server Management Shell digitare il comando seguente e premere INVIO (specificare il percorso effettivo della copia di Watchernode.msi):
    
        C:\Tools\Watchernode.msi Authentication=TrustedServer
    

    > [!NOTE]
    > È anche possibile eseguire Watchernode.msi da una finestra di comando. Per aprire una finestra di comando, fare clic sul pulsante <STRONG>Start</STRONG>, fare clic con il pulsante destro del mouse su <STRONG>Prompt dei comandi</STRONG> e quindi scegliere <STRONG>Esegui come amministratore</STRONG>. Quando viene visualizzata la finestra di comando, digitare lo stesso comando precedente.



Si noti che la coppia nome/valore del comando precedente Authentication=TrustedServer presenta la distinzione tra maiuscole e minuscole. Digitarla esattamente come mostrato. Il comando seguente non riesce in quanto non utilizza la corretta distinzione tra maiuscole e minuscole per le lettere:

C:\\Tools\\Watchernode.msi authentication=trustedserver

È possibile utilizzare la modalità TrustedServer solo con i computer situati all'interno della rete perimetrale. Quando un nodo viene eseguito in modalità TrustedServer, gli amministratori non devono mantenere le password di prova degli utenti sul computer.

