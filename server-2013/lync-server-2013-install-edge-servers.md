---
title: 'Lync Server 2013: Installare server perimetrali'
TOCTitle: Installare server perimetrali
ms:assetid: 1655ab69-3899-4ee4-a1cc-8243bc1bfa0f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398230(v=OCS.15)
ms:contentKeyID: 49299794
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Installare server perimetrali per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-08_

È possibile installare Lync Server 2013 in server perimetrali utilizzando Distribuzione guidata di Lync Server. Eseguendo la distribuzione guidata in ogni server perimetrale, è possibile effettuare la maggior parte delle attività necessarie per installare il server perimetrale. Per poter distribuire Lync Server 2013 in un server perimetrale, è necessario avere già eseguito Generatore di topologie per definire e pubblicare la topologia del server perimetrale e aver effettuato l'esportazione su un supporto accessibile dal server perimetrale. Per informazioni dettagliate, vedere [Scenari per l'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-scenarios-for-external-user-access.md) e [Esportare la topologia di Lync Server 2013 e copiarla su supporto esterno per l'installazione perimetrale](lync-server-2013-export-your-topology-and-copy-it-to-external-media-for-edge-installation.md).

Dopo aver utilizzato la Distribuzione guidata per installare ogni server perimetrale, installare e assegnare i certificati necessari e avviare i servizi necessari, è possibile completare l'installazione seguendo le istruzioni contenute in [Configurazione del supporto per l'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-configuring-support-for-external-user-access.md) per abilitare e configurare l'accesso utente esterno, nonché le istruzioni contenute in [Verifica della distribuzione dei componenti perimetrali in Lync Server 2013](lync-server-2013-verifying-your-edge-deployment.md) per convalidare l'installazione, inclusa la connettività di server e client.

## Per installare un server perimetrale

1.  Eseguire l'accesso al computer in cui si desidera installare il server perimetrale come membri del gruppo Administrators locale o utilizzando un account con autorizzazioni e diritti utente equivalenti.

2.  Assicurarsi che il file di configurazione della topologia creato utilizzando Generatore di topologie, e quindi esportato e copiato su un supporto esterno, sia disponibile nel server perimetrale. Accedere ad esempio all'unità USB in cui è stato copiato il file di configurazione della topologia oppure verificare l'accesso alla condivisione di rete in cui è stato copiato il file.

3.  Avviare la Distribuzione guidata.
    

    > [!NOTE]
    > Se viene visualizzato un messaggio che indica la necessità di installare Microsoft Visual C++ Redistributable, fare clic su <STRONG>Sì</STRONG> . Nella finestra di dialogo successiva è possibile accettare il &nbsp; percorso di installazione predefinito oppure fare clic su <STRONG>Sfoglia</STRONG> per selezionare un percorso diverso e quindi fare clic su <STRONG>Installa</STRONG> . Nella finestra di dialogo successiva selezionare la casella di controllo <STRONG>Accetto i termini del Contratto di licenza</STRONG> e quindi fare clic su <STRONG>OK</STRONG> .



4.  Nella Distribuzione guidata fare clic su **Installa o aggiorna il sistema Lync Server** .

5.  Dopo che viene determinato lo stato della distribuzione, per **Passaggio 1: Installazione dell'archivio di configurazione locale** fare clic su **Esegui** e quindi eseguire le operazioni seguenti:
    
      - Nella finestra di dialogo **Configura la replica locale dell'archivio di gestione centrale** fare clic su **Importa da un file (opzione consigliata per Edge Server)** , passare al percorso del file di configurazione della topologia esportato, selezionare il file con estensione zip, fare clic su **Apri** e quindi su **Avanti** .
    
      - Le informazioni di configurazione presenti nel file verranno lette e scritte nel file di configurazione XML nel computer locale.
    
      - Al termine del processo **Esecuzione comandi in corso** , fare clic su **Fine** .

6.  Nella Distribuzione guidata fare clic su **Passaggio 2: Installazione o rimozione componenti di Lync Server** per installare i componenti perimetrali di Lync Server 2013 specificati nel file di configurazione XML archiviato nel computer locale.

7.  Al termine dell'installazione, utilizzare le istruzioni contenute in [Configurare i certificati perimetrali per Lync Server 2013](lync-server-2013-set-up-edge-certificates.md) per installare e assegnare i certificati necessari prima di avviare i servizi.

