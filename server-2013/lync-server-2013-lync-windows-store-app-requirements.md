---
title: Requisiti dell'app Lync di Windows Store
TOCTitle: Requisiti dell'app Lync di Windows Store
ms:assetid: 5f2e0a40-8450-4f61-b6f6-913fc1906020
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ823129(v=OCS.15)
ms:contentKeyID: 52062166
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti dell'app Lync di Windows Store

 

_**Ultima modifica dell'argomento:** 2013-12-03_

Le organizzazioni con una distribuzione locale di Lync Server devono soddisfare i requisiti seguenti per supportare app Windows Store Lync.


> [!NOTE]
> Per Lync Server 2010, eseguire l'aggiornamento cumulativo per Lync Server 2010 di febbraio 2012 (disponibile all'indirizzo <A class=uri href="http://go.microsoft.com/fwlink/?linkid=3052%26kbid=2670352">http://go.microsoft.com/fwlink/?linkid=3052&amp;kbid=2670352</A>) o successivo su tutti i server. Per consentire agli utenti di partecipare alle riunioni, eseguire l'aggiornamento cumulativo per Lync Server 2010 di ottobre 2012 (disponibile all'indirizzo <A class=uri href="http://go.microsoft.com/fwlink/?linkid=3052%26kbid=2737915">http://go.microsoft.com/fwlink/?linkid=3052&amp;kbid=2737915</A>) sui server.



  - Abilitare l'individuazione automatica, Lync Web App e WebTicket sul server.

  - Abilitare l'autenticazione dei certificati nel Front End Server o nel pool Front End. Il processo di registrazione dell'utente nel Front End Server o nel pool Front End viene spesso denominato registrar. Per informazioni dettagliate, vedere [Creare le impostazioni di configurazione di Registrazione avanzata](lync-server-2013-create-registrar-configuration-settings.md).

  - Pubblicare i record di risorsa dell'alias DNS (CNAME) per il servizio di individuazione automatica.

  - Non è più necessario verificare che il punto di distribuzione dell'elenco di revoche di certificati (CRL) per i certificati emessi per i punti del server Lync faccia riferimento a una risorsa HTTP anziché a una risorsa LDAP. Verificare comunque che nei computer client siano installati gli aggiornamenti più recenti di Windows.

  - Configurare i proxy HTTP dell'organizzazione in modo da consentire il traffico HTTP relativo al server Lync. Aggiungere le eccezioni per i servizi di individuazione automatica, Lync Web App e WebTicket, se necessario.

  - Nei client, installare Windows 8.1 e la versione più recente di app Windows Store Lync per correggere un problema di accesso che in genere si verifica quando si utilizzano più domini (ad esempio, quando l'URI SIP è **userA@domainZ.com** ma il server perimetrale è **sip.domainX.com**).

Se l'organizzazione sottoscrive un abbonamento a Lync Online o Office 365 e si utilizza il proprio nome di dominio, è necessario eseguire alcuni passaggi aggiuntivi per configurare la rete per l'individuazione automatica dei server Lync. I requisiti della configurazione di rete sono gli stessi per app Windows Store Lync e Lync sui dispositivi mobili. Seguire le istruzioni per la configurazione della rete nell'articolo wiki su Office 365 relativo alla configurazione di dispositivi mobili con Lync, disponibile all'indirizzo [http://go.microsoft.com/fwlink/?LinkId=271822](http://go.microsoft.com/fwlink/?linkid=271822).

## Vedere anche

#### Concetti

[Distribuzione dell'app Lync di Windows Store](lync-server-2013-deploying-lync-windows-store-app.md)

