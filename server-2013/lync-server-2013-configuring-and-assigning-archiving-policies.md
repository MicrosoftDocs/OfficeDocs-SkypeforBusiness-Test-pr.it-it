---
title: Configurazione e assegnazione dei criteri di archiviazione
TOCTitle: Configurazione e assegnazione dei criteri di archiviazione
ms:assetid: acd18ea8-c7f1-4178-871a-cd3b75bdaa8b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205175(v=OCS.15)
ms:contentKeyID: 49301650
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione e assegnazione dei criteri di archiviazione

 

_**Ultima modifica dell'argomento:** 2012-10-01_

In Lync Server 2013 è possibile utilizzare i criteri per abilitare e disabilitare l'archiviazione per le comunicazioni interne ed esterne per gli utenti che si trovano in Lync Server 2013. Sono inclusi i criteri di archiviazione seguenti:

  - Un criterio globale che viene creato per impostazione predefinita quando si distribuisce Lync Server 2013.

  - Criteri a livello di sito e di utente facoltativi che è possibile creare e utilizzare per specificare la modalità di implementazione dell'archiviazione per siti o utenti specifici.

È inizialmente necessario impostare i criteri di archiviazione quando si distribuisce l'archiviazione, ma è possibile modificare, aggiungere ed eliminare criteri dopo la distribuzione. Nel Pannello di controllo di Lync Server 2013 è possibile utilizzare la pagina **Criteri di archiviazione** del gruppo **Archiviazione e monitoraggio** per gestire i criteri a livello globale, di sito e di utente.


> [!NOTE]
> Per controllare l'implementazione dell'archiviazione, è necessario specificare le opzioni nelle configurazioni di archiviazione, ad esempio l'archiviazione delle sessioni di messaggistica istantanea o di conferenza, l'utilizzo della modalità critica e le opzioni di eliminazione. Per impostazione predefinita, nessuna opzione è abilitata nella configurazione di archiviazione globale o in una qualsiasi configurazione di archiviazione a livello di sito o di pool. Specificare tutte le opzioni appropriate nelle configurazioni di archiviazione prima di abilitare l'archiviazione per le comunicazioni interne o esterne nei criteri di archiviazione. Per informazioni dettagliate, vedere <A href="lync-server-2013-managing-archiving-configuration-options-for-your-organization-sites-and-pools.md">Gestione delle opzioni di configurazione dell'archiviazione per l'organizzazione, i siti e i pool in Lync Server 2013</A> nella documentazione relativa alle operazioni.<BR>Se si integra l'archivio di Lync Server con l'archivio di Exchange 2013, i criteri utente di Exchange hanno la precedenza sui criteri di archiviazione di Lync Server 2013, ma solo per gli utenti disponibili in Exchange 2013 le cui cassette postali sono in archiviazione sul posto.



Per informazioni dettagliate sull'implementazione dei criteri, inclusa la gerarchia dei criteri, vedere [Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md) nella documentazione relativa alla pianificazione, alla distribuzione o alle operazioni. Per informazioni dettagliate su come gestire i criteri dopo la distribuzione, vedere [Gestione dell'archiviazione delle comunicazioni interne ed esterne in Lync Server 2013](lync-server-2013-managing-the-archiving-of-internal-and-external-communications.md) nella documentazione relativa alle operazioni.

## Argomenti della sezione

  - [Configurazione dei criteri globali per l'archiviazione](lync-server-2013-configuring-the-global-policy-for-archiving.md)

  - [Configurazione dei criteri sito per l'archiviazione](lync-server-2013-setting-up-site-policies-for-archiving.md)

  - [Impostazione dei criteri di archiviazione per gli utenti](lync-server-2013-setting-up-archiving-policies-for-users.md)

