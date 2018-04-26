---
title: 'Lync Server 2013: Creare o modificare provider federati SIP ospitati'
TOCTitle: Creare o modificare provider federati SIP ospitati
ms:assetid: 0dd6dcb6-a88d-46b8-9c96-b35967309bcd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ552445(v=OCS.15)
ms:contentKeyID: 49299674
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare provider federati SIP ospitati in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-19_

La connettività di messaggistica istantanea con provider ospitato consente agli utenti dell'organizzazione di utilizzare la messaggistica istantanea per comunicare gli utenti dei servizi di messaggistica istantanea forniti dai provider ospitati, tra cui Microsoft Office 365 e Lync Online.

Ogni provider ospitato è configurato con il nome di dominio completo del server perimetrale del provider e il livello di verifica predefinito **Consenti agli utenti di comunicare solo con le persone incluse nell'elenco Contatti che usano questo provider** .

Per creare o modificare provider gestiti, eseguire la procedura seguente:

## Per creare o modificare provider gestiti

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Federazione e accesso esterno** e quindi su **Provider federati SIP** .

4.  Se è necessario creare un nuovo provider ospitato fare clic su **Nuovo** e quindi su **Provider ospitato** .

5.  Se è necessario modificare una voce nell'elenco di provider ospitati, selezionare un provider ospitato, fare clic su **Modifica** e quindi su **Mostra dettagli** .

6.  Nella pagina **Modifica Provider federato SIP** è possibile digitare o modificare le impostazioni seguenti:
    
      - **Abilita comunicazioni con questo provider**    Questa impostazione abilita le comunicazioni con gli utenti del provider.
    
      - **Nome provider:**    Proprietà obbligatoria. Digitare il nome del provider, che verrà riportato nell'elenco dei provider federati SIP.
    
      - **Servizio Access Edge (FQDN)**    Si tratta di una proprietà obbligatoria. Digitare il nome di dominio completo del servizio Access Edge del provider ospitato che si sta configurando. Queste informazioni deve essere fornite dal provider ospitato e devono essere modificate solo in caso di modifica del nome di dominio completo (FQDN) del servizio Access Edge presso il provider ospitato.
    
      - **Livello di verifica predefinito:**    L'impostazione predefinita, **Consenti agli utenti di comunicare solo con le persone incluse nell'elenco Contatti che usano questo provider** consente di comunicare solo con i contatti accettati e presenti nell'elenco contatti.
        
        Se si seleziona **Consenti agli utenti di comunicare con chiunque usi questo provider** , viene rimossa la limitazione che prevede che sia stato ricevuto e accettato un invito di contatto. Questa impostazione non limita gli utenti dai quali è possibile essere contattati dalla rete del provider ospitato.

7.  Al termine della configurazione delle impostazioni, fare clic su **Commit** per salvare o su **Annulla** per annullare le modifiche.

## Vedere anche

#### Attività

[Configurare criteri per controllare l'accesso degli utenti pubblici in Lync Server 2013](lync-server-2013-configure-policies-to-control-public-user-access.md)  
[Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica in Lync Server 2013](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md)

