---
title: "Lync Server 2013: Definisce requisiti dell'organizzazione per l'archiviazione"
TOCTitle: Definizione dei requisiti dell'organizzazione per l'archiviazione
ms:assetid: ce0fc0f6-7704-4b80-bf19-a1fa9818fc7a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205276(v=OCS.15)
ms:contentKeyID: 49302017
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definizione dei requisiti dell'organizzazione per l'archiviazione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-09_

Se l'organizzazione deve attenersi a requisiti di conformità, è possibile distribuire la funzionalità di archiviazione per abilitare il supporto dell'archiviazione per la messaggistica istantanea e le conferenze (riunioni) di Lync Server 2013. Per informazioni dettagliate sul tipo di contenuto che è possibile archiviare, vedere [Panoramica dell'archiviazione in Lync Server 2013](lync-server-2013-overview-of-archiving.md) nella documentazione relativa alla pianificazione.

Per implementare l'archiviazione, è necessario innanzitutto decidere come soddisfare i requisiti di archiviazione dell'organizzazione. A tale scopo, prendere in considerazione i fattori seguenti:

  - **Quando distribuire la funzionalità di archiviazione**. È possibile distribuire la funzionalità di archiviazione durante la distribuzione iniziale di Lync Server 2013 oppure aggiungerla a una distribuzione esistente. Per distribuire l'archiviazione, si utilizza Generatore di topologie per aggiungerla alla topologia e quindi si pubblica la topologia.

  - **Se archiviare comunicazioni interne o esterne**. È possibile abilitare l'archiviazione delle comunicazioni interne (tra utenti interni), delle comunicazioni esterne (che includono almeno un utente all'esterno della rete interna) o di entrambe. Queste opzioni possono essere specificate per l'intera organizzazione oppure per siti e pool particolari. Per impostazione predefinita, non è abilitata alcuna di queste opzioni.
    

    > [!NOTE]
    > Se si utilizza l'integrazione con Microsoft Exchange per memorizzare i dati archiviati, le impostazioni di Exchange determinano se vengono archiviate le comunicazioni di Lync. Se la distribuzione include più foreste, è necessario sincronizzare le impostazioni tra Lync Server ed Exchange. La possibilità di definire l'archiviazione solo per le comunicazioni interne o solo per quelle esterne è disponibile solo nei criteri di Lync. Per l'archiviazione integrata con Exchange è possibile abilitare o meno l'archiviazione di tutte le comunicazioni e non solo di un tipo.



  - **Perché abilitare l'archiviazione**. È possibile abilitare e disabilitare l'archiviazione per l'intera distribuzione a livello globale e per siti e utenti specifici. A ognuno di questi livelli è possibile specificare se abilitare l'archiviazione delle sessioni di messaggistica istantanea (peer-to-peer), delle conferenze (riunioni, ovvero sessioni con più parti) o di entrambe. Per impostazione predefinita, l'archiviazione è disabilitata.

  - **Importanza dell'archiviazione per gli utenti dell'organizzazione**. Se l'archiviazione riveste un'importanza cruciale nell'organizzazione, è possibile specificare l'esecuzione di Lync Server 2013 in modalità critica, che comporta il blocco delle sessioni di messaggistica istantanea e delle conferenze in caso di errore del servizio di archiviazione. Ad esempio:
    
      - Se il servizio di archiviazione non è temporaneamente in grado di inviare un messaggio alla coda del database o di inserire un messaggio nel database, vengono bloccate sia la funzionalità di messaggistica istantanea che quella di conferenza nella distribuzione fino a quando non viene ripristinato il supporto dell'archiviazione.
    
      - Se un utente di conferenza carica un file, ma il file non può essere copiato nell'archivio file, la funzionalità di conferenza viene bloccata nella distribuzione fino alla risoluzione del problema, ma la funzionalità di messaggistica istantanea non viene bloccata.
    
    È possibile configurare questa opzione a livello globale, di sito e di pool. Per impostazione predefinita, la modalità critica non è abilitata.

  - **Se utilizzare l'integrazione con Microsoft Exchange**. Questa opzione consente di integrare lo spazio di archiviazione del servizio di archiviazione con quello di Exchange 2013, in modo che i dati archiviati di Lync Server e i dati archiviati di Exchange 2013 vengano archiviati insieme in Exchange. È possibile utilizzare l'integrazione con Microsoft Exchange per memorizzare i dati di archiviazione degli utenti ospitati in Exchange 2013, qualora le relative cassette postali siano state definite per l'archiviazione sul posto. Se non si dispone di una distribuzione di Exchange 2013, se alcuni utenti di Lync non sono ospitati in Exchange 2013 o se si preferisce non usufruire dell'integrazione, è possibile distribuire database di archiviazione separati utilizzando SQL Server per memorizzare i dati archiviati delle comunicazioni di Lync. L'opzione di integrazione con Microsoft Exchange può essere configurata a livello globale, di sito e di pool. Per impostazione predefinita, l'integrazione con Microsoft Exchange non è abilitata.

  - **Modalità di gestione dei dati archiviati**. Il database di archiviazione non deve essere utilizzato per la conservazione a lungo termine e in Lync Server 2013 non è disponibile una soluzione di e-discovery (ricerca) per i dati archiviati, pertanto i dati devono essere spostati in un altro spazio di archiviazione. In Lync Server non è disponibile uno strumento di esportazione delle sessioni da utilizzare per l'esportazione dei dati archiviati e per creare trascrizioni dei dati in cui eseguire ricerche. Per i criteri globali e per i singoli criteri sito e utente creati, è possibile abilitare l'eliminazione dei dati e specificare una delle opzioni seguenti:
    
      - Eliminare sia i dati di archiviazione esportati che i dati di archiviazione memorizzati dopo un numero specifico di giorni. Il valore minimo supportato è un giorno. Il valore massimo è 2562 giorni.
    
      - Eliminare solo i dati di archiviazione esportati. Questa opzione consente di eliminare tutti i record esportati e contrassegnati come sicuri per l'eliminazione dallo strumento di esportazione delle sessioni.
    
    È possibile configurare questa opzione a livello globale, di sito e di pool. Per impostazione predefinita, l'eliminazione non è abilitata.

È possibile definire l'archiviazione utilizzando i metodi seguenti:

  - **Criteri di archiviazione**. Utilizzare uno o più criteri di archiviazione per abilitare e disabilitare l'archiviazione delle comunicazioni interne ed esterne. Per impostazione predefinita, l'archiviazione non è abilitata. È possibile abilitare o disabilitare l'archiviazione delle comunicazioni interne, di quelle esterne o di entrambi i tipi nella distribuzione utilizzando i criteri globali predefiniti. Non è possibile eliminare i criteri globali. È possibile specificare uno o più criteri sito facoltativi per abilitare o disabilitare l'archiviazione per le comunicazioni interne ed esterne di siti specifici. È inoltre possibile specificare uno o più criteri per abilitare o disabilitare l'archiviazione per utenti e gruppi di utenti specifici. I criteri a livello di utente hanno la priorità sui criteri sito. I criteri a livello di sito hanno la priorità sui criteri a livello globale. I criteri a livello di utente vengono implementati solo per gli utenti specifici configurati per l'utilizzo dei criteri. I messaggi istantanei e le conferenze di gruppo vengono archiviati solo se è configurato un criterio di abilitazione dell'archiviazione per almeno uno dei partecipanti.
    

    > [!NOTE]
    > Se si utilizza l'integrazione con Microsoft Exchange, i criteri di Exchange 2013 hanno la priorità sui criteri di archiviazione di Lync Server per tutti gli utenti ospitati nei server Exchange 2013.



  - **Configurazioni di archiviazione**. È possibile utilizzare una o più configurazioni di archiviazione per specificare la maggior parte delle opzioni di archiviazione descritte precedentemente nell'argomento, ad eccezione dell'abilitazione dell'archiviazione delle comunicazioni interne ed esterne, configurate mediante i criteri di archiviazione come descritto nel punto precedente. Le configurazioni di archiviazione includono la configurazione globale predefinita e le configurazioni facoltative a livello di sito e di pool. Non è possibile eliminare la configurazione globale. Le configurazioni a livello di pool hanno la priorità su quelle a livello di sito. Le configurazioni a livello di sito a loro volta hanno la priorità su quelle a livello globale.

Nell'analisi dei requisiti è necessario determinare come definire la configurazione di archiviazione globale e i criteri di archiviazione globali. È inoltre necessario determinare i requisiti per eventuali configurazioni di archiviazione a livello di sito e a livello di pool, nonché per criteri di archiviazione a livello di sito e a livello di utente.

Se si distribuisce l'archiviazione in un pool Front End o in un server Standard Edition, è consigliabile abilitarla anche per tutti gli altri pool Front End e server Standard Edition della distribuzione. Ciò è necessario perché gli utenti di cui viene richiesta l'archiviazione delle comunicazioni possono essere invitati a una conversazione di messaggistica istantanea o a riunioni di gruppo ospitate in un pool diverso. Se nel pool che ospita la conversazione o la riunione l'archiviazione non è abilitata, è possibile che non vengano archiviati tutti i dati di conferenza. L'archiviazione continuerà a funzionare per gli utenti abilitati e tutti i messaggi di messaggistica istantanea, ma è possibile che il contenuto delle conferenze e gli eventi non vengano archiviati.


> [!NOTE]
> Per abilitare la delega delle attività amministrative nel rispetto degli standard di sicurezza dell'organizzazione, in Lync Server 2013 viene utilizzato il controllo di accesso basato sui ruoli. Con questo tipo di controllo di accesso, i privilegi amministrativi vengono concessi assegnando gli utenti a ruoli amministrativi predefiniti. Per configurare i criteri di archiviazione di Lync e altre impostazioni di configurazione, l'utente deve essere assegnato al ruolo CsArchivingAdministrator, a meno che la configurazione non venga eseguita direttamente nel server in cui è distribuita l'archiviazione, anziché in remoto da un altro computer. Per informazioni dettagliate sul controllo di accesso basato sui ruoli, vedere <A href="lync-server-2013-planning-for-role-based-access-control.md">Pianificazione del controllo di accesso basato sui ruoli in Lync Server 2013</A> nella documentazione relativa alla pianificazione. Per un elenco dei diritti utente, delle autorizzazioni e dei ruoli necessari per la distribuzione delle funzionalità di archiviazione, vedere <A href="lync-server-2013-deployment-checklist-for-archiving.md">Elenco di controllo di distribuzione per l'archiviazione in Lync Server 2013</A>, disponibile sia nella documentazione relativa alla pianificazione che in quella relativa alla distribuzione.<BR>Se si utilizza l'integrazione con Microsoft Exchange, per la configurazione dei criteri di Exchange è necessario disporre delle autorizzazioni e dei diritti di amministratore appropriati. Per informazioni dettagliate, vedere la documentazione relativa a Exchange 2013.


