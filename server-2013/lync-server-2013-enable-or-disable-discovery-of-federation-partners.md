---
title: "Lync Server 2013: Abilitare o disabilitare l'individuazione dei partner della federazione"
TOCTitle: Abilitare o disabilitare l'individuazione dei partner della federazione
ms:assetid: 91fd036b-b1af-47cf-b1cf-0aa0a783c2aa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182550(v=OCS.15)
ms:contentKeyID: 49301333
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare o disabilitare l'individuazione dei partner della federazione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Al momento della distribuzione degli Edge Server e dell'abilitazione della federazione per l'organizzazione, dovrebbe essere stato specificato se supportare l'individuazione automatica dei domini partner federati. Utilizzare la procedura descritta in questo argomento per modificare tale configurazione.


> [!NOTE]
> Nella procedura che segue si presuppone che sia stata già abilitata la federazione per l'organizzazione. Per informazioni dettagliate sull'abilitazione della federazione, vedere <A href="lync-server-2013-enable-or-disable-remote-user-access.md">Abilitare o disabilitare l'accesso degli utenti remoti in Lync Server 2013</A> nella documentazione relativa alla distribuzione o alle operazioni.



## Per abilitare o disabilitare l'individuazione automatica dei domini federati per l'organizzazione

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Accesso utente esterno** e su **Configurazione Access Edge** .

4.  Nella pagina **Configurazione Access Edge** fare clic su **Globale** , fare clic su **Modifica** e quindi su **Mostra dettagli** .

5.  In **Modifica configurazione Access Edge** , in **Abilita comunicazioni con utenti federati** selezionare o deselezionare la casella di controllo **Abilita individuazione dominio partner** per abilitare o disabilitare l'individuazione automatica dei domini partner.

6.  Fare clic su **Commit** .

Per consentire agli utenti federati di collaborare con gli utenti della distribuzione di Lync Server, è anche necessario aver configurato almeno un criterio di accesso esterno per il supporto dell'accesso degli utenti federati. Per informazioni dettagliate, vedere [Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica in Lync Server 2013](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md) nella documentazione relativa alla distribuzione o alle operazioni. Per informazioni dettagliate sul controllo dell'accesso per domini federati specifici, vedere [Gestire i domini federati SIP per l'organizzazione in Lync Server 2013](lync-server-2013-manage-sip-federated-domains-for-your-organization.md), [Gestire i provider federati SIP per l'organizzazione in Lync Server 2013](lync-server-2013-manage-sip-federated-providers-for-your-organization.md) and [Gestire i partner federati XMPP per l'organizzazione in Lync Server 2013](lync-server-2013-manage-xmpp-federated-partners-for-your-organization.md) nella documentazione relativa alla distribuzione o alle operazioni.

## Abilitazione o disabilitazione dell'individuazione dei partner di federazione tramite i cmdlet di Windows PowerShell

L'individuazione dei partner di federazione può essere gestita mediante Windows PowerShell e il cmdlet Set-CsAccessEdgeConfiguration. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per abilitare l'individuazione dei partner federati

  - Per abilitare l'individuazione dei partner federati, impostare il valore della proprietà **EnablePartnerDiscovery** su True ($True). Tenere presente che è necessario abilitare l'instradamento DNS SRV per modificare il valore di questa proprietà.
    
        Set-CsAccessEdgeConfiguration -UseDnsSrvRouting -EnablePartnerDiscovery $True

## Per disabilitare l'individuazione dei partner federati

  - Per disabilitare l'individuazione dei partner federati, impostare il valore della proprietà **EnablePartnerDiscovery** su False ($False).
    
        Set-CsAccessEdgeConfiguration -UseDnsSrvRouting -EnablePartnerDiscovery $False

