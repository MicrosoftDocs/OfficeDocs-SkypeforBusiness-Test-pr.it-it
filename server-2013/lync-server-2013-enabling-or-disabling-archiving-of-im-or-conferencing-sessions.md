---
title: "Lync Server 2013: Abilita/disab. archiviaz. sessioni di mess. e conferenza"
TOCTitle: "Lync Server 2013: Abilita/disab. archiviaz. sessioni di mess. e conferenza"
ms:assetid: aa4b5983-dbe1-4d64-8a18-fe2c33994e94
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182567(v=OCS.15)
ms:contentKeyID: 49301613
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitazione o disabilitazione dell'archiviazione delle sessioni di messaggistica istantanea e di conferenza

 

_**Ultima modifica dell'argomento:** 2012-10-10_

Nel Pannello di controllo di Lync Server 2013 è possibile utilizzare le configurazioni di archiviazione per abilitare e disabilitare l'archiviazione delle sessioni di messaggistica istantanea, delle sessioni di conferenza o di entrambi i tipi di sessioni. Sono incluse le configurazioni di archiviazione seguenti:

  - Una configurazione globale che viene creata per impostazione predefinita quando si distribuisce Lync Server 2013.

  - Configurazioni a livello di sito e di pool facoltative che è possibile creare e utilizzare per specificare la modalità di implementazione dell'archiviazione per siti o pool specifici.

È inizialmente necessario impostare le configurazioni di archiviazione quando si distribuisce l'archiviazione, ma è possibile modificare, aggiungere ed eliminare configurazioni dopo la distribuzione. Per informazioni dettagliate sulle modalità di implementazione delle configurazioni di archiviazione, incluse le opzioni che è possibile specificare e la gerarchia di tali configurazioni, vedere [Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md) nella documentazione relativa alla pianificazione, alla distribuzione o alle operazioni.


> [!NOTE]
> Per utilizzare l'archiviazione, è necessario configurare criteri di archiviazione per specificare se abilitare l'archiviazione per le comunicazioni interne, per le comunicazioni esterne o per entrambi i tipi di comunicazioni per gli utenti disponibili in Lync Server 2013. Per impostazione predefinita, l'archiviazione non è abilitata per le comunicazioni interne o esterne. Prima di abilitare l'archiviazione in qualsiasi criterio, è necessario specificare le configurazioni di archiviazione appropriate per la distribuzione corrente e, facoltativamente, per siti e pool specifici, come illustrato in questa sezione. Per informazioni dettagliate sull'abilitazione dell'archiviazione, vedere <A href="lync-server-2013-configuring-and-assigning-archiving-policies.md">Configurazione e assegnazione dei criteri di archiviazione</A> nella documentazione di distribuzione.<BR>Se dopo avere distribuito l'archiviazione si decide di utilizzare l'integrazione di Microsoft Exchange per archiviare i file e i dati di archiviazione nei server di Exchange 2013 e tutti gli utenti si trovano nei server di Exchange 2013, rimuovere la configurazione di database di SQL Server dalla topologia. A tale scopo, è necessario utilizzare Generatore di topologie. Per informazioni dettagliate, vedere <A href="lync-server-2013-changing-archiving-database-options.md">Modifica delle opzioni del database di archiviazione in Lync Server 2013</A> nella documentazione relativa alle operazioni.



## Per abilitare o disabilitare l'archiviazione delle sessioni di messaggistica istantanea o di conferenza

1.  Da un account utente assegnato al ruolo CsArchivingAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di navigazione di sinistra fare clic su **Monitoraggio e archiviazione**, quindi scegliere **Configurazione archiviazione**.

4.  Selezionare la configurazione globale, del sito o del pool appropriata nell'elenco delle configurazioni di archiviazione, fare clic su **Modifica**, su **Mostra dettagli** e quindi eseguire le operazioni seguenti:
    
      - Per abilitare l'archiviazione solo per le sessioni di messaggistica istantanea, fare clic su **Archivia sessioni di messaggistica istantanea**.
    
      - Per abilitare l'archiviazione per le sessioni di messaggistica istantanea e le conferenze, fare clic su **Archivia sessioni di messaggistica istantanea e Web Conferencing**.
    
      - Per disabilitare l'archiviazione per il criterio, fare clic su **Disabilita archiviazione**.

5.  Fare clic su **Commit**.

## Vedere anche

#### Ulteriori risorse

[Gestione delle opzioni di configurazione dell'archiviazione per l'organizzazione, i siti e i pool in Lync Server 2013](lync-server-2013-managing-archiving-configuration-options-for-your-organization-sites-and-pools.md)  
[Configurazione e assegnazione dei criteri di archiviazione](lync-server-2013-configuring-and-assigning-archiving-policies.md)

