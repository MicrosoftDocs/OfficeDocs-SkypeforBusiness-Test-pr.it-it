---
title: "Lync Server 2013: Componenti necessari per l'accesso degli utenti esterni"
TOCTitle: Componenti necessari per l'accesso degli utenti esterni
ms:assetid: 2d0f9817-14e7-4109-95dc-62420e3c29e2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425779(v=OCS.15)
ms:contentKeyID: 49300047
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Componenti necessari per l'accesso degli utenti esterni in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-05-29_

La maggior parte dei componenti perimetrali viene distribuita in una rete perimetrale. I componenti riportati di seguito costituiscono la topologia perimetrale della rete perimetrale. Se non indicato altrimenti, i componenti fanno parte degli [Scenari per l'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-scenarios-for-external-user-access.md) e si trovano nella rete perimetrale. I componenti perimetrali includono:

  - server perimetrali

  - Proxy inversi

  - Firewall

  - Director (facoltativi e ubicati logicamente nella rete interna)

  - Bilanciamento del carico di tipo per topologie perimetrali con scalabilità implementata (bilanciamento del carico DNS o dispositivo di bilanciamento del carico hardware)
    
    > [!IMPORTANT]  
    > Non è possibile usare il bilanciamento del carico DNS in un'interfaccia e il bilanciamento del carico hardware in un'altra. È necessario usare lo stesso tipo di bilanciamento del carico per entrambe le interfacce, in quanto non è supportata una combinazione dei due tipi.

## server perimetrali

I server perimetrali inviano e ricevono il traffico di rete per i servizi offerti dalla distribuzione interna eseguita dagli utenti esterni. Il server perimetrale esegue i servizi seguenti:

  - **Servizio Access Edge**   Questo servizio fornisce un singolo punto di connessione attendibile per il traffico SIP (Session Initiation Protocol) sia in ingresso che in uscita.

  - **Servizio Web Conferencing Edge**   Questo servizio consente agli utenti esterni di partecipare alle riunioni ospitate nella distribuzione di Lync Server 2013 interna.

  - **Servizio A/V Edge**   Questo servizio mette a disposizione degli utenti esterni funzionalità audio, video, di condivisione applicazioni e di trasferimento di file. Gli utenti possono aggiungere le funzionalità audio e video alle riunioni a cui partecipano utenti esterni, nonché comunicare usando audio e video direttamente con un utente esterno nelle sessioni point-to-point. Il servizio A/V Edge offre inoltre il supporto per la condivisione desktop e il trasferimento di file.

  - **Servizio proxy XMPP**   Il servizio proxy XMPP accetta e invia messaggi XMPP (Extensible Messaging and Presence Protocol) da e a partner federati XMPP configurati.

Gli utenti esterni autorizzati possono accedere ai server perimetrali per connettersi alla distribuzione di Lync Server 2013 interna, ma i server perimetrali non offrono altro accesso alla rete interna.


> [!NOTE]
> I server perimetrali vengono distribuiti per consentire le connessioni per i client Lync abilitati e altri server perimetrali Microsoft, ad esempio in scenari di federazione. Non sono progettati per consentire le connessioni da altri tipi di client o server endpoint. È possibile distribuire il server XMPP Gateway per consentire le connessioni con i partner XMPP configurati. Il server perimetrale e XMPP Gateway possono supportare solo connessioni endpoint da questi tipi di client e federazioni.



## Proxy inverso

Questo proxy è necessario per eseguire le operazioni seguenti:

  - Consentire agli utenti di connettersi alle riunioni o alle conferenze telefoniche con accesso esterno utilizzando URL semplici

  - Consentire agli utenti esterni di scaricare il contenuto delle riunioni

  - Consentire agli utenti esterni di espandere i gruppi di distribuzione

  - Consentire all'utente di ottenere un certificato basato sugli utenti per l'autenticazione basata sui certificati client

  - Consentire agli utenti remoti di scaricare file dal server della Rubrica o inviare query al servizio Address Book Web Query

  - Consentire agli utenti remoti di ottenere aggiornamenti per il software client e dei dispositivi

  - Consentire ai dispositivi mobili di individuare automaticamente i Front End Server che offrono servizi per i dispositivi mobili

  - Abilitare le notifiche push per i dispositivi mobili dai servizi di notifica push Office 365 o Apple

Per ulteriori informazioni relative ai proxy inversi e ai requisiti che devono essere soddisfatti dai proxy inversi, vedere [Configurazione dei requisiti per il proxy inverso in Lync Server 2013](lync-server-2013-configuration-requirements-for-reverse-proxy.md).


> [!NOTE]
> Gli utenti esterni non necessitano di una connessione di rete privata virtuale (VPN) all'organizzazione per poter partecipare alle comunicazioni usando Lync Server 2013. Se nella propria organizzazione è stata implementata la tecnologia VPN e gli utenti usano la rete VPN per Lync, il traffico multimediale (ad esempio le videoconferenze) potrebbe subire effetti negativi. È consigliabile fornire un metodo per la connessione diretta del traffico multimediale al servizio AV Edge, ignorando la rete VPN. Per informazioni dettagliate, vedere l'articolo del blog NextHop su come consentire al traffico multimediale di Lync di ignorare un tunnel VPN all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=256532">http://go.microsoft.com/fwlink/p/?LinkId=256532</A>.



## Firewall

È possibile distribuire la topologia perimetrale solo con un firewall esterno oppure con un firewall esterno e uno interno. Le architetture degli scenari includono due firewall. L'uso di due firewall è il metodo consigliato poiché garantisce un routing rigoroso da un perimetro all'altro della rete e protegge la distribuzione interna con due livelli di firewall.

## Server Director

Un Server Director è un ruolo server facoltativo separato in Lync Server 2013 che non ospita account utente né fornisce informazioni sulla presenza o servizi di conferenza. Può essere usato piuttosto come server dell'hop successivo interno a cui un server perimetrale instrada il traffico SIP in ingresso destinato ai server interni. Il Server Director preautentica le richieste in ingresso e le reindirizza al server o al pool principale dell'utente. Grazie alla preautenticazione nel Director, è possibile rimuovere le richieste degli account utente che non sono note alla distribuzione.

Un Server Director consente di proteggere i server Standard Edition e i Front End Server nei pool Enterprise Edition Front End da attacchi di utenti malintenzionati, ad esempio attacchi Denial-of-Service (DoS). Se la rete è inondata da traffico esterno non valido durante un attacco di questo tipo, il traffico termina in corrispondenza del Server Director. Per informazioni dettagliate sull'uso dei Director, vedere [Scenari per il server Director in Lync Server 2013](lync-server-2013-scenarios-for-the-director.md).

## Vedere anche

#### Concetti

[Requisiti relativi al servizio di bilanciamento del carico hardware per Lync Server 2013](lync-server-2013-hardware-load-balancer-requirements.md)

