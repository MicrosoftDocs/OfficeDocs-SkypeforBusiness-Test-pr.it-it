---
title: Eseguire la migrazione di Response Group
TOCTitle: Eseguire la migrazione di Response Group
ms:assetid: 5c07bf4b-ad8a-4b83-b970-7d933bb7c4ef
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204931(v=OCS.15)
ms:contentKeyID: 49300669
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eseguire la migrazione di Response Group

 

_**Ultima modifica dell'argomento:** 2012-10-19_

Dopo aver trasferito gli utenti in pool di Lync Server 2013, è possibile eseguire la migrazione dei Response Group. Questa migrazione include la copia di gruppi di agenti, code, flussi di lavoro e file audio, oltre allo spostamento degli oggetti contatto Response Group dalla distribuzione legacy al pool Lync Server 2013. Dopo aver eseguito la migrazione dei Response Group legacy, le chiamate ai Response Group vengono gestite dall' applicazione Response Group nel pool Lync Server 2013. Le chiamate ai Response Group non sono più gestite dal pool legacy.


> [!NOTE]
> Sebbene sia possibile eseguire la migrazione dei Response Group prima di spostare tutti gli utenti nel pool Lync Server 2013, è consigliabile spostare prima tutti gli utenti. In particolare, gli utenti con funzione di agenti di Response Group potranno disporre appieno di tutte le nuove funzionalità solo dopo il trasferimento nel pool Lync Server 2013.



Prima di eseguire la migrazione dei Response Group, è necessario aver distribuito un pool Lync Server 2013 che include l' applicazione Response Group. L' applicazione Response Group viene installata e attivata per impostazione predefinita quando si distribuisce VoIP aziendale. Per assicurarsi che l' applicazione Response Group sia installata, è possibile eseguire il cmdlet **Get-CsService–ApplicationServer**.


> [!NOTE]
> È possibile creare nuovi Response Group di Lync Server 2013 nel pool Lync Server 2013 prima di eseguire la migrazione dei Response Group legacy.



Per eseguire la migrazione dei Response Group da un pool legacy a Lync Server 2013, eseguire il cmdlet **Move-CsRgsConfiguration**. Prima di poter eseguire **Move-CsRgsConfiguration**, è necessario installare il pacchetto delle interfacce utente per la compatibilità con le versioni precedenti di Strumentazione gestione Windows (WMI). Installare questa applicazione eseguendo OCSWMIBC.msi, disponibile nei supporti di installazione nella cartella Setup.

> [!IMPORTANT]  
> Il cmdlet di migrazione di Response Group sposta la configurazione di Response Group per l'intero pool. Non è possibile selezionare gruppi, code o flussi di lavoro specifici di cui eseguire la migrazione.

Dopo aver eseguito la migrazione dei Response Group è necessario aggiornare l'URL utilizzato dagli agenti formali per accedere ai Response Group e disconnettersi, quindi utilizzare il Pannello di controllo di Lync Server o i cmdlet di Lync Server Management Shell per verificare che siano stati spostati tutti i gruppi di agenti, le code e i flussi di lavoro.

> [!CAUTION]  
> Quando si esegue la migrazione dei Response Group, i Response Group di Office Communications Server 2007 R2 non vengono rimossi. Non rimuovere i Response Group di Office Communications Server 2007 R2. Se si rimuove un Response Group di Office Communications Server 2007 R2, quelli in Lync Server 2013 smettono di funzionare.

> [!IMPORTANT]  
> È consigliabile rimuovere i dati dalla distribuzione precedente solo dopo la rimozione del pool. È inoltre caldamente consigliabile esportare i Response Group subito dopo la migrazione. Se viene rimosso un Response Group di Office Communications Server 2007 R2 , è poi possibile ripristinare i Response Group dal backup per ripristinare il funzionamento dei Response Group di Lync Server 2013.

Quando si esegue il cmdlet **Move-CsRgsConfiguration**, i gruppi di agenti, le code, i flussi di lavoro e i file audio rimangono nel pool legacy per consentirne il ripristino. Se occorre eseguire il rollback dello stato precedente nel pool legacy, tuttavia, è necessario eseguire il cmdlet **Move-CsApplicationEndpoint** per rispostare gli oggetti contatto nel pool legacy.

> [!IMPORTANT]  
> È consigliabile eliminare eventuali dati dei Response Group nel pool legacy solo dopo la rimozione del pool.

Nella procedura seguente per la migrazione delle configurazioni dei Response Group si presuppone che esista una relazione uno-a-uno tra i pool legacy e i pool Lync Server 2013. Se si prevede di consolidare o dividere i pool durante la migrazione e la distribuzione, è necessario pianificare il mapping tra i pool legacy e il pool Lync Server 2013.

## Per eseguire la migrazione delle configurazioni dei Response Group

1.  Individuare il file OCSWMIBC.msi nella cartella Setup dei supporti di installazione e installarlo.

2.  Accedere al computer con un account membro del gruppo RTCUniversalServerAdmins o con le autorizzazioni e i diritti di amministratore equivalenti.

3.  Aprire Lync Server Management Shell.

4.  Nella riga di comando digitare quanto segue:
    
        Move-CsRgsConfiguration -Source <source pool FQDN> -Destination <destination pool FQDN>
    
    Ad esempio:
    
        Move-CsRgsConfiguration -Source pool01.contoso.net -Destination pool02.contoso.net

5.  Se è stata distribuita la scheda Response Group per Microsoft Office Communicator 2007 R2 nell'ambiente Office Communications Server 2007 R2, rimuoverla dal file tabs.xml di Office Communicator 2007 R2.
    

    > [!NOTE]
    > Gli agenti formali utilizzavano la scheda Response Group per accedere ai Response Group in modo da poter ricevere le chiamate. Se si distribuiva la scheda Response Group, si sceglieva il percorso del file tabs.xml di Office Communicator 2007 R2 al momento della distribuzione.



6.  Fornire agli utenti l'URL aggiornato richiesto dagli agenti per l'accesso e la disconnessione dai Response Group.
    

    > [!NOTE]
    > L'URL in genere è https://FQDNpoolWeb/RgsClients/Tab.aspx, dove <EM>FQDNpoolWeb</EM> è il nome di dominio completo (FQDN) del pool Web associato al pool di cui è stata eseguita la migrazione in Lync Server 2013.

    

    > [!NOTE]
    > Questo passaggio non è necessario dopo che gli utenti eseguono l'aggiornamento a Lync 2013, poiché l'URL è disponibile dal menu <STRONG>Strumenti</STRONG> in Lync.



## Per verificare la migrazione dei Response Group tramite il Pannello di controllo di Lync Server

1.  Aprire Pannello di controllo di Lync Server.

2.  Nel riquadro di spostamento sinistro fare clic su **Response Group** .

3.  Nella scheda **Flusso di lavoro** verificare che nell'elenco siano inclusi tutti i flussi di lavoro dell'ambiente Office Communications Server 2007 R2.

4.  Fare clic sulla scheda **Coda** e verificare che nell'elenco siano incluse tutte le code dell'ambiente Office Communications Server 2007 R2.

5.  Fare clic sulla scheda **Gruppo** e verificare che nell'elenco siano inclusi tutti i gruppi di agenti dell'ambiente Office Communications Server 2007 R2.

## Per verificare la migrazione dei Response Group tramite i cmdlet

1.  Aprire Lync Server Management Shell.
    
    Per informazioni dettagliate sui cmdlet seguenti, eseguire:
    
        Get-Help <cmdlet name> -Detailed

2.  Nella riga di comando digitare quanto segue:
    
        Get-CsRgsAgentGroup

3.  Verificare che nell'elenco siano inclusi tutti i gruppi di agenti dell'ambiente Office Communications Server 2007 R2.

4.  Nella riga di comando digitare quanto segue:
    
        Get-CsRgsQueue

5.  Verificare che nell'elenco siano incluse tutte le code dell'ambiente Office Communications Server 2007 R2.

6.  Nella riga di comando digitare quanto segue:
    
        Get-CsRgsWorkflow

7.  Verificare che nell'elenco siano inclusi tutti i flussi di lavoro dell'ambiente Office Communications Server 2007 R2.

