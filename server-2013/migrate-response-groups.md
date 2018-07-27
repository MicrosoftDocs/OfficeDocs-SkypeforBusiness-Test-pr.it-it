---
title: Eseguire la migrazione di Response Group
TOCTitle: Eseguire la migrazione di Response Group
ms:assetid: 43741ae7-c871-4573-b660-f2f5febc0856
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204854(v=OCS.15)
ms:contentKeyID: 49300352
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eseguire la migrazione di Response Group

 

_**Ultima modifica dell'argomento:** 2013-09-23_

Dopo aver trasferito gli utenti in pool di Lync Server 2013, è possibile eseguire la migrazione dei Response Group. Questa migrazione include la copia di gruppi di agenti, code, flussi di lavoro e file audio, oltre allo spostamento degli oggetti contatto Response Group dalla distribuzione legacy al pool Lync Server 2013. Dopo aver eseguito la migrazione dei Response Group legacy, le chiamate ai Response Group vengono gestite dall' applicazione Response Group nel pool Lync Server 2013. Le chiamate ai Response Group non sono più gestite dal pool legacy.


> [!NOTE]
> Sebbene sia possibile eseguire la migrazione dei Response Group prima di spostare tutti gli utenti nel pool Lync Server 2013, è consigliabile spostare prima tutti gli utenti. In particolare, gli utenti con funzione di agenti di Response Group potranno disporre appieno di tutte le nuove funzionalità solo dopo il trasferimento nel pool Lync Server 2013.



Prima di eseguire la migrazione dei Response Group, è necessario aver distribuito un pool Lync Server 2013 che include l' applicazione Response Group. L' applicazione Response Group viene installata e attivata per impostazione predefinita quando si distribuisce VoIP aziendale. Per assicurarsi che l' applicazione Response Group sia installata, è possibile eseguire il cmdlet **Get-CsService –ApplicationServer**.


> [!NOTE]
> È possibile creare nuovi Response Group di Lync Server 2013 nel pool Lync Server 2013 prima di eseguire la migrazione dei Response Group legacy.



Per eseguire la migrazione dei Response Group da un pool legacy a Lync Server 2013, eseguire il cmdlet **Move-CsRgsConfiguration**.

> [!IMPORTANT]  
> Il cmdlet di migrazione di Response Group sposta la configurazione di Response Group per l'intero pool. Non è possibile selezionare gruppi, code o flussi di lavoro specifici di cui eseguire la migrazione.

Dopo aver eseguito la migrazione dei Response Group, è necessario utilizzare il Pannello di controllo di Lync Server o i cmdlet di Lync Server Management Shell per verificare che siano stati spostati tutti i gruppi di agenti, le code e i flussi di lavoro.

Quando si esegue la migrazione dei Response Group, i Response Group di Lync Server 2010 non vengono rimossi. Quando si gestiscono i Response Group dopo la migrazione utilizzando il Pannello di controllo di Lync Server o Lync Server Management Shell, è possibile visualizzare sia quelli di Lync Server 2010 che quelli di Lync Server 2013. Gli aggiornamenti devono essere applicati esclusivamente ai Response Group di Lync Server 2013. I Response Group di Lync Server 2010 vengono mantenuti solo per scopi di rollback.

> [!CAUTION]  
> Al termine della migrazione e della creazione dei nuovi Response Group, nelle versioni Lync Server 2010 e Lync Server 2013 di ogni Response Group vengono visualizzati il Pannello di controllo di Lync Server e Lync Server Management Shell. Non usare Pannello di controllo di Lync Server o Lync Server Management Shell per rimuovere i Response Group di Lync Server 2010. In caso di rimozione di uno di essi, il Response Group corrispondente creato durante la migrazione smetterà di funzionare. I Response Group di Lync Server 2010 verranno rimossi quando verranno rimosse le autorizzazioni del pool di Lync Server 2010.

> [!IMPORTANT]  
> È consigliabile rimuovere i dati dalla distribuzione precedente solo dopo la rimozione del pool. È inoltre consigliabile esportare i Response Group subito dopo la migrazione. Se viene rimosso un Response Group di Lync Server 2010, è poi possibile ripristinare i Response Group dal backup per ripristinare il funzionamento dei Response Group di Lync Server 2013.

In Lync Server 2013 è stata introdotta una nuova funzionalità dei Response Group denominata **Tipo di flusso di lavoro** . Il **Tipo di flusso di lavoro** può essere **Gestito** o **Non gestito** . Tutti i Response Group vengono migrati con il **Tipo di flusso di lavoro** impostato su **Non gestito** e con un elenco di responsabili vuoto.

Quando si esegue il cmdlet **Move-CsRgsConfiguration**, i gruppi di agenti, le code, i flussi di lavoro e i file audio rimangono nel pool legacy per consentirne il ripristino. Se occorre eseguire il rollback dello stato precedente nel pool legacy, tuttavia, è necessario eseguire il cmdlet **Move-CsApplicationEndpoint** per rispostare gli oggetti contatto nel pool legacy.

Nella procedura seguente per la migrazione delle configurazioni dei Response Group si presuppone che esista una relazione uno-a-uno tra i pool legacy e i pool Lync Server 2013. Se si prevede di consolidare o dividere i pool durante la migrazione e la distribuzione, è necessario pianificare il mapping tra i pool legacy e il pool Lync Server 2013.

## Per eseguire la migrazione delle configurazione dei Response Group

1.  Accedere al computer con un account membro del gruppo RTCUniversalServerAdmins o con le autorizzazioni e i diritti di amministratore equivalenti.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire:
    
        Move-CsRgsConfiguration -Source <source pool FQDN> -Destination <destination pool FQDN>
    
    Ad esempio:
    
        Move-CsRgsConfiguration -Source lync-old.contoso.net -Destination lync-new.contoso.net

4.  Dopo la migrazione dei Response Group e degli agenti al pool Lync Server 2013, l'URL utilizzato dagli agenti per accedere e disconnettersi è un URL di Lync Server 2013 ed è disponibile nel menu **Strumenti** . Ricordare agli agenti di aggiornare eventuali riferimenti, come segnalibri, al nuovo URL.

## Per verificare la migrazione di Response Group tramite i cmdlet di Pannello di controllo di Lync Server

1.  Eseguire l'accesso al computer con un account membro del gruppo RTCUniversalReadOnlyAdmins o come minimo membro del ruolo CsViewOnlyAdministrator.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nel riquadro di spostamento sinistro fare clic su **Response Group** .

4.  Nella scheda **Flusso di lavoro** verificare che nell'elenco siano inclusi tutti i flussi di lavoro dell'ambiente Lync Server 2010.

5.  Fare clic sulla scheda **Coda** e verificare che nell'elenco siano incluse tutte le code dell'ambiente Lync Server 2010.

6.  Fare clic sulla scheda **Gruppo** e verificare che nell'elenco siano inclusi tutti i gruppi di agenti dell'ambiente Lync Server 2010.

## Per verificare la migrazione di Response Group tramite Lync Server Management Shell

1.  Eseguire l'accesso al computer con un account membro del gruppo RTCUniversalReadOnlyAdmins o come minimo membro del ruolo CsViewOnlyAdministrator.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.
    
    Per informazioni dettagliate sui cmdlet seguenti, eseguire:
    
        Get-Help <cmdlet name> -Detailed

3.  Eseguire:
    
        Get-CsRgsAgentGroup

4.  Verificare che nell'elenco siano inclusi tutti i gruppi di agenti dell'ambiente Lync Server 2010.

5.  Eseguire:
    
        Get-CsRgsQueue

6.  Verificare che nell'elenco siano incluse tutte le code dell'ambiente Lync Server 2010.

7.  Eseguire:
    
        Get-CsRgsWorkflow

8.  Verificare che nell'elenco siano inclusi tutti i flussi di lavoro dell'ambiente Lync Server 2010.

