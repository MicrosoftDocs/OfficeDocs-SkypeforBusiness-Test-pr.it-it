---
title: "Lync Server 2013: Elenco di controllo di distribuzione per l'accesso degli utenti esterni"
TOCTitle: Elenco di controllo di distribuzione per l'accesso degli utenti esterni
ms:assetid: 3f55f502-88a0-4315-8783-45a32a0b78ea
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425910(v=OCS.15)
ms:contentKeyID: 49300310
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Elenco di controllo di distribuzione per l'accesso degli utenti esterni in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per distribuire la rete perimetrale e implementare il supporto per gli utenti esterni, è necessario aver già distribuito i server interni di Microsoft Lync Server 2013, incluso un pool Front End o un server Standard Edition. Se si prevede di distribuire i server Director facoltativi nella rete interna, è inoltre consigliabile distribuirli prima dei server perimetrali. Per informazioni dettagliate sul processo di distribuzione dei server Server Director, vedere [Scenari per il server Director in Lync Server 2013](lync-server-2013-scenarios-for-the-director.md) nella documentazione relativa alla pianificazione.

Microsoft Lync Server 2013 include strumenti che facilitano la pianificazione e la distribuzione dei server interni e di quelli perimetrali. Al completamento della topologia, pubblicare la definizione di topologia risultante nell'ambiente di produzione. A tale scopo, è necessario essere membri dei gruppi **Domain Admins** e **RTCUniversalServerAdmins**.

  - **Strumento di pianificazione**    Office Communications Server 2007 R2 includeva uno strumento di pianificazione vero e proprio e uno strumento di pianificazione della topologia perimetrale che poteva essere utilizzato come supporto per la progettazione della topologia. In Lync Server 2010 questi due strumenti sono stati combinati in un unico Strumento di pianificazione che contiene caratteristiche e funzionalità aggiuntive, inclusi la registrazione del numero di utenti pianificato, i requisiti relativi ai servizi vocali, i tipi di accesso degli utenti esterni e le opzioni di federazione. Inoltre, è possibile pianificare i parametri di rete di un'infrastruttura, inclusi gli indirizzi IP, i tipi di servizio di bilanciamento del carico e altre considerazioni in merito alle reti perimetrali.

  - **Generatore di topologie**    Lync Server 2013  Generatore di topologie consente di definire la topologia e i componenti. Il Generatore di topologie è essenziale per la distribuzione di server che eseguono Lync Server 2013. Il Generatore di topologie pubblica i risultati in un archivio di gestione centrale utilizzato per configurare tutti i server che eseguono Lync Server 2013 nell'organizzazione. Non è possibile installare Lync Server 2013 nei server senza utilizzare il Generatore di topologie.

Se la topologia perimetrale è stata definita durante il processo di pianificazione, eseguendo anche il Generatore di topologie per definirla, è possibile utilizzare tali risultati per avviare la distribuzione del server perimetrale. Se la creazione della topologia perimetrale non è stata completata in precedenza o si desidera modificare informazioni specificate in precedenza, è necessario interrompere l'esecuzione di Generatore di topologie prima di procedere ad altri passaggi di distribuzione. Per informazioni dettagliate su come creare la topologia, vedere [Scenari per l'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-scenarios-for-external-user-access.md).

Per informazioni dettagliate sullo strumento di pianificazione e sul Generatore di topologie, vedere [Inizio del processo di pianificazione per Lync Server 2013](lync-server-2013-beginning-the-planning-process.md) nella documentazione relativa alla pianificazione.

Nella tabella riportata di seguito viene fornita una panoramica del processo di distribuzione dei server perimetrali. Per esaminare le decisioni di pianificazione da prendere prima di distribuire l'accesso degli utenti esterni, vedere [Scenari per l'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-scenarios-for-external-user-access.md).


> [!WARNING]
> Le informazioni riportate nella tabella seguente fanno riferimento a una nuova distribuzione. Se sono stati distribuiti server perimetrali in un ambiente Lync Server 2010, Office Communications Server 2007 R2 o Office Communications Server 2007, vedere <A href="migration.md">Migrazione</A> per informazioni dettagliate sulla migrazione a Lync Server 2013. La migrazione non è supportata da versioni precedenti a Office Communications Server 2007 R2, inclusi Office Communications Server 2007, Live Communications Server 2005 e Live Communications Server 2003.



Per migliorare la sicurezza e le prestazioni dei server perimetrali e facilitare la distribuzione, applicare le procedure consigliate seguenti quando si distribuiscono la rete perimetrale e i server perimetrali:

  - Distribuire i server perimetrali solo dopo aver verificato il funzionamento di Lync Server 2013 all'interno dell'organizzazione.

  - Si consiglia di distribuire i server perimetrali in un gruppo di lavoro anziché in un dominio. In questo modo si semplifica l'installazione e si mantengono i Servizi di dominio Active Directory (AD DS) al di fuori della rete perimetrale. La presenza dei servizi AD DS nella rete perimetrale può infatti costituire un rischio di sicurezza significativo.

  - L'unione di un server perimetrale a un dominio situato interamente nella rete perimetrale è supportata ma non consigliata. Un server perimetrale come parte del dominio interno viola i limiti di attendibilità della rete, in cui Internet presenta attendibilità minima, la rete perimetrale attendibilità superiore e la rete interna attendibilità massima. Un server perimetrale come membro del dominio fa automaticamente parte della rete più attendibile, ma risiede in una rete meno attendibile (il perimetro).

## Processo di distribuzione dei server perimetrali


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Fase</th>
<th>Passaggi</th>
<th>Autorizzazioni</th>
<th>Documentazione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Creare la topologia perimetrale appropriata e determinare i componenti appropriati.</p></td>
<td><ul>
<li><p>Eseguire Generatore di topologie per configurare le impostazioni dei server perimetrali e per creare e pubblicare la topologia. Utilizzare quindi Lync Server Management Shell per esportare il file di configurazione della topologia.</p></li>
</ul>
<p></p></td>
<td><p>Gruppi <strong>Domain Admins</strong> e <strong>RTCUniversalServerAdmins</strong> o <strong>CsAdmins</strong></p>
<div class="alert">

> [!NOTE]
> È possibile definire una topologia utilizzando un account membro del gruppo degli utenti locali, ma per la pubblicazione di una topologia è necessario un account membro dei gruppi <STRONG>Domain Admins</STRONG> e <STRONG>RTCUniversalServerAdmins</STRONG>.


</div></td>
<td><p><a href="lync-server-2013-building-an-edge-and-director-topology.md">Creazione di una topologia di server perimetrali e server Director in Lync Server 2013</a> nella documentazione relativa alla distribuzione</p></td>
</tr>
<tr class="even">
<td><p>Preparare la configurazione.</p></td>
<td><ol>
<li><p>Verificare che vengano soddisfatti i prerequisiti del sistema.</p></li>
<li><p>Configurare gli indirizzi IP (IPv4 e IPv6, se utilizzati) per le interfacce di rete interne e pubbliche in ogni server perimetrale.</p></li>
<li><p>Configurare record DNS interni ed esterni (host A e AAAA per IPv4 e IPv6), inclusa la configurazione del suffisso DNS nel computer da distribuire come server perimetrale.</p></li>
<li><p>(Facoltativo) Creare e installare certificati pubblici. Il tempo necessario per ottenere i certificati dipende dall'Autorità di certificazione (CA) che emette il certificato. Se non si esegue questo passaggio in questa fase, sarà necessario eseguirlo durante l'installazione dei server perimetrali. I servizi dei server perimetrali non possono essere avviati se non si ottengono e installano i certificati.</p></li>
<li><p>Fornire il supporto per la connettività per messaggistica istantanea pubblica se la distribuzione deve supportare le comunicazioni con utenti di Windows Live, AOL o Yahoo!.</p>
<div class="alert">
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Dal 1 settembre 2012, la licenza di sottoscrizione utenti per la connettività di messaggistica istantanea pubblica di Microsoft Lync (“PIC USL”) non è più disponibile per l'acquisto per i nuovi contratti o quelli in fase di rinnovo. I clienti con licenze attive potranno continuare a eseguire la federazione con Yahoo! Messenger fino alla data di chiusura del servizio. Giugno 2014 è la data di fine servizio annunciata per Yahoo! e AOL. Per informazioni dettagliate, vedere <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Supporto della connettività per messaggistica istantanea pubblica in Lync Server 2013</a>.</p></li>
<li><p>La licenza PIC USL è una licenza di sottoscrizione di tipo mensile per utente, richiesta per la federazione di Lync Server o Office Communications Server con Yahoo! Messenger. La capacità di Microsoft di fornire questo servizio dipende dal supporto offerto da Yahoo! e il contratto sottostante è in fase di chiusura.</p></li>
<li><p>Oggi più che mai, Lync è un potente strumento per la connessione tra diverse organizzazioni e con utenti di tutto il mondo. La federazione con Windows Live Messenger non richiede ulteriori licenze per utente/dispositivo in aggiunta alla licenza CAL Standard per Lync. La federazione con Skype verrà aggiunta a questo elenco, consentendo agli utenti di Lync di raggiungere centinaia di milioni di persone tramite messaggistica istantanea e comunicazioni vocali.</p></li>
</ul></td>
</tr>
</tbody>
</table>

</div></li>
<li><p>Fornire supporto per XMPP e la federazione per i partner di Office Communications Server 2007, Office Communications Server 2007 R2, Lync Server 2010, se la distribuzione li utilizzerà</p></li>
<li><p>Configurare i firewall.</p></li>
</ol></td>
<td><p>In base all'organizzazione</p></td>
<td><p><a href="lync-server-2013-preparing-for-installation-of-servers-in-the-perimeter-network.md">Preparazione dell'installazione dei server nella rete perimetrale per Lync Server 2013</a> nella documentazione relativa alla distribuzione</p></td>
</tr>
<tr class="odd">
<td><p>Configurare il proxy inverso.</p></td>
<td><ul>
<li><p>Configurare il proxy inverso, ad esempio Microsoft Forefront Threat Management Gateway 2010 o Microsoft Internet Security and Acceleration (ISA) Server con Service Pack 1, nella rete perimetrale, ottenere i certificati pubblici necessari e configurare le regole di pubblicazione Web nel server proxy inverso.</p>
<p>Preparare il proxy inverso per i servizi dei dispositivi mobili se si intende utilizzare tali dispositivi e distribuire i servizi nel pool Front End o nel server Standard Edition.</p></li>
</ul></td>
<td><p>Gruppo <strong>Administrators</strong> o amministratore del proxy inverso</p></td>
<td><p></p>
<p><a href="lync-server-2013-setting-up-reverse-proxy-servers.md">Configurare server proxy inversi per Lync Server 2013</a> nella documentazione relativa alla distribuzione</p></td>
</tr>
<tr class="even">
<td><p>Configurare un server Director (facoltativo).</p></td>
<td><ul>
<li><p>(Facoltativo) Installare e configurare uno o più Director nella rete interna.</p></li>
</ul></td>
<td><p>Gruppo <strong>Administrators</strong></p></td>
<td><p><a href="lync-server-2013-setting-up-the-director.md">Configurazione del server Director in Lync Server 2013</a> nella documentazione relativa alla distribuzione</p></td>
</tr>
<tr class="odd">
<td><p>Configurare i server perimetrali.</p></td>
<td><ol>
<li><p>Installare i prerequisiti software.</p></li>
<li><p>Trasportare in ogni server perimetrale il file di configurazione della topologia esportato.</p></li>
<li><p>Installare il software Lync Server 2013 in ogni server perimetrale.</p></li>
<li><p>Configurare i server perimetrali.</p></li>
<li><p>Richiedere e installare i certificati per ogni server perimetrale.</p></li>
<li><p>Avviare i servizi dei server perimetrali.</p></li>
</ol></td>
<td><p>Gruppo <strong>Administrators</strong></p></td>
<td><p><a href="lync-server-2013-setting-up-edge-servers.md">Configurazione di server perimetrali in Lync Server 2013</a> nella documentazione relativa alla distribuzione</p></td>
</tr>
<tr class="even">
<td><p>Configurare la distribuzione per l'accesso degli utenti esterni.</p></td>
<td><ol>
<li><p>Utilizzare il Pannello di controllo di Lync Server per configurare il supporto per ognuno degli elementi seguenti (in base alle esigenze):</p>
<ul>
<li><p>Media Relay</p></li>
<li><p>Route di federazione</p></li>
<li><p>Accesso degli utenti remoti</p></li>
<li><p>Federazione con Lync Server, Office Communications Server e Live Communications Server</p></li>
<li><p>Connettività per messaggistica istantanea pubblica</p></li>
<li><p>Federazione XMPP</p></li>
<li><p>Utenti anonimi</p></li>
</ul></li>
<li><p>Configurare gli account utente per l'accesso degli utenti remoti, la federazione, la connettività per messaggistica istantanea pubblica e il supporto degli utenti anonimi (in base alle esigenze)</p></li>
</ol></td>
<td><p>Gruppo <strong>RTCUniversalServerAdmins</strong> o account utente assegnato al ruolo <strong>CSAdministrator</strong></p>
<p></p></td>
<td><p><a href="lync-server-2013-configuring-support-for-external-user-access.md">Configurazione del supporto per l'accesso degli utenti esterni in Lync Server 2013</a> nella documentazione relativa alla distribuzione</p></td>
</tr>
<tr class="odd">
<td><p>Verificare la configurazione dei server perimetrali.</p></td>
<td><ol>
<li><p>Verificare la connettività dei server e la replica dei dati di configurazione dai server interni.</p></li>
<li><p>Verificare che gli utenti esterni possano connettersi, inclusi gli utenti remoti, gli utenti di domini federati, gli utenti di messaggistica istantanea pubblica e gli utenti anonimi, a seconda dei requisiti della distribuzione.</p></li>
<li><p>Verificare la configurazione e la comunicazione utilizzando Lync Server Remote Connectivity Analyzer <a href="https://www.testocsconnectivity.com" class="uri">https://www.testocsconnectivity.com</a></p></li>
<li><p>Risolvere i problemi di comunicazione e configurazione</p></li>
</ol></td>
<td><p>Per la verifica della replica, il gruppo <strong>RTCUniversalServerAdmins</strong> o l'account utente assegnato al ruolo <strong>CSAdministrator</strong></p>
<p>Per la verifica della connettività degli utenti, un utente per ogni tipo di accesso degli utenti esterni supportato</p>
<p>Utenti remoti</p></td>
<td><p><a href="lync-server-2013-verifying-your-edge-deployment.md">Verifica della distribuzione dei componenti perimetrali in Lync Server 2013</a> nella documentazione relativa alla distribuzione</p></td>
</tr>
</tbody>
</table>

