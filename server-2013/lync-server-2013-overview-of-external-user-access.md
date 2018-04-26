---
title: "Lync Server 2013: Panoramica dell'accesso degli utenti esterni"
TOCTitle: Panoramica dell'accesso degli utenti esterni
ms:assetid: 97aded6c-5fa3-4225-95a6-9ad094d61654
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398775(v=OCS.15)
ms:contentKeyID: 49301422
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Panoramica dell'accesso degli utenti esterni in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-11-07_

In questa documentazione, il termine *utente esterno* viene usato per definire un'ampia categoria di utenti che comunicano con gli utenti di Lync Server 2013 e Lync 2013 dall'esterno del firewall. Gli utenti esterni autorizzati a comunicare con utenti interni di Lync Server 2013 (ovvero utenti che accedono a Lync Server dall'interno del firewall) possono includere le tipologie seguenti:

  - **Utenti remoti**   Utenti dell'organizzazione che accedono a Lync Server dall'esterno del firewall.

  - **Utenti federati**   Utenti che dispongono di un account presso un'organizzazione cliente o partner attendibile, ad esempio Lync Server 2010, Lync Server 2013 o Office Communications Server 2007 R2. Gli utenti federati possono essere anche membri di organizzazioni partner definite mediante il protocollo XMPP (Extensible Messaging and Presence Protocol) mediante il proxy XMPP nel server perimetrale e il gateway XMPP nel Front End Server o nel pool. Una relazione di trust definita, denominata federazione, non è correlata né dipende da una relazione di trust di Servizi di dominio Active Directory.
    

    > [!NOTE]
    > Giugno 2014 è la data di fine servizio annunciata per AOL e Yahoo!. Per informazioni dettagliate, vedere <A href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Supporto della connettività per messaggistica istantanea pubblica in Lync Server 2013</A>.



  - **Utenti di sistemi di messaggistica istantanea pubblici**   Contatti che gli utenti stabiliscono tramite servizi di messaggistica istantanea pubblici (Windows Live, Yahoo\! e AOL).

  - **Utenti mobili**   Utenti membri dell'organizzazione che usano uno smartphone o un tablet che esegue il client Lync Mobile accedono alla distribuzione interna e possono comunicare con altre categorie di utenti. L'utente mobile usa i servizi per dispositivi mobili pubblicati tramite il proxy inverso per accedere alla distribuzione interna. Per informazioni dettagliate sulle caratteristiche e le funzionalità disponibili in Lync Mobile, vedere le tabelle di confronto dei client per dispositivi mobili all'indirizzo [http://go.microsoft.com/fwlink/?linkid=234777\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=234777%26clcid=0x410).

  - **Utenti anonimi**   Utenti che non dispongono di un account utente in Servizi di dominio Active Directory dell'organizzazione o in un dominio federato supportato, ma che possono essere stati invitati a partecipare in remoto a una conferenza locale.

La distribuzione del server perimetrale offre accesso esterno per i tipi di comunicazioni seguenti:

  - **IM e presenza**   Gli utenti esterni autorizzati possono partecipare a conversazioni e conferenze di messaggistica istantanea e possono ottenere informazioni sullo stato di presenza di altri utenti. Gli utenti di provider di servizi IM pubblici possono partecipare a conversazioni con singoli utenti di Lync Server dell'organizzazione e accedere alle informazioni sulla presenza ma non possono prendere parte a conferenze IM a più utenti mediante Lync Server. Si tratta di comunicazioni strettamente peer-to-peer. Il trasferimento dei file non è supportato per gli utenti di provider di servizi IM pubblici e le comunicazioni audio/video peer-to-peer sono supportate per gli utenti di Windows Messenger 2011 ma non per altri provider di servizi IM pubblici.
    
    Sono supportati entrambi i protocolli SIP e XMPP. Per offrire servizi per XMPP, vedere [Pianificazione per SIP, federazione XMPP e messaggistica istantanea pubblica in Lync Server 2013](lync-server-2013-planning-for-sip-xmpp-federation-and-public-instant-messaging.md).

  - **Conferenze Web**   Gli utenti esterni autorizzati possono partecipare a conferenze ospitate nella distribuzione di Lync Server. Gli utenti remoti, federati e anonimi possono essere autorizzati alla partecipazione alle conferenze Web, ma gli utenti di messaggistica istantanea pubblica non possono partecipare alle conferenze. In base alle opzioni selezionate, gli utenti abilitati per il Web Conferencing possono partecipare alla condivisione di desktop e applicazioni e possono fungere da organizzatori o relatori delle riunioni.

  - **Conferenze audio e video**   Gli utenti esterni autorizzati possono partecipare a conferenze audio e video ospitate da una distribuzione di Lync Server. Le comunicazioni audio/video peer-to-peer sono supportate per gli utenti di Windows Messenger 2011 ma non per altri utenti si provider di servizi IM pubblici.

Per controllare le comunicazioni, è possibile configurare uno o più criteri che definiscono le modalità di comunicazione tra gli utenti che si trovano all'interno e all'esterno dell'organizzazione. È inoltre possibile configurare impostazioni e applicare criteri per singoli utenti interni o per tipi specifici di utenti esterni allo scopo di controllare le comunicazioni con gli utenti esterni.

Ruoli Lync Server 2013 usati per fornire accesso esterno:

**Server perimetrale**   Il server perimetrale è un server o un pool di server che esegue i servizi che consentono l'accesso esterno a servizi di IM e presenza, conferenza, audio/video e altri contenuti multimediali (ad esempio il trasferimento di file). Se lo si desidera, è anche possibile configurare il server perimetrale per la federazione con altre distribuzioni di Lync Server o Office Communications Server 2007 R2 e altre distribuzioni XMPP. La funzionalità di connettività IM pubblica facoltativa viene abilitata e configurata tramite server perimetrale.

**Director**   Il Server Director è un server o un pool di server facoltativo che esegue il ruolo Lync Server 2013  Server Director responsabile della preautenticazione delle richieste utente e del relativo instradamento al Front End Server o pool Front End principale dell'utente. Esso tuttavia non ospita account utente.

**Proxy inverso**   Proxy inverso è un termine generico che fa riferimento a server specializzati usati per pubblicare risorse disponibili nella rete interna e recuperare informazioni per i client dalla risorse pubblicate. Lync Server 2013 usa il proxy inverso per pubblicare numerose funzionalità quali le riunioni in conferenza, le ubicazioni di partecipazione alle conferenze, la rubrica, l'espansione delle liste di distribuzione, il download dei contenuti delle riunioni, gli aggiornamenti dei dispositivi, i servizi per dispositivi mobili e molto altro. Qualsiasi proxy inverso che soddisfa i requisiti per la pubblicazione dei percorsi di risorse necessari è utilizzabile. Microsoft Forefront Threat Management Gateway (TMG) 2010 viene usato come esempio per illustrare le regole di pubblicazione necessarie, tuttavia Forefront TMG 2010 non è richiesto.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync Server 2013 supporta sia IPv4 sia IPv6. Windows Server 2008 R2, Windows Server 2012 e Windows Server 2012 R2 usano un dual stack in grado di avvalersi di IPv4 e di IPv6 simultaneamente. Ciò è importante in considerazione della natura transitoria di una distribuzione in fase di passaggio da IPv4 a IPv6. IPv4 può essere supportato in alcune aree della distribuzione mentre in altre si può usare IPv6. Ciò è di particolare importanza per quanto concerne Internet e le distribuzioni interne. I client esterni devono comunicare tramite il proxy inverso per usare servizi quali le riunioni, il download della rubrica e così via. Allo stesso tempo Forefront Threat Management Gateway 2010 e Internet Security and Acceleration Server 2006 non supportano l'assegnazione indirizzi IPv6, indipendentemente dalla versione del sistema operativo in cui sono stati distribuiti. È necessario predisporre una pianificazione coerente in relazione all'uso di IPv6 e IPv4 in quanto essi sono correlati ai dati esterni.</td>
</tr>
</tbody>
</table>

