---
title: Configurare il Mediation Server
TOCTitle: Configurare il Mediation Server
ms:assetid: 583236fd-33cd-4045-81df-baa58ed07779
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204913(v=OCS.15)
ms:contentKeyID: 49300634
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare il Mediation Server

 

_**Ultima modifica dell'argomento:** 2012-09-28_

In questa procedura vengono illustrati i passaggi per configurare il pool Lync Server 2013 per l'uso del Mediation Server Lync Server 2013, anziché del Mediation Server Office Communications Server 2007 R2 legacy.

Per pubblicare, abilitare o disabilitare correttamente una topologia quando si aggiunge o si rimuove un ruolo del server, è necessario accedere come utente membro dei gruppi RTCUniversalServerAdmins e Domain Admins. È inoltre possibile delegare i diritti di amministratore e le autorizzazioni appropriate per l'aggiunta di ruoli del server. Per informazioni dettagliate, vedere Delegare autorizzazioni di installazione nella documentazione relativa alla distribuzione del server Standard Edition o Enterprise Edition. Per apportare altre modifiche relative alla configurazione è sufficiente appartenere al gruppo RTCUniversalServerAdmins.


> [!NOTE]
> Per informazioni aggiornate sulla ricerca di gateway PSTN, IP-PBX e servizi di trunking SIP pubblici qualificati che supportano le interazioni con Lync Server 2013, vedere "Programma di interoperabilità aperto per Microsoft Unified Communications" all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=206015">http://go.microsoft.com/fwlink/p/?linkId=206015</A>.



## Per configurare Mediation Server mediante il Generatore di topologie

1.  Apertura di una topologia esistente da Generatore di topologie

2.  Nel riquadro sinistro spostarsi su **Gateway PSTN** .

3.  Fare clic con il pulsante destro del mouse su **Gateway PSTN** e quindi scegliere **Nuovo gateway IP/PSTN** .

4.  Inserire le informazioni seguenti nella pagina **Definisci nuovo gateway IP/PSTN** :
    
      - Immettere il nome di dominio completo (FQDN) o l'indirizzo IP del gateway. Il nome di dominio completo (FQDN) del gateway è richiesto se il gateway usa il protocollo TLS.
    
      - Accettare il valore predefinito di **Porta di attesa per gateway IP/PSTN** o immettere la nuova porta di attesa, se è stata modificata.
    
      - Impostare il **Protocollo trasporto SIP** .

5.  Nel riquadro sinistro spostarsi su **Pool Enterprise Edition Front End** o **Server Standard** .

6.  Fare clic con il pulsante destro del mouse sul pool e quindi scegliere **Modifica proprietà** .

7.  In **Mediation Server** impostare le **Porte di attesa** .

8.  Quindi, associare il gateway PSTN creato selezionandolo e facendo clic su **Aggiungi** .

9.  In **Generatore di topologie** selezionare il nodo di primo livello **Lync Server** .

10. Nel menu **Azioni** selezionare **Pubblica topologia** e fare clic su **Avanti** .

11. Al termine della **Pubblicazione guidata** , fare clic su **Fine** per chiudere la procedura guidata.


> [!NOTE]
> È importante completare l'argomento successivo, <A href="change-voice-routes-to-use-the-new-lync-server-2013-mediation-server.md">Modificare le route vocali per l'utilizzo del nuovo Lync Server 2013 Mediation Server</A> per assicurarsi che le route vocali puntino al Mediation Server corretto.


