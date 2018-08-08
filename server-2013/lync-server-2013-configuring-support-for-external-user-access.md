---
title: "Lync Server 2013: Configura il supporto per accesso utenti esterni"
TOCTitle: Configurazione del supporto per l'accesso degli utenti esterni
ms:assetid: f8424f8c-f965-4414-8485-30f07e10214a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413051(v=OCS.15)
ms:contentKeyID: 49302530
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione del supporto per l'accesso degli utenti esterni in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

La distribuzione di un server perimetrale o di un pool di server perimetrali è il primo passaggio per il supporto degli utenti esterni. Per informazioni dettagliate sulla distribuzione di server perimetrali, vedere [Distribuzione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-deploying-external-user-access.md) nella documentazione relativa alla distribuzione. Per configurare i criteri, è necessario conoscere la precedenza dei criteri e come questi ultimi vengono applicati. Le impostazioni criteri di Lync Server applicate a un determinato livello di criteri possono sostituire le impostazioni applicate a un altro livello di criteri. La precedenza dei criteri di Lync Server è la seguente: i criteri utente (maggiore influenza) sostituiscono i criteri sito e i criteri sito sostituiscono i criteri globali (minore influenza). Ciò significa che maggiore è la prossimità dell'impostazione criteri all'oggetto su cui influiscono i criteri, maggiore è l'influenza su tale oggetto.

Dopo aver completato l'installazione di un server perimetrale o di un pool di server perimetrali, è necessario abilitare i tipi di accesso per gli utenti esterni che si desidera fornire e configurare le impostazioni per l'accesso esterno. In Lync Server 2013 abilitare e configurare l'accesso degli utenti esterni e i criteri utilizzando il Pannello di controllo di Lync Server, Lync Server Management Shell o entrambi, in base ai requisiti dell'attività.

Per supportare l'accesso utente esterno, è necessario eseguire entrambe le operazioni seguenti:

  - **Abilitare il supporto per l'organizzazione**   Per abilitare il supporto per l'accesso degli utenti esterni nella distribuzione, abilitare ogni tipo di accesso esterno che si desidera supportare. Abilitare e disabilitare il supporto per l'accesso degli utenti esterni modificando le impostazioni globali o creando e configurando criteri per siti o utenti nella pagina **Criteri di accesso esterno** nel gruppo **Federazione e accesso esterno** del Pannello di controllo di Lync Server o utilizzando Lync Server Management Shell e i cmdlet associati. È possibile trovare i cmdlet per gestire i **criteri di accesso esterno** nell'argomento [Cmdlet per la federazione e l'accesso esterno in Lync Server 2013](https://docs.microsoft.com/en-us/powershell/module/skype/). L'abilitazione del supporto per l'accesso esterno specifica che i server che eseguono Lync Server  servizio Access Edge supportano le comunicazioni con utenti e server esterni. Gli utenti interni ed esterni non possono comunicare quando l'accesso degli utenti esterni è disabilitato o non sono configurati criteri per supportarlo.

  - **Configurare e assegnare uno o più criteri**   Per supportare l'accesso degli utenti esterni, configurare i criteri necessari per soddisfare i requisiti, tra cui:
    
      - **Criteri di accesso esterno**    Creati con un ambito di sito o di utente (per impostazione predefinita, è presente un criterio globale con impostazioni disabilitate). Creare e configurare i criteri per controllare l'utilizzo di uno o più tipi di accesso degli utenti esterni, incluso l'accesso utente federato (tra cui i domini XMPP federati, se selezionati), l'accesso per utenti remoti e i provider di servizi di messaggistica istantanea pubblici. È possibile configurare i criteri esterni in Pannello di controllo di Lync Server utilizzando i criteri globali o uno o più criteri per sito e utente creati a livello amministrativo nella pagina **Criteri di accesso esterno** del gruppo **Federazione e accesso esterno** . Non è possibile eliminare i criteri globali. Creare e configurare qualsiasi criterio per siti o utenti che si desidera utilizzare per limitare l'accesso degli utenti esterni a siti o utenti specifici. I criteri globali e per i siti vengono assegnati automaticamente. Se si crea e configura un criterio per gli utenti, è necessario assegnarlo agli utenti specifici utilizzando la pagina di configurazione degli utenti nella pagina **Utenti** del Pannello di controllo di Lync Server. Individuare uno o più utenti a cui si desidera applicare il criterio e assegnare il criterio. Per assegnare a un utente un criterio utente configurato, vedere [Assegnare criteri di accesso per gli utenti esterni a un utente abilitato per Lync in Lync Server 2013](lync-server-2013-assign-an-external-user-access-policy-to-a-lync-enabled-user.md). Ogni criterio per l'accesso degli utenti esterni può supportare una o più delle opzioni seguenti: accesso utente remoto, accesso utente federato SIP, accesso utente federato XMPP e connettività di messaggistica istantanea pubblica.
    
      - **Criteri conferenza**   Creare e configurare i criteri per controllare le conferenze nell'organizzazione, inclusi i criteri relativi agli utenti dell'organizzazione che possono invitare utenti anonimi alle conferenze che ospitano. Nella pagina **Servizio di conferenza** di Pannello di controllo di Lync Server sono disponibili le impostazioni dei criteri con ambito globale, di sito e utente che controllano le impostazioni per le conferenze. Per informazioni dettagliate, vedere [Gestione di riunioni e conferenze in Lync Server 2013](lync-server-2013-managing-meetings-and-conferences.md). Nella pagina **Configurazione Access Edge** abilitare gli utenti anonimi, gli utenti remoti e gli utenti federati per i servizi di conferenza. I criteri nella pagina **Configurazione Access Edge** sono di ambito globale. Non sono presenti opzioni per definire criteri per siti o utenti. Controllare l'ambito nella pagina **Criteri di accesso esterno** mediante l'utilizzo delle impostazioni per i criteri di ambito globale, sito o utente.
        
        Se ad esempio si desidera consentire agli utenti di creare, invitare e gestire i servizi di conferenza con utenti remoti, impostare **Abilita comunicazioni con utenti remoti** nei criteri globali, di sito o utente **Criteri di accesso esterno** e **Abilita comunicazioni con utenti remoti** nella pagina **Configurazione Access Edge** . Analogamente, per consentire i servizi di conferenza con utenti anonimi o partner federati con cui è stata definita una relazione (ad esempio, provider e domini SIP federati configurati; la federazione di XMPP non supporta il servizio di conferenza), impostare **Abilita comunicazioni con utenti pubblici** e **Abilita comunicazioni con utenti federati** nei criteri globali, di sito o utente **Criteri di accesso esterno** . Selezionare quindi le impostazioni opzionali dei criteri globali **Abilita accesso utente anonimo per le conferenze** e **Abilita federazione e connettività di messaggistica istantanea pubblica** nella pagina **Configurazione Access Edge** .

È possibile configurare le impostazioni dell'accesso degli utenti esterni, inclusi eventuali criteri che si desidera utilizzare per controllare l'accesso degli utenti esterni, anche se per l'organizzazione non è stato abilitato l'accesso degli utenti esterni. I criteri e le altre impostazioni configurati tuttavia diventano effettivi solo quando si abilita per l'organizzazione l'accesso degli utenti esterni. Gli utenti esterni non possono comunicare con gli utenti dell'organizzazione se l'accesso degli utenti esterni è disabilitato o se non sono configurati criteri di accesso degli utenti esterni per supportarlo.

La distribuzione di server perimetrali autentica i tipi di utenti esterni (ad eccezione degli utenti anonimi che vengono autenticati dall'ID conferenza e da una passkey inviata al partecipante anonimo quando si crea la conferenza e si invitano i partecipanti) e controlla l'accesso in base alla configurazione del supporto dei server perimetrali. Per controllare le comunicazioni, è possibile configurare uno o più criteri nonché impostazioni che definiscono il modo in cui gli utenti all'interno e all'esterno del firewall comunicano tra loro. I criteri e le impostazioni includono il criterio globale predefinito per l'accesso degli utenti esterni, oltre ai criteri sito e utente che è possibile creare e configurare per abilitare uno o più tipi di accesso degli utenti esterni per siti o utenti specifici.

## Argomenti della sezione

  - [Configurare criteri per controllare l'accesso degli utenti remoti in Lync Server 2013](lync-server-2013-configure-policies-to-control-remote-user-access.md)

  - [Abilitare o disabilitare l'accesso degli utenti remoti in Lync Server 2013](lync-server-2013-enable-or-disable-remote-user-access.md)

  - [Abilitare o disabilitare l'accesso degli utenti anonimi in Lync Server 2013](lync-server-2013-enable-or-disable-anonymous-user-access.md)

  - [Assegnare i criteri di conferenza per supportare gli utenti anonimi in Lync Server 2013](lync-server-2013-assign-conferencing-policies-to-support-anonymous-users.md)

