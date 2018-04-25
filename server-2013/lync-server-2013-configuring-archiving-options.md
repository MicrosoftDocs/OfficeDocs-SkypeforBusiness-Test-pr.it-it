---
title: Configurazione delle opzioni di archiviazione
TOCTitle: Configurazione delle opzioni di archiviazione
ms:assetid: b2f7f74d-e1ad-494e-9d46-5eb0efe5fb29
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205182(v=OCS.15)
ms:contentKeyID: 49301709
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione delle opzioni di archiviazione

 

_**Ultima modifica dell'argomento:** 2012-10-10_

Nel Pannello di controllo di Lync Server 2013 è possibile utilizzare le configurazioni di archiviazione per specificare la modalità di implementazione dell'archiviazione. Sono incluse le configurazioni di archiviazione seguenti:

  - Una configurazione globale che viene creata per impostazione predefinita quando si distribuisce Lync Server 2013.

  - Configurazioni a livello di sito e di pool facoltative che è possibile creare e utilizzare per specificare la modalità di implementazione dell'archiviazione per siti o pool specifici.

È inizialmente necessario impostare le configurazioni di archiviazione quando si distribuisce l'archiviazione, ma è possibile modificare, aggiungere ed eliminare configurazioni dopo la distribuzione. Nel Pannello di controllo di Lync Server 2013 è possibile utilizzare la pagina **Configurazione archiviazione** del gruppo **Archiviazione e monitoraggio** per gestire le configurazioni a livello globale, di sito e di pool. Per informazioni dettagliate sulla modalità di implementazione delle configurazioni di archiviazione, incluse le opzioni che è possibile specificare e la gerarchia di tali configurazioni, vedere [Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md) nella documentazione relativa alla pianificazione, alla distribuzione o alle operazioni. Per informazioni dettagliate su come gestire le configurazioni dopo la distribuzione, vedere [Gestione delle opzioni di configurazione dell'archiviazione per l'organizzazione, i siti e i pool in Lync Server 2013](lync-server-2013-managing-archiving-configuration-options-for-your-organization-sites-and-pools.md) nella documentazione relativa alle operazioni.


> [!NOTE]
> Per utilizzare l'archiviazione, è necessario configurare criteri di archiviazione per specificare se abilitare l'archiviazione per le comunicazioni interne, per le comunicazioni esterne o per entrambi i tipi di comunicazioni per gli utenti disponibili in Lync Server 2013. Per impostazione predefinita, l'archiviazione non è abilitata per le comunicazioni interne o esterne. Prima di abilitare l'archiviazione in qualsiasi criterio, è necessario specificare le configurazioni di archiviazione appropriate per la distribuzione corrente e, facoltativamente, per siti e pool specifici, come illustrato in questa sezione. Per informazioni dettagliate sull'abilitazione dell'archiviazione, vedere <A href="lync-server-2013-configuring-and-assigning-archiving-policies.md">Configurazione e assegnazione dei criteri di archiviazione</A> nella documentazione relativa alla distribuzione.<BR>Se non si utilizza l'integrazione di Microsoft Exchange per tutti gli utenti nella distribuzione, è necessario configurare criteri di archiviazione per specificare se abilitare l'archiviazione per le comunicazioni interne, per le comunicazioni esterne o per entrambi i tipi di comunicazioni. Per impostazione predefinita, l'archiviazione non è abilitata per le comunicazioni interne o esterne per l'archiviazione dei dati quando si utilizzano database di archiviazione di Lync Server 2013. Prima di abilitare l'archiviazione in qualsiasi criterio, è necessario specificare le configurazioni di archiviazione appropriate per la distribuzione corrente e, facoltativamente, per siti e pool specifici, come illustrato in questa sezione. Per informazioni dettagliate sull'abilitazione dell'archiviazione per l'utilizzo con i database di archiviazione di Lync Server 2013, vedere <A href="lync-server-2013-configuring-and-assigning-archiving-policies.md">Configurazione e assegnazione dei criteri di archiviazione</A> nella documentazione relativa alla distribuzione.



## Argomenti della sezione

  - [Configurazione delle opzioni di archiviazione a livello globale](lync-server-2013-configuring-archiving-options-at-the-global-level.md)

  - [Configurazione delle opzioni di archiviazione per un sito](lync-server-2013-configuring-archiving-options-for-a-site.md)

  - [Configurazione delle opzioni di archiviazione per un pool](lync-server-2013-configuring-archiving-options-for-a-pool.md)

