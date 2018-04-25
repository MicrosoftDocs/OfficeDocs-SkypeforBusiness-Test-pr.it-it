---
title: 'Lync Server 2013: Configurazione dei criteri di Qualità del servizio (QoS) per server per conferenze, server applicazioni e Mediation Server'
TOCTitle: Configurazione dei criteri di Qualità del servizio (QoS) per server per conferenze, server applicazioni e Mediation Server
ms:assetid: 8adcbbc5-c9f5-476d-ab7f-72e61859cacf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205076(v=OCS.15)
ms:contentKeyID: 49301259
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione dei criteri di Qualità del servizio (QoS) in Lync Server 2013 per server per conferenze, server applicazioni e Mediation Server

 

_**Ultima modifica dell'argomento:** 2014-06-23_

La configurazione degli intervalli di porte agevola l'uso di QoS (Quality of Service) assicurando che tutto il traffico di un tipo specificato (ad esempio, tutto il traffico audio) passi attraverso lo stesso set di porte. Ciò semplifica l'identificazione e il contrassegno di un determinato pacchetto da parte del sistema: se la porta 49152 è riservata per il traffico audio, qualsiasi attraversamento di pacchetto tramite la porta 49152 può essere contrassegnato con un codice DSCP indicante che si tratta di pacchetti audio. A sua volta, ciò consente ai router di identificare il pacchetto come pacchetto audio e assegnargli una priorità più elevata rispetto ai pacchetti non contrassegnati (ad esempio i pacchetti usati per copiare un file da un server all'altro).

Tuttavia, limitando semplicemente un set di porte a un tipo di traffico specifico non si determina necessariamente l'assegnazione del codice DSCP appropriato ai pacchetti che le attraversano. Oltre a definire gli intervalli di porte è anche necessario creare criteri QoS (Quality of Service) che specificano il codice DSCP da associare a ogni intervallo di porte. Per Microsoft Lync Server 2013 ciò significa in genere creare due criteri: uno per l'audio e uno per i video.

La creazione e la gestione dei criteri QoS risulta particolarmente semplice mediante Criteri di gruppo. Questi stessi criteri possono anche essere creati mediante criteri di sicurezza locali, tuttavia ciò richiede la ripetizione della stessa procedura su ogni computer. Il set iniziale di criteri QoS (uno per l'audio e uno per il video) deve essere applicato solo ai computer Lync Server che eseguono il server per conferenze, il server applicazioni e/o i servizi del Mediation Server. Se tutti questi computer si trovano nella stessa unità organizzativa di Active Directory, è sufficiente assegnare il nuovo oggetto Criteri di gruppo all'unità in questione. In alternativa, è possibile eseguire altre operazioni per assegnare il nuovo criterio ai computer specificati; ad esempio è possibile inserire i computer appropriati in un gruppo di sicurezza e quindi usare i filtri di sicurezza di Criteri di gruppo per applicare l'oggetto Criteri di gruppo solo al gruppo in questione.

Per creare un criterio QoS (Quality of Service) per la gestione dell'audio, accedere a un computer in cui è installato Gestione Criteri di gruppo. Aprire Gestione Criteri di gruppo (fare clic sul pulsante **Start** , scegliere **Strumenti di amministrazione** e quindi fare clic su **Gestione Criteri di gruppo** ), quindi completare la procedura seguente:

1.  In Gestione Criteri di gruppo, individuare il contenitore in cui creare il nuovo criterio. Se ad esempio tutti i computer Lync Server si trovano in un'unità organizzativa denominata Lync Server, il nuovo criterio deve essere creato nell'unità organizzativa Lync Server.

2.  Fare clic con il pulsante destro del mouse sul contenitore appropriato e quindi scegliere **Crea un oggetto Criteri di gruppo in questo dominio e crea qui un collegamento** .

3.  Nella nuova finestra di dialogo **Nuovo oggetto Criteri di gruppo** digitare un nome per il nuovo oggetto Criteri di gruppo nella casella **Nome** (ad esempio, **Lync Server QoS** ) e quindi fare clic su **OK** .

4.  Fare clic con il pulsante destro del mouse sul criterio appena creato e quindi scegliere **Modifica** .

5.  Nell'Editor Gestione Criteri di gruppo espandere **Configurazione computer** , espandere **Criteri** , espandere **Impostazioni di Windows** , fare clic con il pulsante destro del mouse su **QoS basata su criteri** e quindi scegliere **Crea nuovo criterio** .

6.  Nella finestra di dialogo **QoS basata su criteri** , nella pagina di apertura, digitare un nome per il nuovo criterio (ad esempio, **Lync Server QoS** ) nella casella **Nome** . Selezionare **Specifica valore DSCP** e impostare il valore su **46** . Lasciare non selezionata l'opzione **Specifica velocità in uscita** , quindi fare clic su **Avanti** .

7.  Nella pagina successiva, accertarsi che l'opzione **Tutte le applicazioni** sia selezionata e quindi fare clic su **Avanti** . In questo modo ci si assicura che tutte le applicazioni abbineranno i pacchetti dell'intervallo di porte specificato al codice DSCP specificato.

8.  Nella terza pagina accertarsi che entrambe le opzioni **Qualsiasi indirizzo IP di origine e Qualsiasi indirizzo IP di destinazione** siano selezionate e quindi fare clic su **Avanti** . Queste due impostazioni assicurano che i pacchetti vengano gestiti indipendentemente dal computer (indirizzo IP) di provenienza e dal computer (indirizzo IP) di destinazione.

9.  Nella quarta pagina selezionare **TCP e UDP** dall'elenco a discesa **Seleziona il protocollo a cui si applica questo criterio QoS** . TCP (Transmission Control Protocol) e UDP (User Datagram Protocol) sono i due protocolli di rete più usati da Lync Server e dalle relative applicazioni client.

10. Nel gruppo **Specifica il numero della porta di origine** selezionare **Da questa porta o intervallo di origine** . Nella casella di testo associata, digitare l'intervallo di porte riservato per le trasmissioni audio. Se ad esempio sono state riservate le porte da 49152 a 57500 per il traffico audio, immettere l'intervallo in questo formato **49152:57500** . Fare clic su **Fine** .


> [!NOTE]
> Il valore DSCP di 46 è in qualche modo arbitrario: sebbene il valore DSCP 46 sia spesso usato per contrassegnare i pacchetti audio, non è obbligatorio usarlo per le comunicazioni audio. Se si è già implementata la QoS e si usa un codice DSCP diverso per l'audio (ad esempio, DSCP 40) è necessario configurare il criterio Quality of Service per l'uso dello stesso codice (ovvero 40 per l'audio). Se si sta eseguendo una nuova implementazione della Quality of Service, è consigliabile usare il codice DSCP 46 per l'audio in quando si tratta del valore comunemente usato per contrassegnare i pacchetti audio.



Dopo aver creato il criterio QoS per il traffico audio, è necessario creare un secondo criterio per il traffico video (ed eventualmente un terzo criterio per la gestione del traffico di condivisione delle applicazioni). Per creare un criterio per il traffico video, seguire la stessa procedura di base usata per la creazione del criterio audio, con le distinzioni seguenti:

  - Usare un nome diverso (e univoco) per il criterio (ad esempio, **Lync Server Video** ).

  - Impostare il valore DSCP su **34** invece di 46. Si noti che non è obbligatorio usare il valore DSCP 34. L'unico requisito consiste nell'usare un valore DSCP diverso da quello usato per l'audio.

  - Usare l'intervallo di porte configurato in precedenza per il traffico video. Se ad esempio, sono state riservate le porte da 57501 a 65535 per i contenuti video, impostare l'intervallo di porte su: **57501:65535** .

Se si decide di creare un criterio per gestire il traffico di condivisione delle applicazioni, è necessario creare un terzo criterio con le distinzioni seguenti:

  - Usare un nome diverso (e univoco) per il criterio (ad esempio, **Lync Server Application Sharing** ).

  - Impostare il valore DSCP su **24** invece di 46. Come indicato prima, non è obbligatorio usare il valore DSCP 24. L'unico requisito consiste nell'usare un valore DSCP diverso da quello usato per l'audio.

  - Usare l'intervallo di porte configurato in precedenza per il traffico video. Se ad esempio sono state riservate le porte da 40803 a 49151 per il video, impostare l'intervallo di porte su: **40803:49151** .

I nuovi criteri creati non vengono applicati finché non si aggiorna Criteri di gruppo nei computer Lync Server. Sebbene l'aggiornamento di Criteri di gruppo venga eseguito automaticamente periodicamente, è possibile imporre l'aggiornamento immediato eseguendo il comando seguente su ogni computer in cui è necessario:

    Gpupdate.exe /force

Questo comando può essere eseguito dalla Lync Server Management Shell o da qualsiasi finestra di comando in esecuzione con credenziali di amministratore. Per eseguire una finestra di comando con credenziali di amministratore, fare clic sul pulsante **Start** , fare clic con il pulsante destro del mouse su **Prompt dei comandi** e quindi scegliere **Esegui come amministratore** .

Per verificare che i criteri QoS siano stati applicati, effettuare le operazioni seguenti:

1.  In un computer Lync Server fare clic sul pulsante **Start** e quindi su **Esegui** .

2.  Nella finestra di dialogo **Esegui** digitare **regedit** e quindi premere INVIO.

3.  Nell'editor del Registro di sistema espandere **Computer** , **HKEY\_LOCAL\_MACHINE** , **SOFTWARE** , **Policies** , **Microsoft** , **Windows** e quindi fare clic su **QoS** . In **QoS** dovrebbero essere presenti le chiavi del Registro di sistema per ognuno dei Criteri QoS creati. Se ad esempio sono stati creati due criteri, uno denominato Lync Server Audio QoS e l'altro Lync Server Video QoS, dovrebbero essere presenti le voci per Lync Server Audio QoS e Lync Server Video QoS.

Per assicurare che i pacchetti di rete siano contrassegnati con il valore DSCP appropriato, è consigliabile creare una nuova voce del Registro di sistema su ogni computer completando la procedura seguente:

1.  Fare clic sul pulsante **Start** , quindi scegliere **Esegui** .

2.  Nella finestra di dialogo **Esegui** digitare **regedit** e quindi premere INVIO.

3.  Nell'editor del Registro di sistema espandere **HKEY\_LOCAL\_MACHINE** , **SYSTEM** , **CurrentControlSet** , **Services** e quindi **Tcpip** .

4.  Fare clic con il pulsante destro **Tcpip** , scegliere **Nuovo** e quindi fare clic su **Chiave** . Dopo aver creato la nuova chiave del Registro di sistema, digitare **QoS** e quindi premere INVIO per rinominare la chiave.

5.  Fare clic con il pulsante destro del mouse su **QoS** , scegliere **Nuovo** e quindi **Valore stringa** . Dopo aver creato il nuovo valore del Registro di sistema, digitare **Do not use NLA** e quindi premere INVIO per rinominare il valore.

6.  Fare doppio clic su **Do not use NLA** . Nella finestra di dialogo **Modifica stringa** digitare **1** nella casella **Dati valore** e quindi fare clic su **OK** .

7.  Chiudere l'editor del Registro di sistema e riavviare il computer.

