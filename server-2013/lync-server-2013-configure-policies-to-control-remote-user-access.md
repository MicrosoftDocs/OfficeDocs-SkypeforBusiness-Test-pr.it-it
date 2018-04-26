---
title: "Lync Server 2013: Configurare criteri per controllare l'accesso degli utenti remoti"
TOCTitle: Configurare criteri per controllare l'accesso degli utenti remoti
ms:assetid: 8f556849-692b-44a0-9514-4468fc9a39d0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398725(v=OCS.15)
ms:contentKeyID: 49301304
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare criteri per controllare l'accesso degli utenti remoti in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-18_

È necessario configurare uno o più criteri di accesso utente esterno per controllare se gli utenti esterni possono collaborare con gli utenti di Lync Server interni. Per controllare l'accesso degli utenti remoti è possibile configurare criteri a livello globale, di sito e di utente. I criteri a livello di sito hanno la priorità sui criteri globali e i criteri utente hanno la priorità sui criteri a livello di sito e globali. Per informazioni dettagliate sui tipi di criteri che è possibile configurare, vedere [Gestione della federazione e dell'accesso esterno a Lync Server 2013](lync-server-2013-managing-federation-and-external-access-to-lync-server-2013.md). Le impostazioni criteri di Lync Server applicate a un determinato livello di criteri possono sostituire le impostazioni applicate a un altro livello di criteri. La precedenza dei criteri di Lync Server è la seguente: i criteri utente (maggiore influenza) sostituiscono i criteri sito e i criteri sito sostituiscono i criteri globali (minore influenza). Ciò significa che maggiore è la prossimità dell'impostazione criteri all'oggetto su cui influiscono i criteri, maggiore è l'influenza su tale oggetto.


> [!NOTE]
> È possibile configurare criteri per il controllo dell'accesso degli utenti remoti anche se non si è abilitato l'accesso utente remoto per l'organizzazione. I criteri configurati, tuttavia, verranno applicati solo dopo l'abilitazione dell'accesso utente remoto per l'organizzazione. Per informazioni dettagliate sull'abilitazione dell'accesso utente remoto, vedere <A href="lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md">Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica in Lync Server 2013</A>. Se inoltre si specifica un criterio utente per il controllo dell'accesso utente remoto, il criterio verrà applicato solo agli utenti abilitati per Lync Server e configurati per l'utilizzo del criterio. Per informazioni dettagliate su come specificare gli utenti autorizzati ad accedere a Lync Server da posizioni remote, vedere <A href="lync-server-2013-assign-an-external-user-access-policy-to-a-lync-enabled-user.md">Assegnare criteri di accesso per gli utenti esterni a un utente abilitato per Lync in Lync Server 2013</A> nella documentazione relativa alla distribuzione o nella documentazione relativa alle operazioni.



Eseguire la procedura seguente per configurare ogni criterio di accesso esterno che si desidera utilizzare per controllare l'accesso degli utenti remoti.


> [!NOTE]
> Questa procedura descrive come configurare un criterio solo per abilitare le comunicazioni con gli utenti remoti, ma qualsiasi criterio configurato per il supporto dell'accesso utente remoto può configurare anche l'accesso degli utenti federati e l'accesso degli utenti pubblici. Per informazioni dettagliate sulla configurazione di criteri per il supporto degli utenti federati, vedere <A href="lync-server-2013-configure-policies-to-control-federated-user-access.md">Configurare criteri per controllare l'accesso utente federato in Lync Server 2013</A>. Per informazioni dettagliate sulla configurazione di criteri per il supporto degli utenti pubblici, vedere <A href="lync-server-2013-create-or-edit-public-sip-federated-providers.md">Creare o modificare provider federati SIP pubblici in Lync Server 2013</A>.



## Per configurare un criterio di accesso esterno per il supporto dell'accesso utente remoto

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Accesso utente esterno** e quindi su **Criteri di accesso esterno** .

4.  Nella pagina **Criteri di accesso esterno** eseguire una delle operazioni seguenti:
    
      - Per configurare il criterio globale per il supporto dell'accesso utente remoto, fare clic sul criterio globale, su **Modifica** e quindi su **Mostra dettagli** .
    
      - Per creare nuovi criteri di sito, fare clic su **Nuovo** e quindi su **Criteri sito** . In **Seleziona un sito** fare clic sul sito appropriato nell'elenco e quindi fare clic su **OK** .
    
      - Per creare nuovi criteri utente, fare clic su **Nuovo** e quindi su **Criteri utente** . In **Nuovi criteri di accesso esterno** creare un nome univoco nel campo **Nome** che indichi lo scopo del criterio, ad esempio **AbilitaUtentiRemoti** per un criterio utente che abilita le comunicazioni per gli utenti remoti.
    
      - Per modificare criteri esistenti, fare clic sui criteri appropriati indicati nella tabella, fare clic su **Modifica** e quindi fare clic su **Mostra dettagli** .

5.  (Facoltativo) Se si desidera aggiungere o modificare una descrizione, specificare le informazioni per i criteri in **Descrizione** .

6.  Eseguire una delle operazioni seguenti:
    
      - Per abilitare l'accesso utente remoto per il criterio, selezionare la casella di controllo **Abilita comunicazioni con utenti remoti** .
    
      - Per disabilitare l'accesso utente remoto per il criterio, deselezionare la casella di controllo **Abilita comunicazioni con utenti remoti** .

7.  Fare clic su **Commit** .

Per abilitare l'accesso utente remoto è necessario abilitare anche il supporto dell'accesso utente remoto nell'organizzazione. Per informazioni dettagliate, vedere [Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica in Lync Server 2013](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md) nella documentazione relativa alla distribuzione o nella documentazione relativa alle operazioni.

Se si tratta di un criterio utente è inoltre necessario applicare il criterio agli utenti ai quali si desidera consentire di effettuare l'accesso in remoto. Per informazioni dettagliate, vedere [Assegnare criteri di accesso per gli utenti esterni a un utente abilitato per Lync in Lync Server 2013](lync-server-2013-assign-an-external-user-access-policy-to-a-lync-enabled-user.md) nella documentazione relativa alla distribuzione o nella documentazione relativa alle operazioni.

