---
title: Applicazione di criteri di archiviazione di Lync Server a un utente
TOCTitle: Applicazione di criteri di archiviazione di Lync Server a un utente
ms:assetid: a23e4876-aa8d-4f49-a3bd-3696616e8290
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205143(v=OCS.15)
ms:contentKeyID: 49301529
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Applicazione di criteri di archiviazione di Lync Server a un utente

 

_**Ultima modifica dell'argomento:** 2012-10-10_

Dopo avere creato criteri utente di Lync Server, è necessario applicarli a utenti o gruppi di utenti specifici che si trovano in Lync Server 2013 prima che possano avere effetto. Per informazioni dettagliate sulla creazione di criteri utente per utenti specifici, vedere [Creazione e configurazione dei criteri utente per l'archiviazione in Lync Server](lync-server-2013-creating-and-configuring-user-policies-for-archiving-in-lync-server.md) nella documentazione relativa alla distribuzione.

Per informazioni dettagliate sul funzionamento dei criteri di archiviazione, inclusa la gerarchia dei criteri globali, del sito e dell'utente, vedere [Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md) nella documentazione relativa alla pianificazione, alla distribuzione o alle operazioni.


> [!NOTE]
> Per configurare e utilizzare l'archiviazione, è innanzitutto necessario distribuire l'archiviazione. Per informazioni dettagliate, vedere <A href="lync-server-2013-deploying-archiving.md">Distribuzione dell'archiviazione in Lync Server 2013</A> nella documentazione relativa alla distribuzione.<BR>Se è stata abilitata l'integrazione di Microsoft Exchange per la distribuzione in uso, i criteri di archiviazione sul posto di Exchange controllano se l'archiviazione è abilitata per gli utenti disponibili in Exchange 2013 le cui cassette postali sono in archiviazione sul posto. Per informazioni dettagliate, vedere <A href="lync-server-2013-setting-up-policies-for-archiving-when-using-exchange-server-integration.md">Configurazione dei criteri per l'archiviazione in caso di utilizzo dell'integrazione di Exchange Server</A> nella documentazione relativa alla distribuzione.<BR>Specificare tutte le opzioni appropriate nelle configurazioni di archiviazione prima di abilitare l'archiviazione. Per informazioni dettagliate, vedere <A href="lync-server-2013-configuring-archiving-options.md">Configurazione delle opzioni di archiviazione</A> nella documentazione relativa alla distribuzione.



## Per applicare criteri di archiviazione di Lync Server a un utente

1.  Da un account utente assegnato al ruolo CsArchivingAdministrator o CsAdministrator, eseguire l'accesso a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server 2013. Per informazioni dettagliate sui diversi metodi che è possibile utilizzare per avviare il Pannello di controllo di Lync Server 2013, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Utenti** e quindi ricercare l'account utente che si desidera configurare.

4.  Nella tabella in cui sono elencati i risultati della ricerca fare clic sull'account utente, su **Modifica** e quindi su **Mostra dettagli**.

5.  In **Modifica utente di Lync Server**, in **Criteri di archiviazione**, selezionare i criteri di archiviazione che si desidera applicare.
    

    > [!NOTE]
    > L'impostazione <STRONG>&lt;Automatici&gt;</STRONG> consente di applicare le impostazioni di installazione del server predefinite. Queste impostazioni vengono applicate automaticamente dal server.



6.  Fare clic su **Commit**.

