---
title: "Lync Server 2013: Nuove funzionalità per l'accesso utente esterno"
TOCTitle: Nuove funzionalità per l'accesso utente esterno
ms:assetid: 99da6bd5-ec14-4ad9-8f7d-37fbddf567dd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398794(v=OCS.15)
ms:contentKeyID: 49301425
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Nuove funzionalità per l'accesso utente esterno in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-17_

Lync Server 2013 introduce nuove funzionalità che estendono le caratteristiche e metodi di comunicazione per gli utenti. Inoltre, Lync Server 2013 introduce modifiche ai servizi esistenti per integrare meglio ed estendere i servizi disponibili nell'organizzazione. Di seguito è disponibile un riepilogo delle modifiche che potrebbero incidere sulla pianificazione e la distribuzione dei servizi Lync Server 2013  server perimetrale.

  - **Supporto per l'assegnazione indirizzi IPv6**     Lync Server 2013 supporta l'assegnazione indirizzi IPv6 per tutti i servizi server perimetrale. Se sono specificati indirizzi IPv6 per le interfacce tramite la configurazione in Windows Server, è possibile usare gli indirizzi IPv6 nella configurazione server perimetrale tramite la configurazione degli indirizzi IP in Generatore di topologie.
    
    > [!IMPORTANT]  
    > L'uso degli indirizzi IPv6 in Lync Server 2013 dipende dal supporto di IPv6 nei router e nei firewall distribuiti dall'organizzazione, nonché il supporto tramite il provider di servizi Internet.

  - **Protocollo XMPP (Extensible Messaging and Presence Protocol)**     Lync Server 2013 introduce un proxy XMPP completamente integrato (distribuito nei server perimetrali) e un gateway XMPP distribuito nei Front End Server. È possibile distribuire la federazione XMPP come componente facoltativo. L'aggiunta e la configurazione del proxy XMPP e del gateway XMPP consentono agli utenti di Microsoft Lync 2013 di aggiungere contatti dai partner basati su XMPP per la messaggistica istantanea (IM) e la presenza.
    

    > [!NOTE]
    > Attualmente, i servizi XMPP in Lync Server 2013 forniscono solo messaggistica istantanea e presenza tra client Lync e contatti basati su XMPP.



  - **Servizi per client mobili**    Introdotti in un aggiornamento per Lync Server 2010, i servizi per dispositivi mobili in Lync Server 2013 consentono ai client Microsoft Lync Mobile su telefoni mobili e dispositivi tablet che utilizzano sistemi Apple iOS, Android, Windows Phone o Nokia supportati per eseguire alcune attività come l'invio e la ricezione di messaggi istantanei, la visualizzazione di contatti e la visualizzazione della presenza. Inoltre, i dispositivi mobili supportano alcune funzionalità di VoIP aziendale, ad esempio la partecipazione con un clic, Chiamata tramite ufficio, numero unico, segreteria telefonica e notifica delle chiamate senza risposta.
    

    > [!NOTE]
    > I servizi per dispositivi mobili usano il proxy inverso e i servizi pubblicati distribuiti nei Front End Server. Non sono necessarie modifiche ai server perimetrali.



  - **Director sono un ruolo facoltativo**    Il ruolo del server Server Director nella topologia di Lync Server 2013 non è stato modificato. Continua a ospitare i servizi Web, esegue la preautenticazione delle richieste utente in arrivo e indirizza gli utenti esterni al pool principale. La modifica del Server Director da ruolo consigliato a ruolo facoltativo non riduce il valore del Server Director, ma accentua la riduzione del numero di server necessarie e degli altri requisiti hardware (ad esempio, servizi di bilanciamento del carico hardware per il Server Director) senza compromettere caratteristiche e funzionalità. Poiché i Front End Server possono effettuare le stesse operazioni del Server Director senza influire sui servizi forniti, è eventualmente possibile distribuire Director se lo si desidera. È possibile escludere in tutta sicurezza il Server Director essendo sicuri che i Front End Server forniscono gli stessi servizi.

## Vedere anche

#### Concetti

[Pianificazione e configurazione di IPv6 in Lync Server 2013](lync-server-2013-planning-for-and-configuring-ipv6.md)  

#### Ulteriori risorse

[Pianificazione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-planning-for-external-user-access.md)  
[Pianificazione per la federazione di XMPP (Extensible Messaging and Presence Protocol) in Lync Server 2013](lync-server-2013-planning-for-extensible-messaging-and-presence-protocol-xmpp-federation.md)

