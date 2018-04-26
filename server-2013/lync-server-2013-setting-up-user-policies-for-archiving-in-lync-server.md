---
title: Impostazione dei criteri utente per l'archiviazione in Lync Server
TOCTitle: Impostazione dei criteri utente per l'archiviazione in Lync Server
ms:assetid: 22d6cc76-6b5c-4a8c-bb8a-7996450ec085
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204742(v=OCS.15)
ms:contentKeyID: 49299929
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Impostazione dei criteri utente per l'archiviazione in Lync Server

 

_**Ultima modifica dell'argomento:** 2012-10-10_

L'abilitazione o la disabilitazione dell'archiviazione per utenti specifici ospitati in Lync Server 2013 richiede la creazione e la configurazione di uno o più criteri utente, quindi l'applicazione dei criteri appropriati a utenti o gruppi di utenti specifici. I criteri utente sostituiscono i criteri sito e globali, ma solo per gli utenti ospitati in Lync Server 2013.

Gli utenti sono sempre ospitati in Lync Server. Se è abilitata l'integrazione di Microsoft Exchange, non è necessario che siano gestiti i criteri di archiviazione in Lync Server per gli utenti con cassette postali in Microsoft Exchange Server 2013. Questi utenti con archiviazione saranno gestiti dall'archiviazione sul posto di Exchange.

Per informazioni sul funzionamento dei criteri di archiviazione, inclusa la gerarchia per i criteri globali, sito e utente, vedere [Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md) nella documentazione relativa alla pianificazione, alla distribuzione o alle operazioni.


> [!NOTE]
> Se è stata abilitata l'integrazione di Microsoft Exchange per una distribuzione, i criteri di archiviazione sul posto di Exchange controllano se l'archiviazione è abilitata per gli utenti ospitati in Exchange 2013. L'archiviazione per questi utenti richiede che abbiano le cassette postali archiviate sul posto. Per informazioni, vedere <A href="lync-server-2013-setting-up-policies-for-archiving-when-using-exchange-server-integration.md">Configurazione dei criteri per l'archiviazione in caso di utilizzo dell'integrazione di Exchange Server</A> nella documentazione relativa alla distribuzione.<BR>È necessario specificare tutte le opzioni appropriate nelle configurazioni di archiviazione prima di abilitare l'archiviazione. Per informazioni, vedere <A href="lync-server-2013-configuring-archiving-options.md">Configurazione delle opzioni di archiviazione</A> nella documentazione relativa alla distribuzione.



## Argomenti della sezione

  - [Creazione e configurazione dei criteri utente per l'archiviazione in Lync Server](lync-server-2013-creating-and-configuring-user-policies-for-archiving-in-lync-server.md)

  - [Applicazione di criteri di archiviazione di Lync Server a un utente](lync-server-2013-applying-a-lync-server-archiving-policy-to-a-user.md)

