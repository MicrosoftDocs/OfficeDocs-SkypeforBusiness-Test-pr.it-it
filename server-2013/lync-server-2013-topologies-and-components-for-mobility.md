---
title: 'Lync Server 2013: Componenti e topologie per dispositivi mobili'
TOCTitle: Componenti e topologie per dispositivi mobili
ms:assetid: be3cae7a-095d-4785-91ba-6fac99eba92a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690037(v=OCS.15)
ms:contentKeyID: 49301823
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Componenti e topologie per dispositivi mobili in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-17_

    The information in this topic pertains to Cumulative Updates for Lync Server 2013: February 2013.

Per supportare le applicazioni Lync Mobile sui dispositivi mobili, in Lync Server 2013 sono disponibili tre servizi: servizio Mobility Mcx di Lync Server 2013, servizio di individuazione automatica di Lync Server 2013 e servizio notifica Push di Lync Server 2013. Negli aggiornamenti cumulativi per Lync Server 2013 di febbraio 2013 è stato aggiunto un servizio gratuito ma avanzato per i client Lync 2013 Mobile: per il supporto per dispositivi mobili viene utilizzata l'API Web Unified Communications o UCWA. In questa sezione vengono descritti brevemente questi componenti e vengono identificate le topologie di Lync Server 2013 che supportano i servizi per dispositivi mobili.


> [!NOTE]
> I servizi per dispositivi mobili sono disponibili anche nelle distribuzioni ibride. Non è necessario distribuire servizi per supportare i dispositivi mobili se gli utenti si trovano online. Non è necessario definire un'impostazione per il servizio di individuazione automatica per consentire agli utenti mobili di trovare la rispettiva identità online.



> [!important]  
> Se si pianifica la connettività di utenti esterni, ad esempio con federazione, accesso utenti esterni o funzionalità per dispositivi mobili, è necessario utilizzare i server perimetrali con il server Standard Edition e il Front End Server o il pool Front End. Il server Standard Edition e il Front End Server o il pool Front End non dispongono dei componenti necessari per consentire agli utenti esterni di accedere alla distribuzione interna o per consentire alla distribuzione interna di comunicare con gli utenti esterni. Per tutti gli scenari che includono utenti esterni che collaborano o comunicano con utenti interni, inclusi i servizi per dispositivi mobili, è necessario distribuire almeno un server perimetrale e un proxy inverso.<br />La <em>notifica Push</em> utilizza un tipo di federazione con i servizi di Lync Online che ospita il fornitore di servizi di accesso a terze parti della notifica Push (PNCH, Push Notification Clearing House). La notifica Push comprende gli avvisi sonori, gli avvisi su schermo (testo) e i riquadri che vengono inviati tramite push dalle applicazioni ai dispositivi Apple iPhone, iPad e Windows Phone quando il dispositivo mobile è inattivo. PNCH riceve le notifiche Push da Lync Server. Quando PNCH riceve una notifica di un messaggio, inoltra una notifica ai client mobili tramite i Servizi di notifica Push Apple o il Servizio di notifica Push di Lync Server 2013, a seconda del client mobile a cui è destinato il messaggio. PNCH è un servizio necessario per questi client mobili. Per stabilire una federazione con Lync Online, PNCH utilizza server perimetrali e certificati per garantire la riservatezza e l'autenticazione, criteri e record DNS (Domain Name System) configurati correttamente. I client Lync Mobile basati su Android e Nokia Symbian non utilizzano PNCH. Per informazioni dettagliate sulla pianificazione e la distribuzione dei server perimetrali, vedere <a href="lync-server-2013-planning-for-external-user-access.md">Pianificazione dell'accesso degli utenti esterni in Lync Server 2013</a> e <a href="lync-server-2013-deploying-external-user-access.md">Distribuzione dell'accesso degli utenti esterni in Lync Server 2013</a>.<br />I client Lync 2013 Mobile per dispositivi Apple introdotti con gli aggiornamenti cumulativi per Lync Server 2013 di febbraio 2013 non utilizzano più la notifica Push o il fornitore di servizi di accesso a terze parti della notifica Push (PNCH, Push Notification Clearing House). I client Lync 2013 Mobile in Windows Phone continuano a utilizzare la notifica Push e PNCH.

## Componenti di mobilità

I servizi che supportano i dispositivi mobili sono i seguenti:

  - **API Web Unified Communications (UCWA) di Lync Server 2013**   Fornisce i servizi per le comunicazioni in tempo reale con client per dispositivi mobili e client Web in Lync Server 2013. Quando si distribuiscono gli aggiornamenti cumulativi per Lync Server 2013 di febbraio 2013 nel Front End Server e nel Server Director, l'installazione crea una directory virtuale nei servizi Web interni ed esterni (Ucwa). Un componente Web che fa parte della directory virtuale Ucwa accetta le chiamate dai client abilitati per UCWA. Le app client comunicano tramite un'interfaccia REST per la presenza, i contatti, la messaggistica istantanea, VoIP, le videoconferenze e la collaborazione. UCWA utilizza un canale basato su P-GET per inviare eventi, ad esempio una chiamata in arrivo, un messaggio istantaneo in arrivo o un messaggio all'app client.
    

    > [!NOTE]
    > <EM>REST</EM> o Representational State Transfer è uno stile architettonico software per sistemi distribuiti ampiamente adottato in diverse forme e rispondente ai requisiti dei servizi Web in generale.



  - **Servizio Mobility (Mcx) di Lync Server 2013**   Questo servizio supporta le funzionalità Lync, ad esempio messaggistica istantanea, presenza e contatti, sui dispositivi mobili. Il servizio Mobility viene installato in ogni Front End Server di ciascun pool pianificato per il supporto delle funzionalità Lync nei dispositivi mobili. Quando si installa Lync Server 2013, viene creata una nuova directory virtuale (Mcx) sia nel sito Web interno che nel sito Web esterno dei Front End Server.
    
    > [!important]  
    > Lync Server 2013 con gli aggiornamenti cumulativi per Lync Server 2013 di febbraio 2013 supporta sia il servizio Mobility introdotto nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011, comunemente noto come Mcx, sia il componente Web UCWA. La combinazione di questi due servizi per dispositivi mobili garantisce l'interoperabilità e consente agli utenti l'utilizzo con i client Lync 2010 Mobile e Lync 2013 Mobile in Lync Server 2013.

  - **Servizio di individuazione automatica di Lync Server 2013**   Questo servizio identifica la posizione dell'utente e consente ai dispositivi mobili e ad altri client Lync di individuare le risorse, come gli URL interni ed esterni per i servizi Web di Lync Server 2013 e l'URL per Mcx o UCWA, indipendentemente dalla posizione di rete. L'individuazione automatica utilizza nomi host hardcoded (lyncdiscoverinternal per gli utenti all'interno della rete, lyncdiscover per quelli all'esterno) e il dominio SIP dell'utente. Sono supportate connessioni client che utilizzano HTTP o HTTPS.
    
    Il servizio di individuazione automatica è installato in tutti i Front End Server e in tutti i Server Director, in ogni pool pianificato per il supporto delle funzionalità Lync nei dispositivi mobili. Quando si installa il servizio di individuazione automatica, viene creata una nuova directory virtuale (Autodiscover) sia nel sito Web interno che nel sito Web esterno dei Front End Server e dei Director.
    

    > [!NOTE]
    > Il servizio di individuazione automatica è presente nell'elenco in quanto componente critico per la distribuzione di servizi client per dispositivi mobili. Il ruolo dell'individuazione automatica in Lync Server 2013 è stato ampliato in modo da offrire servizi per tutti i client. Per informazioni dettagliate sulla pianificazione del servizio di individuazione automatica, vedere <A href="lync-server-2013-planning-for-autodiscover.md">Pianificazione dell'individuazione automatica</A>.



  - **Servizio di notifica Push**   Questo servizio basato su cloud è disponibile nel data center di Lync Online. Quando l'applicazione per dispositivi mobili Lync è inattiva in un dispositivo Apple iOS o Windows Phone supportato, non può rispondere a nuovi eventi, come un nuovo invito tramite messaggistica istantanea, un messaggio istantaneo perso, una chiamata senza risposta o un messaggio in segreteria telefonica, perché questi dispositivi non supportano l'esecuzione in background delle applicazioni per dispositivi mobili. In questi casi, al dispositivo mobile viene inviata una notifica del nuovo evento, nota come *notifica Push*. Il servizio Mobility invia la notifica al servizio di notifica Push basato su cloud, che invia quindi la notifica al Servizio di notifica Push Apple (APNS) (per i dispositivi Apple iOS supportati) o al Servizio di notifica Push Microsoft (MPNS) (per Windows Phone), che a sua volta la invia al dispositivo mobile. L'utente può quindi rispondere alla notifica nel dispositivo mobile per attivare l'applicazione.
    
    I dispositivi Lync 2010 Mobile in Apple e Windows Phone utilizzano le notifiche Push. Il client Lync 2013 Mobile per dispositivi Apple introdotto con gli aggiornamenti cumulativi per Lync Server 2013 di febbraio 2013 non utilizza più la notifica Push o il fornitore di servizi di accesso a terze parti della notifica Push (PNCH, Push Notification Clearing House).

Nel diagramma seguente viene illustrata la posizione del Servizio di notifica Push in una topologia di Lync Server 2013 che utilizza UCWA e i client Lync 2013 Mobile.

![UCWA servizio di notifica Push](images/Hh690037.166d60fd-ff71-4ffe-9f66-3c8bbde0b5ae(OCS.15).jpg "UCWA servizio di notifica Push")

Il servizio Mcx, introdotto nell'aggiornamento cumulativo per Lync Server 2010 di novembre 2011, offre servizi ai client Lync 2010 Mobile. Nel diagramma seguente viene illustrato il servizio di notifica Push applicato a una topologia che utilizza Mcx e i client Lync 2010 Mobile.

![MCX servizio di notifica Push](images/Hh690037.3081634e-60e7-4348-b24e-bbbf05a90f5f(OCS.15).jpg "MCX servizio di notifica Push")

## Topologie supportate

Applicando gli aggiornamenti cumulativi per Lync Server 2013 di febbraio 2013, vengono aggiunti i componenti Web UCWA per supportare i dispositivi mobili per le caratteristiche dei client Lync 2013 Mobile nelle topologie seguenti:

  - Lync Server 2013 Standard Edition

  - Lync Server 2013 Enterprise Edition

Il server perimetrale può essere un server perimetrale di Lync Server 2010. 

Una distribuzione di Lync Server 2013 senza gli aggiornamenti cumulativi per Lync Server 2013 di febbraio 2013 utilizzerà il servizio Mobility Mcx e sarà in grado di offrire servizi solo per Lync 2010 Mobile.

> [!important]  
> Il servizio Mobility è supportato nei Front End Server collocati con il ruolo Mediation Server con due interfacce di rete, ma è necessario eseguire i passaggi appropriati per configurare le interfacce. È necessario assegnare gli indirizzi IP all'interfaccia specifica che comunicherà come Mediation Server e l'IP dell'interfaccia di rete che comunicherà come Front End Server. È possibile eseguire questa operazione in Generatore di topologie selezionando l'indirizzo IP corretto per ogni servizio, anziché utilizzare l'opzione predefinita <strong>Usa tutti gli indirizzi IP configurati</strong>.

## Vedere anche

#### Ulteriori risorse

[Pianificazione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-planning-for-external-user-access.md)  
[Distribuzione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-deploying-external-user-access.md)  
[Pianificazione dell'individuazione automatica](lync-server-2013-planning-for-autodiscover.md)

