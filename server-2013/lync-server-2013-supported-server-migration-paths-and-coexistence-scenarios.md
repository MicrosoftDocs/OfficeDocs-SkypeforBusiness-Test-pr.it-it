---
title: "Lync Server 2013: Supporta percorsi migraz. server e scenari di coesistenza"
TOCTitle: Percorsi di migrazione dei server supportati e scenari di coesistenza
ms:assetid: 2a6a730f-7f80-45f9-9540-3edfdaa265fb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425764(v=OCS.15)
ms:contentKeyID: 49300009
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Percorsi di migrazione dei server supportati e scenari di coesistenza in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-16_

Lync Server 2013 supporta la migrazione da uno degli ambienti seguenti:

  - Microsoft Lync Server 2010

  - Microsoft Office Communications Server 2007 R2

La migrazione da un ambiente in cui vengono eseguite entrambe le versioni sopra indicate non è supportata, così come non è supportata la migrazione da versioni precedenti, ad esempio Microsoft Office Communications Server 2007 o Live Communications Server 2005. Se la distribuzione precedente includeva Group Chat, è necessario eseguirne la migrazione separatamente.

## Metodi di migrazione

È supportata la migrazione di tutte le topologie e di tutti i ruoli server di Lync Server. È possibile eseguire la migrazione da una topologia a un'altra, incluso da un server Standard Edition a un server Enterprise Edition.

Lync Server 2013 supporta solo il metodo di migrazione seguente:

   **Migrazione side-by-side** In questo tipo di migrazione Lync Server 2013 viene distribuito accanto a una distribuzione esistente di Microsoft Lync Server 2010 o di Office Communications Server 2007 R2 e quindi le operazioni vengono trasferite nei nuovi server e gli utenti vengono spostati in Lync Server 2013. Questo metodo richiede l'uso di ulteriori piattaforme server, inclusi hardware e software, durante la migrazione e i nomi dei sistemi e dei pool sono diversi nella nuova configurazione. Se è necessario ripristinare la versione precedente, è possibile spostare di nuovo le operazioni nei server precedenti.

La migrazione attraverso foreste di Servizi di dominio Active Directory non è supportata.

Il metodo di migrazione consigliato è di tipo incrementale. Per informazioni dettagliate sulla migrazione da una versione precedente, inclusa la tempistica appropriata per la distribuzione dei componenti, vedere gli argomenti seguenti nella documentazione relativa alla migrazione:

  - [Migrazione da Lync Server 2010 a Lync Server 2013](migration-from-lync-server-2010-to-lync-server-2013.md)

  - [Migrazione da Office Communications Server 2007 R2 a Lync Server 2013](migration-from-office-communications-server-2007-r2-to-lync-server-2013.md)

  - [Migrazione da Lync Server 2010, Group Chat o Office Communications Server 2007 R2 Group Chat al server chat persistente di Lync Server 2013](migration-from-lync-server-2010-group-chat-or-office-communications-server-2007-r2-group-chat-to-lync-server-2013-persistent-chat-server.md)

## Scenari di coesistenza

Lync Server 2013 può coesistere con i componenti di una distribuzione di Lync Server 2010 o di Office Communications Server 2007 R2. La distribuzione simultanea di Lync Server 2013 con entrambi Lync Server 2010 e Office Communications Server 2007 R2 (distribuzione simultanea di tutte e tre le versioni) non è supportata.

Durante una migrazione incrementale in cui una distribuzione precedente di Lync Server 2010 o di Office Communications Server 2007 R2 coesistono temporaneamente con la distribuzione di Lync Server 2013, il supporto per il routing della versione mista è limitato. Per informazioni dettagliate, vedere la documentazione relativa alla migrazione.

È necessario usare computer distinti e separati che eseguono Microsoft SQL Server 2008 R2 o Microsoft SQL Server 2012 per le istanze del database di Lync Server 2013. Non è possibile usare per un pool Front End di Lync Server 2013 la stessa istanza di SQL Server usata per un pool Front End di Lync Server 2010 o di Office Communications Server 2007 R2. Se si definisce e si configura Lync Server 2013 in Generatore di topologie per una distribuzione in cui Lync Server 2010 o Office Communications Server 2007 R2 è già distribuito, Generatore di topologie non consentirà di definire un'istanza di un Lync Server 2013 già in uso nella topologia.

Generatore di topologie visualizzerà il messaggio seguente per informare l'utente del problema: "SQL server \[FQDN del server\] contiene già un ruolo che ospita un'istanza SQL 'Archivio utenti'."


> [!NOTE]
> Se si prevede di distribuire ruoli server che sono nuovi per la distribuzione di Lync Server 2013, è consigliabile eseguire innanzitutto l'aggiornamento della distribuzione esistente come descritto nella documentazione relativa alla migrazione e alla distribuzione e quindi distribuire i nuovi ruoli server come descritto nella documentazione relativa alla pianificazione e alla distribuzione. Se si sta eseguendo la migrazione di una versione precedente di Group Chat, eseguire questa operazione per ultima, dopo aver completato il processo di migrazione di tutti gli altri componenti da Lync Server 2010 o da Office Communications Server 2007 R2.



Per requisiti di coesistenza specifici e altre informazioni dettagliate sulla coesistenza e la migrazione dei componenti di Lync Server 2010 o di Office Communications Server 2007 R2 e Lync Server 2013, vedere [Migrazione da Lync Server 2010 a Lync Server 2013](migration-from-lync-server-2010-to-lync-server-2013.md) e [Migrazione da Office Communications Server 2007 R2 a Lync Server 2013](migration-from-office-communications-server-2007-r2-to-lync-server-2013.md) nella documentazione relativa alla migrazione. Per informazioni dettagliate sul supporto della versione mista per i client, vedere [Client supportati dalle distribuzioni precedenti in Lync Server 2013](lync-server-2013-supported-clients-from-previous-deployments.md).

