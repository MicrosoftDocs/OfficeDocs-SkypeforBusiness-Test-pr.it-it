---
title: Gestione dell'archiviazione delle comunicazioni interne ed esterne in Lync Server 2013
TOCTitle: Gestione dell'archiviazione delle comunicazioni interne ed esterne in Lync Server 2013
ms:assetid: 6c2cf941-3204-4f1a-a7e0-416c828056d9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204977(v=OCS.15)
ms:contentKeyID: 49300890
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestione dell'archiviazione delle comunicazioni interne ed esterne in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-09_

In Lync Server 2013, i Criteri di archiviazione sono utilizzati per abilitare o disabilitare l'archiviazione delle comunicazioni interne o esterne quando non si usa l'integrazione di Microsoft Exchange o si hanno utenti non ospitati da Exchange 2013, per le cui cassette postali è stata impostata l'archiviazione sul posto. Tra questi Criteri di archiviazione vi sono:

  - Un criterio globale creato per impostazione predefinita quando si distribuisce Lync Server 2013.

  - Criteri facoltativi a livello di sito e a livello di utente che è possibile creare e utilizzare per specificare la modalità di implementazione dell'archiviazione in relazione a siti e utenti specifici.

I criteri di archiviazione sono configurati durante la distribuzione iniziale dell'archiviazione, ma è possibile aggiungerli, modificarli ed eliminarli anche dopo la distribuzione. In Pannello di controllo di Lync Server 2013, è possibile utilizzare la pagina **Criteri di archiviazione** del gruppo **Archiviazione e monitoraggio** per gestire i criteri a livello globale, sito e utente. Se si integra lo storage di Lync Server con quello di Exchange 2013, i criteri utente di Exchange hanno la precedenza rispetto ai criteri di archiviazione di Lync Server 2013.

Per informazioni dettagliate sulle modalità di implementazione dei criteri e sulle gerarchie dei criteri, vedere [Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md) nella documentazione relativa alla pianificazione o nella documentazione relativa alle operazioni.


> [!NOTE]
> Per controllare l'implementazione dell'archiviazione, è necessario specificare le opzioni di configurazione dell'archiviazione, tra cui l'archiviazione (o meno) di messaggistica istantanea e conferenze, l'utilizzo della modalità critica e le opzioni di eliminazione. Per impostazione predefinita, nessuna delle opzioni nella configurazione dell'archiviazione globale o a livello di sito o pool è abilitata. Prima di abilitare l'archiviazione delle comunicazioni interne o esterne nei criteri di archiviazione è necessario specificare tutte le opzioni appropriate nelle configurazioni di archiviazione. Per ulteriori dettagli, vedere <A href="lync-server-2013-managing-archiving-configuration-options-for-your-organization-sites-and-pools.md">Gestione delle opzioni di configurazione dell'archiviazione per l'organizzazione, i siti e i pool in Lync Server 2013</A> nella documentazione relativa alle operazioni.<BR>Se si abilita l'integrazione di Microsoft Exchange nella propria distribuzione, i criteri Exchange controlleranno se l'archiviazione è abilitata per gli utenti ospitati su Exchange 2013 e per le cui cassette postali è stata impostata l'archiviazione sul posto. Per informazioni dettagliate, vedere <A href="lync-server-2013-setting-up-policies-for-archiving-when-using-exchange-server-integration.md">Configurazione dei criteri per l'archiviazione in caso di utilizzo dell'integrazione di Exchange Server</A> nella documentazione relativa alla distribuzione.



## Argomenti della sezione

  - [Creazione di criteri di archiviazione per abilitare o disabilitare l'archiviazione delle comunicazioni interne o esterne per specifici siti o utenti](lync-server-2013-creating-an-archiving-policy-to-enable-or-disable-archiving-of-internal-or-external-communications-for-specific-sites-or-users.md)

  - [Modifica di criteri di archiviazione per abilitare o disabilitare l'archiviazione delle comunicazioni interne o esterne per l'organizzazione, siti o utenti](lync-server-2013-changing-an-archiving-policy-to-enable-or-disable-archiving-of-internal-or-external-communications-for-your-organization-sites-or-us.md)

  - [Applicazione di criteri di archiviazione agli utenti](lync-server-2013-applying-an-archiving-policy-to-users.md)

  - [Configurazione dei criteri per l'archiviazione in caso di utilizzo dell'integrazione di Exchange Server](lync-server-2013-setting-up-policies-for-archiving-when-using-exchange-server-integration.md)

  - [Eliminazione dei criteri di archiviazione](lync-server-2013-deleting-an-archiving-policy.md)

