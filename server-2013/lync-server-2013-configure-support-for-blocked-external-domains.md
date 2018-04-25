---
title: 'Lync Server 2013: Configurare il supporto per i domini esterni bloccati'
TOCTitle: Configurare il supporto per i domini esterni bloccati
ms:assetid: 49103138-e1ab-42bf-91aa-57cf23bbf260
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619176(v=OCS.15)
ms:contentKeyID: 49300442
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare il supporto per i domini esterni bloccati in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-08_

Se il supporto per i partner federati è configurato, è possibile gestire i domini ai quali impedire di federarsi con l'organizzazione. L'elenco dei domini bloccati svolgerà la funzione di elenco blocchi (elenco di una serie di voci esplicite da non consentire) e verrà applicato nell'individuazione di domini federati, se questa opzione è abilitata. Per informazioni dettagliate, vedere [Abilitare o disabilitare l'individuazione dei partner della federazione in Lync Server 2013](lync-server-2013-enable-or-disable-discovery-of-federation-partners.md).

Impedire a uno o più domini esterni di connettersi all'organizzazione. A tale scopo, aggiungere il dominio all'elenco dei domini bloccati.

## Per aggiungere un dominio esterno all'elenco dei domini bloccati

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Accesso utente esterno** .

4.  Fare clic su **Domini federati** , su **Nuovo** e quindi su **Dominio bloccato** .

5.  In **Nuovi domini federati** eseguire le operazioni seguenti:
    
      - In **Nome di dominio (o FQDN)** digitare il nome del dominio del partner federato che si desidera bloccare.
        

        > [!NOTE]
        > Il nome può essere costituito da un massimo di 256 caratteri.<BR>La ricerca in base al nome di dominio del partner federato si basa sulla corrispondenza del suffisso. Se ad esempio si digita <STRONG>contoso.com</STRONG> , la ricerca restituirà anche il dominio <STRONG>it.contoso.com</STRONG> .<BR>Un dominio di partner federato non può essere contemporaneamente bloccato e consentito. Questa eventualità non viene consentita da Lync Server 2013 perché non sia necessario sincronizzare gli elenchi.

    
      - (Facoltativo) In **Commento** digitare le informazioni che si desidera condividere con gli altri amministratori di sistema su questa configurazione.

6.  Fare clic su **Commit** .

7.  Ripetere i passaggi da 4 a 6 per ogni partner federato che si desidera bloccare.

Per consentire l'accesso degli utenti federati, è inoltre necessario abilitare il supporto per l'accesso degli utenti federati nell'organizzazione. Per informazioni dettagliate, vedere [Abilitare o disabilitare l'accesso degli utenti remoti in Lync Server 2013](lync-server-2013-enable-or-disable-remote-user-access.md).

È inoltre necessario configurare e applicare i criteri agli utenti per i quali si desidera consentire la collaborazione con gli utenti federati. Per informazioni dettagliate, vedere [Configurare criteri per controllare l'accesso utente federato in Lync Server 2013](lync-server-2013-configure-policies-to-control-federated-user-access.md).

