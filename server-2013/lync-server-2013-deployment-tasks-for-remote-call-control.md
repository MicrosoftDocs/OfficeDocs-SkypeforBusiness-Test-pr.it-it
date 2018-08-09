---
title: "Lync Server 2013: Attività di distribuz. per controllo chiamate remote"
TOCTitle: Attività di distribuzione per il controllo delle chiamate remote
ms:assetid: 20218871-4f27-4611-9b7e-c0ca55908284
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558624(v=OCS.15)
ms:contentKeyID: 49299895
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Attività di distribuzione per il controllo delle chiamate remote in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-05_

In questo argomento vengono descritte le attività di distribuzione che è necessario eseguire per abilitare il controllo delle chiamate remote per gli utenti nell'ambiente Lync Server.


> [!NOTE]
> Se si esegue la migrazione di utenti precedentemente abilitati per il controllo delle chiamate remote in Microsoft Office Communicator 2007 R2, è necessario eseguire un'attività di distribuzione aggiuntiva prima di effettuare le attività di distribuzione del controllo delle chiamate remote descritte in questo argomento. Durante il processo di migrazione a Lync Server, è necessario rimuovere le voci di applicazioni attendibili (precedentemente note come <EM>voci di host autorizzati</EM> ) utilizzando gli strumenti di amministrazione di Office Communications Server 2007 R2, secondo necessità.<BR>Per informazioni dettagliate sulla rimozione di host autorizzati, vedere <A href="lync-server-2013-remove-a-legacy-authorized-host-optional.md">Rimuovere un host autorizzato legacy in Lync Server 2013 (facoltativo)</A>.



## Passaggio 1: installare e configurare il gateway SIP/CSTA per comunicare con un PBX

È necessario installare almeno un gateway SIP/CSTA in grado di connettersi sia a Lync Server che al centralino (PBX) esistente nell'ambiente per offrire agli utenti funzionalità di controllo delle chiamate remote. Un gateway SIP/CSTA è un gateway tra SIP e CSTA (Computer-Supported Telecommunications Application). Indipendentemente dal numero di gateway installati, ogni utente può essere configurato con un solo gateway o PBX. Se il PBX esistente non dispone di un'interfaccia SIP/CSTA, distribuire un gateway SIP/CSTA in grado di supportare il PBX, incluso il supporto per protocolli di segnalazione specifici del fornitore del PBX proprietario. Per informazioni dettagliate sulle funzionalità, rivolgersi direttamente al fornitore.

Quando si è pronti per distribuire un gateway SIP/CSTA in grado di integrarsi con Lync Server per il controllo delle chiamate remote, rivolgersi anche al fornitore del gateway oppure consultare la relativa documentazione per informazioni sulla sintassi richiesta dal gateway per le informazioni seguenti:

  - URI server linea del gateway

  - URI di linea per gli utenti che verranno assegnati al gateway

Le impostazioni precedenti sono necessarie durante la configurazione utente e devono essere specificate come previsto dal gateway per eseguire correttamente il routing e la connessione al PBX.

È possibile utilizzare come riferimento i fornitori indicati nel sito Web Microsoft Unified Communications Open Interoperability Program, all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=203309](http://go.microsoft.com/fwlink/p/?linkid=203309).

## Passaggio 2: configurare Lync Server per instradare le richieste CSTA al gateway SIP/CSTA

È necessario creare route statiche nei pool di Lync Server per l'indirizzo di destinazione (URI server) di tutti i gateway SIP/CSTA della distribuzione a cui si desidera instradare richieste di controllo delle chiamate remote. È inoltre necessario creare una voce di applicazione attendibile corrispondente a ogni indirizzo di destinazione. Quando viene designato come applicazione attendibile, il gateway acquisisce lo stato di attendibile per l'esecuzione nell'ambiente Lync Server, anche se è stato sviluppato da terze parti e viene eseguito come *servizio esterno* perché non incorporato nel prodotto. Se infine Lync Server si connette al gateway SIP/CSTA utilizzando una connessione TCP (Transmission Control Protocol) anziché una connessione TLS (Transport Layer Security), sarà necessario anche definire l'indirizzo IP del gateway utilizzando Generatore di topologie.

Per informazioni dettagliate sulla configurazione di route statiche, vedere [Configurare una route statica per il controllo delle chiamate remote in Lync Server 2013](lync-server-2013-configure-a-static-route-for-remote-call-control.md).

Per informazioni dettagliate sulla configurazione di voci di applicazioni attendibili, vedere [Configurare una voce applicazione attendibile per il controllo delle chiamate remote in Lync Server 2013](lync-server-2013-configure-a-trusted-application-entry-for-remote-call-control.md).

Per informazioni dettagliate sulla definizione di un indirizzo IP di un gateway SIP/CSTA in Generatore di topologie, vedere [Definire l'indirizzo IP di un gateway SIP/CSTA in Lync Server 2013](lync-server-2013-define-a-sip-csta-gateway-ip-address.md).

## Passaggio 3: configurare gli utenti di Lync per il controllo delle chiamate remote

Dopo che gli utenti sono stati abilitati per Lync Server, è possibile utilizzare il Pannello di controllo di Lync Server o Lync Server Management Shell per abilitarli per il controllo delle chiamate remote. Durante questo passaggio di distribuzione si assegna a ogni utente in URI server linea e un URI di linea. L'URI server linea è l'URI SIP del gateway SIP/CSTA che si intende assegnare all'utente. L'URI di linea è il numero di telefono univoco assegnato all'utente.

Per informazioni dettagliate sulla configurazione degli utenti per il controllo delle chiamate remote, vedere [Abilitare gli utenti di Lync per il controllo delle chiamate remote in Lync Server 2013](lync-server-2013-enable-lync-users-for-remote-call-control.md).

## Passaggio 4: definire le regole di normalizzazione dei numeri di telefono di Lync Server

Negli scenari di controllo delle chiamate remote Lync Server utilizza le regole di normalizzazione dei numeri di telefono per convertire i numeri di telefono che riceve dal gateway SIP/CSTA nel formato E.164. I numeri di telefono devono essere in questo formato standardizzato per garantire il corretto funzionamento di alcune funzionalità di controllo delle chiamate remote. Il controllo delle chiamate remote utilizza le stesse regole di normalizzazione dei numeri di telefono configurate per la normalizzazione dei numeri di telefono del servizio Rubrica, che sono diverse da quelle utilizzate per VoIP aziendale.

Per informazioni dettagliate sull'utilizzo delle regole di normalizzazione dei numeri di telefono da parte del controllo delle chiamate remote, vedere [Controllo delle chiamate remote e normalizzazione dei numeri di telefono in Lync Server 2013](lync-server-2013-remote-call-control-and-phone-number-normalization.md). Per informazioni dettagliate sulle regole di normalizzazione dei numeri di telefono, vedere [Amministrazione del servizio Rubrica in Lync Server 2013](lync-server-2013-administering-the-address-book-service.md) nella documentazione relativa alle operazioni.

