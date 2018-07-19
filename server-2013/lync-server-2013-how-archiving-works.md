---
title: Funzionamento dell'archiviazione in Lync Server 2013
TOCTitle: Funzionamento dell'archiviazione in Lync Server 2013
ms:assetid: 536a52a9-cfb7-4392-9620-ffc5b319b31b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204900(v=OCS.15)
ms:contentKeyID: 49300592
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Funzionamento dell'archiviazione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-02-04_

Lync Server 2013 L'archiviazione offre alcune opzioni che consentono di soddisfare qualsiasi esigenza relativa alla conformità. Per implementare e gestire l'archiviazione in modo da soddisfare i requisiti dell'organizzazione nel modo più efficiente, è necessario comprendere:

  - Quali informazioni possono essere archiviate.

  - Come abilitare e disabilitare l'archiviazione nella distribuzione in uso.

  - Quali opzioni di archiviazione possono essere configurate per controllare la modalità di implementazione dell'archiviazione.

## Quali informazioni possono essere archiviate?

È possibile archiviare i tipi di contenuto seguenti:

  - Messaggi istantanei peer-to-peer

  - Conferenze (riunioni), che corrispondono in pratica a messaggi istantanei tra più utenti

  - Contenuto di conferenze, compreso il contenuto caricato (ad esempio, stampati) e correlato agli eventi (ad esempio, accesso, uscita, caricamento in condivisione e modifiche della visibilità)

  - Lavagne e sondaggi condivisi durante una conferenza

Non vengono archiviati i tipi di contenuto seguenti:

  - Trasferimenti di file peer-to-peer

  - Audio e video per messaggi istantanei peer-to-peer e conferenze

  - Condivisione di desktop e applicazioni per messaggi istantanei peer-to-peer e conferenze

Lync Server, inoltre, non archivia conversazioni Chat persistente. Per archiviare conversazioni Chat persistente, è necessario abilitare e configurare il servizio Conformità, un componente che può essere distribuito con il server Chat persistente di Microsoft Lync Server 2013. Per informazioni dettagliate, vedere [Pianificazione del server Chat persistente in Lync Server 2013](lync-server-2013-planning-for-persistent-chat-server.md) nella documentazione relativa alla pianificazione.

## Come si inizia a usare la funzionalità di archiviazione?

L'installazione della funzionalità di archiviazione avviene automaticamente in ogni Front End Server durante la distribuzione del server. L'abilitazione della funzionalità, tuttavia, avviene solo al momento della configurazione. La modalità di configurazione dell'archiviazione è determinata dalla modalità di distribuzione usata:

  - **Archiviazione con uso dell'integrazione di Microsoft Exchange.** Se un certo numero di utenti è disponibile in Exchange 2013 e le cassette postali di questi sono impostate per l'archiviazione sul posto, è possibile selezionare l'opzione per l'integrazione dell'archiviazione Lync Server 2013 con l'archiviazione Exchange. Se si sceglie l'opzione relativa all'integrazione di Microsoft Exchange, per il controllo dell'archiviazione dei dati di Lync Server 2013 per gli utenti interessati si usano i criteri e le configurazioni di Exchange 2013.

  - **Archiviazione con uso di database di archiviazione di Lync Server.** Se un certo numero di utenti non è disponibile in Exchange 2013, le cassette postali di questi utenti non sono impostate per l'archiviazione sul posto o non si vuole usare l'integrazione di Microsoft Exchange per alcuni o per tutti gli utenti presenti nella distribuzione, è possibile distribuire database di archiviazione di Lync Server mediante SQL Server per memorizzare i dati di archiviazione per gli utenti interessati. In questo caso, sono i criteri e le configurazioni di archiviazione di Lync Server 2013 a determinare l'abilitazione e la modalità di implementazione dell'archiviazione. Per usare Lync Server 2013, è necessario aggiungere i database SQL Server appropriati alla topologia e pubblicare quest'ultima.

## Impostazione della funzionalità di archiviazione per l'uso dell'integrazione di Microsoft Exchange

Se gli utenti sono disponibili in Exchange 2013 e le loro cassette postali sono impostate per l'archiviazione sul posto, è possibile eseguire l'archiviazione Lync Server 2013 di questi utenti tramite l'opzione relativa all'**integrazione di Microsoft Exchange** (descritta più avanti in questa sezione) e quindi controllare l'archiviazione per tali utenti specificando criteri e impostazioni dell'archiviazione sul posto di Exchange. È inoltre possibile impostare configurazioni di Lync Server per controllare quanto segue:

  - Archiviazione dei messaggi istantanei, delle conferenze o di entrambi.

  - Implementazione della modalità critica per la distribuzione Lync Server.

  - Selezione dell'opzione di integrazione di Microsoft Exchange per l'uso di Exchange 2013 per la memorizzazione dei dati archiviati.

Queste opzioni di configurazione di archiviazione di Lync Server 2013 sono descritte più avanti in questa sezione. Per informazioni su come configurare i criteri e le impostazioni dell'archiviazione sul posto di Exchange per supportare l'archiviazione, vedere la documentazione del prodotto Exchange 2013.

## Impostazione della funzionalità di archiviazione per l'uso con database di archiviazione di Lync Server

Se si vogliono usare database di archiviazione di Lync Server (database SQL Server) per archiviare dati di utenti specifici presenti nella distribuzione, è possibile configurare criteri di archiviazione di Lync Server per controllare l'abilitazione dell'archiviazione per tali utenti. Nei criteri di archiviazione è possibile abilitare o disabilitare la funzionalità per uno o entrambi i tipi di comunicazione seguenti:

  - Comunicazioni interne

  - Comunicazioni esterne

Per impostazione predefinita, in tutti i criteri di archiviazione di Lync Server l'archiviazione è disabilitata sia per le comunicazioni interne che per quelle esterne. È possibile abilitare e disabilitare le comunicazioni tramite il Pannello di controllo di Lync Server 2013 o cmdlet in Lync Server 2013 Management Shell.

I criteri di archiviazione di Lync Server 2013 sono:

  - **Criteri di archiviazione globale**. Questi criteri di archiviazione sono predefiniti e si applicano all'intera distribuzione. Vengono creati al momento della distribuzione di Lync Server 2013 e, per impostazione predefinita, disabilitano l'archiviazione sia per le comunicazioni interne che per quelle esterne. Non è possibile eliminare questi criteri. Se si sceglie l'opzione di eliminazione, per i criteri globali vengono ripristinate le impostazioni predefinite.

  - **Criteri di archiviazione a livello di sito**. Facoltativamente è possibile abilitare o disabilitare l'archiviazione per uno o più siti specifici creando e configurando criteri di archiviazione a livello di sito per i siti interessati. Quando si creano criteri di archiviazione a livello di sito, per impostazione predefinita l'archiviazione è disabilitata. È possibile eliminare i criteri di archiviazione a livello di sito creati. I criteri di archiviazione a livello di sito forzano i criteri globali, ma solo per il sito specificato nei criteri stessi. Se ad esempio si abilita l'archiviazione per le comunicazioni interne ed esterne nei criteri globali e si creano criteri a livello di sito in cui si disabilita l'archiviazione per le comunicazioni esterne, per il sito in questione verranno archiviate solo le comunicazioni interne.

  - **Criteri di archiviazione a livello di utente**. Facoltativamente è possibile abilitare o disabilitare l'archiviazione per uno o più utenti e gruppi di utenti specifici creando, configurando e applicando criteri di archiviazione a livello di utente per gli utenti e i gruppi di utenti specificati. Quando si creano criteri di archiviazione a livello di utente, per impostazione predefinita l'archiviazione è disabilitata. È possibile eliminare i criteri di archiviazione a livello di utente creati e cambiare gli utenti e i gruppi di utenti a cui applicare tali criteri. I criteri di archiviazione a livello di utente forzano i criteri globali e i criteri sito, ma solo per gli utenti e i gruppi di utenti a cui i criteri a livello di utente sono applicati. Se ad esempio si disabilita l'archiviazione per le comunicazioni interne ed esterne nei criteri globali, si creano criteri a livello di sito con cui si abilita l'archiviazione delle comunicazioni interne ed esterne e quindi si creano criteri a livello di utente con cui si disabilita l'archiviazione per le comunicazioni esterne, l'archiviazione verrà eseguita per le comunicazioni esterne e interne per gli utenti di tutti i siti ad eccezione degli utenti a cui si applicano i criteri a livello di utente, per i quali verranno archiviate solo le comunicazioni interne.

Per informazioni dettagliate su come impostare criteri di archiviazione iniziali durante la distribuzione della funzionalità di archiviazione, vedere [Configurazione e assegnazione dei criteri di archiviazione](lync-server-2013-configuring-and-assigning-archiving-policies.md) nella documentazione relativa alla distribuzione. Per informazioni dettagliate sull'uso di criteri di archiviazione per abilitare e disabilitare le comunicazioni dopo la distribuzione, vedere [Gestione dell'archiviazione delle comunicazioni interne ed esterne in Lync Server 2013](lync-server-2013-managing-the-archiving-of-internal-and-external-communications.md) nella documentazione relativa alle operazioni.


> [!NOTE]
> Se si implementano entrambi i database di archiviazione Lync Server 2013 e si abilita l'integrazione di Microsoft Exchange, i criteri di Exchange 2013 forzano i criteri di archiviazione di Lync Server, ma solo per gli utenti disponibili in Exchange 2013 con la cassetta postale impostata per l'archiviazione sul posto. La funzionalità di archiviazione di Lync dipende solo dai criteri di archiviazione sul posto di Microsoft Exchange.



## Quali sono le opzioni disponibili per la configurazione dell'archiviazione?

Oltre all'uso di criteri e alla possibilità di abilitare e disabilitare l'archiviazione, sono disponibili altre opzioni di archiviazione configurabili per l'intera distribuzione e, facoltativamente, per siti e pool specifici. È possibile controllare la maggior parte delle opzioni di archiviazione mediante una o più delle configurazioni disponibili nel Pannello di controllo di Lync Server 2013. Esiste inoltre un'altra opzione, configurabile solo tramite Lync Server 2013 Management Shell.

## Opzioni di configurazione dell'archiviazione disponibili nel Pannello di controllo di Lync Server 2013

Per ciascuna configurazione di archiviazione sono disponibili le opzioni seguenti:

La configurazione a livello globale viene creata automaticamente quando si distribuisce la funzionalità di archiviazione e può essere configurata, ma non eliminata. Se si seleziona l'opzione di eliminazione della configurazione globale, per le impostazioni vengono ripristinati i valori predefiniti. È possibile creare più configurazioni a livello di sito e di pool che, insieme alla configurazione globale, consentono di controllare le impostazioni di archiviazione. Per la configurazione globale e la configurazione a livello di ogni sito e di ogni pool sono disponibili le opzioni seguenti:

  - Disabilitare l'archiviazione, abilitare l'archiviazione solo per la messaggistica istantanea o abilitarla sia per la messaggistica istantanea che per le conferenze.

  - Configurare la modalità critica in modo da bloccare le sessioni di messaggistica istantanea e di conferenza nel caso di un errore di Lync Server. Gli errori possono riguardare:
    
      - **Messaggistica istantanea**, nel caso di un problema del servizio di archiviazione di Lync Server. In questo caso, la funzionalità di messaggistica istantanea viene bloccata per gli utenti per i quali l'archiviazione è abilitata.
    
      - **Conferenze**, nel caso di una condivisione file non disponibile o di un problema del servizio di archiviazione. In questo caso, tutte le conferenze attive ospitate nel pool al momento dell'errore passano in modalità limitata e non è possibile attivare nuove conferenze.
    
    Sia la funzionalità di messaggistica istantanea che il servizio di conferenza vengono ripristinati automaticamente subito dopo la correzione degli errori.

  - Specificare l'uso dell'integrazione di Microsoft Exchange Server 2013 per usare Exchange 2013 per la memorizzazione dei dati archiviati, invece di impostare database SQL Server separati per la memorizzazione dei dati di archiviazione di Lync Server 2013.

  - Configurare opzioni di eliminazione per i dati archiviati. Questa opzione consente di specificare quando eliminare i dati archiviati, scegliendo tra le alternative seguenti:
    
      - Dopo il numero di giorni specificato
    
      - Dopo l'esportazione dei dati di archiviazione. Questa alternativa comprende i dati caricati in Exchange, se si abilita l'integrazione di Microsoft Exchange.
    

    > [!NOTE]
    > Se si abilita l'integrazione di Microsoft Exchange, l'eliminazione degli utenti ospitati in Exchange 2013 con cassette postali impostate per l'archiviazione sul posto è controllata da Exchange. L'unica qualifica riguarda i file di conferenza, che vengono memorizzati nella condivisione file di Lync Server. Questi file vengono eliminati dalla condivisione file solo dopo che sono stati esportati (caricati in Exchange), se si seleziona l'opzione relativa all'eliminazione dei dati dopo l'esportazione dei dati di archiviazione, oppure dopo il numero massimo di giorni specificato, se si specifica il numero massimo di giorni di conservazione.



Per impostazione predefinita, non sono abilitate opzioni di archiviazione. Per gestire le configurazioni di archiviazione è possibile usare il Pannello di controllo di Lync Server 2013.

Si possono specificare le configurazioni di archiviazione seguenti:

  - **Configurazione di archiviazione globale**. Questa è la configurazione di archiviazione predefinita e si applica all'intera distribuzione. Viene creata al momento della distribuzione di Lync Server 2013 e, per impostazione predefinita, non abilita la funzionalità di archiviazione. È possibile modificare la configurazione globale, ma non è possibile eliminarla. Se si sceglie l'opzione di eliminazione, per la configurazione globale vengono ripristinate le impostazioni predefinite.

  - **Configurazione di archiviazione a livello di sito**. Facoltativamente è possibile configurare l'archiviazione per uno o più siti specifici creando e impostando una configurazione di archiviazione a livello di sito per un sito singolo. Una configurazione di archiviazione a livello di sito esiste solo se viene creata. È possibile modificare o eliminare le configurazioni di archiviazione a livello di sito. Le configurazioni di archiviazione a livello di sito forzano la configurazione globale, ma solo per il sito specificato nella configurazione a livello di sito. Se, ad esempio, nella configurazione globale si abilita la funzionalità di archiviazione solo per la messaggistica istantanea e si crea una configurazione a livello di sito in cui si abilita l'archiviazione sia per la messaggistica istantanea che per le conferenze, queste ultime verranno archiviate solo per il sito ma non per il resto dell'organizzazione.

  - **Configurazione di archiviazione a livello di pool**. Facoltativamente è possibile specificare impostazioni di archiviazione per uno o più pool specifici creando e impostando una configurazione a livello di pool per un pool singolo. Una configurazione di archiviazione a livello di pool esiste solo se viene creata. È possibile modificare ed eliminare le configurazioni di archiviazione a livello di pool. Le configurazioni di archiviazione a livello di pool forzano la configurazione globale e le eventuali configurazioni di archiviazione a livello di sito create. Se, ad esempio, nella configurazione globale si abilita la funzionalità di archiviazione solo per la messaggistica istantanea, si crea una configurazione a livello di sito in cui è abilitata l'archiviazione sia per la messaggistica istantanea che per le conferenze del sito e quindi si crea una configurazione a livello di pool in cui l'archiviazione è abilitata solo per la messaggistica istantanea, le comunicazioni di messaggistica istantanea e di conferenza verranno archiviate per tutti gli utenti del sito ad eccezione degli utenti disponibili nel pool specificato nella configurazione a livello di pool. Per tutti gli altri utenti dell'organizzazione, l'archiviazione sarà abilitata solo per la messaggistica istantanea.

Per informazioni dettagliate su come impostare configurazioni di archiviazione iniziali durante la distribuzione della funzionalità di archiviazione, vedere [Configurazione delle opzioni di archiviazione](lync-server-2013-configuring-archiving-options.md) nella documentazione relativa alla distribuzione. Per informazioni dettagliate sull'uso di criteri di archiviazione per abilitare e disabilitare le comunicazioni dopo la distribuzione, vedere [Gestione delle opzioni di configurazione dell'archiviazione per l'organizzazione, i siti e i pool in Lync Server 2013](lync-server-2013-managing-archiving-configuration-options-for-your-organization-sites-and-pools.md) nella documentazione relativa alle operazioni.

## Opzioni di archiviazione disponibili solo in Windows PowerShell

Con Lync Server 2013 Management Shell è possibile usare cmdlet per implementare opzioni non disponibili nel Pannello di controllo di Lync Server 2013. Queste opzioni sono:

  - **Archiviazione di messaggi duplicati**. Per informazioni dettagliate, vedere [New-CsArchivingConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsArchivingConfiguration) e [Set-CsArchivingConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsArchivingConfiguration) nella documentazione relativa alle operazioni.

  - **Esportazione di dati archiviati**. Per informazioni dettagliate, vedere [Export-CsArchivingData](https://docs.microsoft.com/en-us/powershell/module/skype/Export-CsArchivingData)

## Come si accede ai dati archiviati?

La modalità di accesso ai dati archiviati dipende dalla posizione dei dati stessi:

  - **Archiviazione Microsoft Exchange**. Se si sceglie l'opzione di integrazione di Exchange, Lync Server deposita il contenuto di archiviazione nell'archivio di Exchange 2013 per tutti gli utenti ospitati in Exchange 2013 con cassette postali impostate per l'archiviazione sul posto. I dati archiviati sono memorizzati nella cartella Elementi ripristinabili delle cassette postali degli utenti, in genere non visibile per gli utenti, all'interno della quale possono eseguire ricerche solo gli utenti che dispongono del ruolo **Gestione individuazione** di Exchange. Exchange consente la ricerca federata e l'individuazione, insieme a SharePoint, se distribuito. Per ulteriori informazioni sull'archiviazione, la conservazione e l'individuazione di dati archiviati in Exchange, vedere la documentazione di Exchange 2013 e SharePoint.

  - **Archiviazione Lync Server**. Se si impostano database di archiviazione di Lync Server 2013 per l'archiviazione di dati Lync Server, Lync Server deposita il contenuto di archiviazione nei database di archiviazione di Lync Server (database SQL Server) per tutti gli utenti non disponibili in Exchange 2013 le cui cassette postali non sono impostate per l'archiviazione sul posto. Non è possibile sottoporre questi dati a ricerca, ma è possibile esportarli nei formati di altri strumenti di ricerca. Per informazioni dettagliate sull'esportazione di dati memorizzati all'interno di database di archiviazione, vedere [Esportazione dei dati archiviati da Lync Server 2013](lync-server-2013-exporting-archived-data.md) nella documentazione relativa alle operazioni.

Per ulteriori informazioni sulla collaborazione tra Lync Server 2013 e Exchange 2013, vedere [Supporto per l'integrazione di Exchange Server e SharePoint in Lync Server 2013](lync-server-2013-exchange-and-sharepoint-integration-support.md) nella documentazione relativa alla supportabilità.

