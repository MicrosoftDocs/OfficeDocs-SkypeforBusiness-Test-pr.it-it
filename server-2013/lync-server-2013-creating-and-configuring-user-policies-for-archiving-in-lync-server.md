---
title: Creazione e configurazione dei criteri utente per l'archiviazione in Lync Server
TOCTitle: Creazione e configurazione dei criteri utente per l'archiviazione in Lync Server
ms:assetid: 5af0e605-3563-4d6f-a3c6-511d204a3165
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204923(v=OCS.15)
ms:contentKeyID: 49300679
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creazione e configurazione dei criteri utente per l'archiviazione in Lync Server

 

_**Ultima modifica dell'argomento:** 2012-10-09_

Per abilitare o disabilitare l'archiviazione per utenti specifici ospitati in Lync Server, è innanzitutto necessario creare criteri utente e quindi applicare tali criteri a uno o più utenti o gruppi di utenti. Per informazioni dettagliate sull'applicazione di criteri utente a utenti e gruppi di utenti specifici, vedere [Applicazione di criteri di archiviazione di Lync Server a un utente](lync-server-2013-applying-a-lync-server-archiving-policy-to-a-user.md) nella documentazione relativa alla distribuzione.

Per informazioni dettagliate sul funzionamento dei criteri di archiviazione, inclusa la gerarchia per i criteri globali, del sito e degli utenti, vedere [Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md) nella documentazione relativa alla pianificazione, alla distribuzione o alle operazioni.


> [!NOTE]
> Se per la distribuzione viene abilitata l'integrazione di Microsoft Exchange, i criteri di archiviazione sul posto di Exchange determinano se l'archiviazione è abilitata per gli utenti ospitati in Exchange 2013 con cassette postali impostate per l'archiviazione sul posto. Per informazioni dettagliate, vedere <A href="lync-server-2013-setting-up-policies-for-archiving-when-using-exchange-server-integration.md">Configurazione dei criteri per l'archiviazione in caso di utilizzo dell'integrazione di Exchange Server</A> nella documentazione relativa alla distribuzione.<BR>Prima di abilitare l'archiviazione, è necessario specificare tutte le opzioni appropriate nelle configurazioni di archiviazione. Per informazioni dettagliate, vedere <A href="lync-server-2013-configuring-archiving-options.md">Configurazione delle opzioni di archiviazione</A> nella documentazione relativa alla distribuzione.



## Per configurare i criteri di archiviazione per gli utenti ospitati in Lync Server

1.  Da un account utente assegnato al ruolo CsArchivingAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server 2013. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server 2013, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di navigazione di sinistra fare clic su **Monitoraggio e archiviazione**, quindi scegliere **Criteri di archiviazione**.

4.  Fare clic su **Nuovo** e quindi su **Criteri utente**.

5.  In **Nuovi criteri di archiviazione** eseguire le operazioni seguenti:
    
      - In **Nome** specificare un nome per i criteri utente.
    
      - In **Descrizione** immettere informazioni sugli scopi dei criteri utente, ad esempio "Criteri utente per il reparto legale".
    
      - Per controllare l'archiviazione delle comunicazioni interne per i criteri utente, selezionare o deselezionare la casella di controllo **Archivia comunicazioni interne**.
    
      - Per controllare l'archiviazione delle comunicazioni esterne per i criteri utente, selezionare o deselezionare la casella di controllo **Archivia comunicazioni esterne**.

6.  Fare clic su **Commit**.

I criteri utente si applicano solo agli utenti a cui vengono assegnati. Per informazioni dettagliate sull'applicazione di criteri utente a utenti specifici, vedere [Applicazione di criteri di archiviazione di Lync Server a un utente](lync-server-2013-applying-a-lync-server-archiving-policy-to-a-user.md) nella documentazione relativa alla distribuzione.

