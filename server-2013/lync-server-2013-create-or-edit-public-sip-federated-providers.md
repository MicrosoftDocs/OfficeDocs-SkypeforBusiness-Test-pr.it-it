---
title: 'Lync Server 2013: Creare o modificare provider federati SIP pubblici'
TOCTitle: Creare o modificare provider federati SIP pubblici
ms:assetid: 5321598c-1ab1-40e3-b739-4b2e6d0a3a3b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398349(v=OCS.15)
ms:contentKeyID: 49300532
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare provider federati SIP pubblici in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-19_

La connettività di messaggistica istantanea pubblica consente agli utenti dell'organizzazione di usare la messaggistica istantanea per comunicare con utenti di servizi di messaggistica istantanea forniti da provider di servizi di messaggistica istantanea pubblica, inclusi Windows Live Messenger, Yahoo\! e AOL.

Lync Server 2013 dispone di configurazioni di provider pubblico per la messaggistica istantanea di America Online, Windows Live e Yahoo\!. Ogni provider pubblico è configurato con il nome di dominio completo del server perimetrale del provider e il livello di verifica predefinito **Consenti agli utenti di comunicare solo con le persone incluse nell'elenco Contatti che usano questo provider** .

Per impostazione predefinita, nessuno dei provider pubblici è abilitato. Prima di abilitare i provider pubblici è necessario eseguire le attività relative al contratto di licenza e al provisioning. È possibile abilitare i provider prima di aver completato queste attività, ma gli utenti potranno comunicare con i contatti all'interno dei provider solo dopo il completamento delle attività prerequisite. Per informazioni dettagliate sulla gestione delle licenze e il provisioning di provider pubblici, vedere [Configurare criteri per controllare l'accesso degli utenti pubblici in Lync Server 2013](lync-server-2013-configure-policies-to-control-public-user-access.md).

Per creare o modificare provider pubblici, eseguire la procedura seguente:

## Per creare o modificare provider pubblici:

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Federazione e accesso esterno** e quindi su **Provider federati SIP** .

4.  Se è necessario creare un nuovo provider pubblico, fare clic su **Nuovo** e quindi su **Provider pubblico** .

5.  Se è necessario modificare una voce dell'elenco di provider pubblici, selezionare un provider pubblico, fare clic su **Modifica** e quindi su **Mostra dettagli** .

6.  Nella pagina **Modifica Provider federato SIP** è possibile digitare o modificare le impostazioni seguenti:
    
      - **Abilita comunicazioni con questo provider**    Se si seleziona questa impostazione, si abilita la messaggistica istantanea con gli utenti del provider specificato.
    
      - **Nome provider:**    Proprietà obbligatoria. Digitare il nome del provider, che verrà riportato nell'elenco dei provider federati SIP.
    
      - **Servizio Access Edge (FQDN):**    Proprietà obbligatoria. Digitare il nome di dominio completo del servizio Access Edge del provider che si sta configurando. Per questa impostazione viene fornito un valore predefinito, che deve essere modificato solo se il provider pubblico modifica il proprio FQDN del servizio Access Edge.
    
      - **Livello di verifica predefinito:**    L'impostazione predefinita, **Consenti agli utenti di comunicare solo con le persone incluse nell'elenco Contatti che usano questo provider** consente di comunicare solo con i contatti accettati e presenti nell'elenco contatti.
        
        Se si seleziona **Consenti agli utenti di comunicare con chiunque usi questo provider** rimuove la limitazione di dover ricevere e accettare l'invito di un contatto. Questa impostazione non impone limiti sugli utenti della rete del provider pubblico da cui si può essere contattati.

7.  Al termine della configurazione delle impostazioni, fare clic su **Commit** per salvare o su **Annulla** per annullare le modifiche.

## Vedere anche

#### Attività

[Configurare criteri per controllare l'accesso degli utenti pubblici in Lync Server 2013](lync-server-2013-configure-policies-to-control-public-user-access.md)  
[Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica in Lync Server 2013](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md)

