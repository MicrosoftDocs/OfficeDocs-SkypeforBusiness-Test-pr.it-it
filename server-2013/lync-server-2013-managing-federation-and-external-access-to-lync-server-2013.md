---
title: "Lync Server 2013: Gestisce federazione e accesso esterno a Lync Server 2013"
TOCTitle: Gestione della federazione e dell'accesso esterno a Lync Server 2013
ms:assetid: 26f806c1-f284-4637-b06b-06270336c540
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520966(v=OCS.15)
ms:contentKeyID: 49299977
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestione della federazione e dell'accesso esterno a Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

La distribuzione di un server perimetrale o di un pool di server perimetrali è il primo passaggio per il supporto di utenti esterni. Per informazioni dettagliate sulla distribuzione di server perimetrali, vedere [Distribuzione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-deploying-external-user-access.md) nella documentazione relativa alla distribuzione.

Dopo aver installato e configurato una distribuzione interna di Lync Server 2013, gli utenti interni dell'organizzazione possono collaborare con altri utenti interni che dispongono di account SIP in Servizi di dominio Active Directory (AD DS). La collaborazione può includere l'invio e la ricezione di messaggi istantanei, l'aggiornamento delle informazioni sulla presenza e la partecipazione a conferenze, anche note come "riunioni". È possibile abilitare e configurare l'accesso utente esterno per controllare se gli utenti esterni supportati possono collaborare con gli utenti interni di Lync Server. Gli utenti esterni possono includere utenti remoti della propria distribuzione, utenti federati (inclusi utenti supportati dei provider di servizi di messaggistica istantanea pubblici), membri della federazione XMPP e partecipanti anonimi delle conferenze.

Se la distribuzione includeva l'installazione di un Lync Server 2013  server perimetrale o di un pool di server perimetrali, l'ambito dei tipi di comunicazione possibili risulta notevolmente espanso con alcune opzioni per l'accesso utente esterno, le comunicazioni con i membri di altri domini federati SIP, provider federati SIP e utenti federati XMPP. Dopo aver impostato il server perimetrale o il pool di server perimetrali, è necessario abilitare i tipi di accesso utente esterno che si desidera fornire e configurare i criteri per il controllo dell'accesso esterno. In Lync Server 2013 è possibile abilitare e configurare l'accesso utente esterno e i criteri usando il Pannello di controllo di Lync Server, Lync Server Management Shell o entrambi, in base ai requisiti delle attività. Per informazioni dettagliate su questi strumenti di gestione, vedere [Strumenti di amministrazione di Lync Server 2013](lync-server-2013-lync-server-administrative-tools.md), [Lync Server Management Shell](lync-server-2013-lync-server-management-shell.md) e [Installare gli strumenti di amministrazione di Lync Server 2013](lync-server-2013-install-lync-server-administrative-tools.md) nella documentazione relativa alle operazioni.

> [!IMPORTANT]  
> Quando si progettano la configurazione e i criteri per l'accesso utente esterno, è necessario conoscere la precedenza dei criteri e la modalità di applicazione degli stessi. Le impostazioni criteri di Lync Server applicate a un determinato livello di criteri possono sostituire le impostazioni applicate a un altro livello di criteri. La precedenza dei criteri di Lync Server è la seguente: i criteri utente (maggiore influenza) sostituiscono i criteri sito e i criteri sito sostituiscono i criteri globali (minore influenza). Ciò significa che maggiore è la prossimità dell'impostazione criteri all'oggetto su cui influiscono i criteri, maggiore è l'influenza su tale oggetto.

Per impostazione predefinita, non vi sono criteri configurati per supportare l'accesso utente esterno, incluso l'accesso utente remoto e federato, anche se il supporto dell'accesso utente esterno è già stato abilitato per l'organizzazione. Per controllare l'uso dell'accesso utente esterno, è necessario configurare uno o più criteri, specificando il tipo di accesso utente esterno supportato per ogni criterio. Sono inclusi i criteri di accesso esterno seguenti:

  - **Criteri globali** I criteri globali vengono creati quando si distribuiscono i server perimetrali. Per impostazione predefinita, nei criteri globali non è abilitata alcuna opzione di accesso utente esterno. Per supportare l'accesso utente esterno a livello globale, è possibile configurare i criteri globali per supportare uno o più tipi di opzioni di accesso utente esterno. I criteri globali si applicano a tutti gli utenti dell'organizzazione, ma i criteri sito e utente hanno la precedenza sui criteri globali. Se si eliminano i criteri globali, questi non vengono rimossi, ma ne vengono reimpostati i valori predefiniti.

  - **Criteri sito** È possibile creare e configurare uno o più criteri sito per limitare il supporto per l'accesso utente esterno a siti specifici. La configurazione dei criteri sito ha la precedenza sui criteri globali, ma solo per il sito specifico a cui i criteri si riferiscono. Se, ad esempio, si abilita l'accesso utente remoto nei criteri globali, è possibile specificare criteri sito tramite cui viene disabilitato l'accesso utente remoto per un sito specifico. Per impostazione predefinita, i criteri sito vengono applicati a tutti gli utenti del sito, ma è possibile assegnare criteri utente a un utente per sostituire l'impostazione dei criteri sito.

  - **Criteri utente** È possibile creare e configurare uno o più criteri utente per limitare il supporto per l'accesso utente remoto a utenti specifici. La configurazione dei criteri utente ha la precedenza sui criteri globali e sui criteri sito, ma solo per gli utenti specifici a cui sono assegnati i criteri utente. Se, ad esempio, si abilita l'accesso utente remoto nei criteri globali e nei criteri sito, è possibile specificare criteri utente tramite cui viene disabilitato l'accesso utente remoto e quindi assegnare tali criteri a utenti specifici. Se si creano criteri utente, è necessario applicarli a uno o più utenti affinché diventino attivi.

Per stabilire quali impostazioni di configurazione e quali criteri è necessario creare o modificare, considerare gli aspetti seguenti:

**Si desidera offrire agli utenti interni ed esterni del dominio la possibilità di collaborare tramite le funzionalità di messaggistica istantanea, Web Conferencing e audio/video?**

Configurare le impostazioni come descritto negli argomenti [Configurare criteri per controllare l'accesso degli utenti remoti in Lync Server 2013](lync-server-2013-configure-policies-to-control-remote-user-access.md) e [Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica in Lync Server 2013](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md)

**Si desidera consentire agli utenti anonimi di partecipare ed essere invitati a conferenze ospitate da utenti inclusi nella distribuzione?**

Configurare le impostazioni come descritto negli argomenti [Assegnare i criteri di conferenza per supportare gli utenti anonimi in Lync Server 2013](lync-server-2013-assign-conferencing-policies-to-support-anonymous-users.md), [Creare o modificare criteri conferenza](lync-server-2013-create-or-modify-a-conferencing-policy.md) e [Guida di riferimento alle impostazioni dei criteri di conferenza di Lync Server 2013](lync-server-2013-conferencing-policy-settings-reference.md)

**Si desidera consentire agli utenti di comunicare con i contatti dei domini federati SIP?**

Configurare le impostazioni come descritto negli argomenti [Configurare criteri per controllare l'accesso utente federato in Lync Server 2013](lync-server-2013-configure-policies-to-control-federated-user-access.md), [Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica in Lync Server 2013](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md) e [Gestire i domini federati SIP per l'organizzazione in Lync Server 2013](lync-server-2013-manage-sip-federated-domains-for-your-organization.md)

**Se le comunicazioni con i domini federati SIP sono state abilitate, si desidera abilitare le comunicazioni con i contatti dei partner federati XMPP?**

Configurare le impostazioni come descritto negli argomenti [Configurare criteri per controllare l'accesso utente federato XMPP in Lync Server 2013](lync-server-2013-configure-policies-to-control-xmpp-federated-user-access.md) e [Gestire i partner federati XMPP per l'organizzazione in Lync Server 2013](lync-server-2013-manage-xmpp-federated-partners-for-your-organization.md).

**Se le comunicazioni con i domini federati SIP sono state abilitate, si desidera abilitare l'individuazione automatica della federazione SIP?**

Configurare le impostazioni come descritto nell'argomento [Abilitare o disabilitare l'individuazione dei partner della federazione in Lync Server 2013](lync-server-2013-enable-or-disable-discovery-of-federation-partners.md).

**Se le comunicazioni con i domini federati SIP sono state abilitate, si desidera abilitare l'invio di una dichiarazione di non responsabilità ai contatti federati per avvisarli che è in uso l'archiviazione e che le comunicazioni potrebbero essere archiviate?**

Configurare le impostazioni come descritto nell'argomento [Abilitare o disabilitare l'invio di una dichiarazione di non responsabilità relativa all'archiviazione ai partner federati in Lync Server 2013](lync-server-2013-enable-or-disable-sending-an-archiving-disclaimer-to-federated-partners.md).

**Si desidera consentire agli utente di comunicare con i provider federati SIP che abilitano le comunicazioni con i provider pubblici, quali Windows Live Messenger, AOL e Yahoo\!?**

Configurare le impostazioni come descritto negli argomenti [Configurare criteri per controllare l'accesso degli utenti pubblici in Lync Server 2013](lync-server-2013-configure-policies-to-control-public-user-access.md)[Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica in Lync Server 2013](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md) e [Creare o modificare provider federati SIP pubblici in Lync Server 2013](lync-server-2013-create-or-edit-public-sip-federated-providers.md).

> [!IMPORTANT]  
> <ul>
> <li><p>Dal 1 settembre 2012, la licenza di sottoscrizione utenti per la connettività di messaggistica istantanea pubblica di Microsoft Lync (“PIC USL”) non è più disponibile per l'acquisto per i nuovi contratti o quelli in fase di rinnovo. I clienti con licenze attive potranno continuare a eseguire la federazione con Yahoo! Messenger fino alla data di chiusura del servizio. Giugno 2014 è la data di fine servizio annunciata per Yahoo! e AOL. Per informazioni dettagliate, vedere <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Supporto della connettività per messaggistica istantanea pubblica in Lync Server 2013</a>.</p></li>
> 
> <li><p>La licenza PIC USL è una licenza di sottoscrizione di tipo mensile per utente, richiesta per la federazione di Lync Server o Office Communications Server con Yahoo! Messenger. La capacità di Microsoft di fornire questo servizio dipende dal supporto offerto da Yahoo! e il contratto sottostante è in fase di chiusura.</p></li>
> 
> 
> <li><p>Oggi più che mai, Lync è un potente strumento per la connessione tra diverse organizzazioni e con utenti di tutto il mondo. La federazione con Windows Live Messenger non richiede ulteriori licenze per utente/dispositivo in aggiunta alla licenza CAL Standard per Lync. La federazione con Skype verrà aggiunta a questo elenco, consentendo agli utenti di Lync di raggiungere centinaia di milioni di persone tramite messaggistica istantanea e comunicazioni vocali.</p></li></ul>


**Si desidera consentire agli utenti di comunicare con i provider federati SIP, ovvero provider ospitati che eseguono Microsoft Office 365, Microsoft Lync Online e Microsoft Lync Online 2010?**

Configurare le impostazioni come descritto negli argomenti [Creare o modificare provider federati SIP pubblici in Lync Server 2013](lync-server-2013-create-or-edit-public-sip-federated-providers.md), [Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica in Lync Server 2013](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md) e [Creare o modificare provider federati SIP ospitati in Lync Server 2013](lync-server-2013-create-or-edit-hosted-sip-federated-providers.md)

**La distribuzione è configurata in un dominio suddiviso (anche detto ibrido), in cui il server principale di alcuni utenti si trova in una distribuzione locale mentre per altri utenti il server principale è configurato in un ambiente online?**

Configurare le impostazioni come descritto negli argomenti [Configurare criteri per controllare l'accesso utente federato in Lync Server 2013](lync-server-2013-configure-policies-to-control-federated-user-access.md), [Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica in Lync Server 2013](lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md) e [Creare o modificare provider federati SIP ospitati in Lync Server 2013](lync-server-2013-create-or-edit-hosted-sip-federated-providers.md)

Di seguito è riportata una tabella con l'elenco dei requisiti:


<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Tabulazione nel tipo Federazione e Accesso esterno (orizzontale) Federazione o Accesso esterno (in basso)</th>
<th>Criteri di accesso esterno</th>
<th>Configurazione Access Edge</th>
<th>Domini federati SIP</th>
<th>Provider federati SIP</th>
<th>Partner federato XMPP</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utenti remoti</p></td>
<td><p><a href="lync-server-2013-configure-policies-to-control-remote-user-access.md">Configurare criteri per controllare l'accesso degli utenti remoti in Lync Server 2013</a></p></td>
<td><p><a href="lync-server-2013-enable-or-disable-remote-user-access.md">Abilitare o disabilitare l'accesso degli utenti remoti in Lync Server 2013</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Contatti federati SIP</p></td>
<td><p><a href="lync-server-2013-configure-policies-to-control-federated-user-access.md">Configurare criteri per controllare l'accesso utente federato in Lync Server 2013</a></p>
<p></p></td>
<td><p><a href="lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md">Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica in Lync Server 2013</a></p>
<p><a href="lync-server-2013-enable-or-disable-discovery-of-federation-partners.md">Abilitare o disabilitare l'individuazione dei partner della federazione in Lync Server 2013</a></p>
<p><a href="lync-server-2013-enable-or-disable-sending-an-archiving-disclaimer-to-federated-partners.md">Abilitare o disabilitare l'invio di una dichiarazione di non responsabilità relativa all'archiviazione ai partner federati in Lync Server 2013</a></p></td>
<td><p><a href="lync-server-2013-manage-sip-federated-domains-for-your-organization.md">Gestire i domini federati SIP per l'organizzazione in Lync Server 2013</a></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Contatti federati XMPP</p></td>
<td><p><a href="lync-server-2013-configure-policies-to-control-federated-user-access.md">Configurare criteri per controllare l'accesso utente federato in Lync Server 2013</a></p>
<p><a href="lync-server-2013-configure-policies-to-control-xmpp-federated-user-access.md">Configurare criteri per controllare l'accesso utente federato XMPP in Lync Server 2013</a></p></td>
<td><p><a href="lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md">Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica in Lync Server 2013</a></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p><a href="lync-server-2013-manage-xmpp-federated-partners-for-your-organization.md">Gestire i partner federati XMPP per l'organizzazione in Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p>Utenti dominio suddiviso/ibrido</p></td>
<td><p><a href="lync-server-2013-configure-policies-to-control-federated-user-access.md">Configurare criteri per controllare l'accesso utente federato in Lync Server 2013</a></p></td>
<td><p><a href="lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md">Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica in Lync Server 2013</a></p></td>
<td><p></p></td>
<td><p><a href="lync-server-2013-create-or-edit-hosted-sip-federated-providers.md">Creare o modificare provider federati SIP ospitati in Lync Server 2013</a></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Contatti servizi di messaggistica istantanea pubblici</p></td>
<td><p><a href="lync-server-2013-configure-policies-to-control-public-user-access.md">Configurare criteri per controllare l'accesso degli utenti pubblici in Lync Server 2013</a></p></td>
<td><p><a href="lync-server-2013-enable-or-disable-federation-and-public-im-connectivity.md">Abilitare o disabilitare la federazione e la connettività per la messaggistica istantanea pubblica in Lync Server 2013</a></p></td>
<td><p></p></td>
<td><p><a href="lync-server-2013-create-or-edit-public-sip-federated-providers.md">Creare o modificare provider federati SIP pubblici in Lync Server 2013</a></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Accesso utente anonimo a riunioni e conferenze</p></td>
<td><p></p></td>
<td><p><a href="lync-server-2013-assign-conferencing-policies-to-support-anonymous-users.md">Assegnare i criteri di conferenza per supportare gli utenti anonimi in Lync Server 2013</a></p>


> [!NOTE]
> È anche necessario considerare le impostazioni di configurazione seguenti nei criteri di conferenza: <A href="lync-server-2013-create-or-modify-a-conferencing-policy.md">Creare o modificare criteri conferenza</A> e <A href="lync-server-2013-conferencing-policy-settings-reference.md">Guida di riferimento alle impostazioni dei criteri di conferenza di Lync Server 2013</A>


</td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


È possibile configurare le impostazioni dell'accesso degli utenti esterni, inclusi eventuali criteri che si desidera utilizzare per controllare l'accesso degli utenti esterni, anche se per l'organizzazione non è stato abilitato l'accesso degli utenti esterni. I criteri e le altre impostazioni configurati tuttavia diventano effettivi solo quando si abilita per l'organizzazione l'accesso degli utenti esterni. Gli utenti esterni non possono comunicare con gli utenti dell'organizzazione se l'accesso degli utenti esterni è disabilitato o se non sono configurati criteri di accesso degli utenti esterni per supportarlo.

La distribuzione di server perimetrali autentica i tipi di utenti esterni (ad eccezione degli utenti anonimi che vengono autenticati dall'ID conferenza e da una passkey inviata al partecipante anonimo quando si crea la conferenza e si invitano i partecipanti) e controlla l'accesso in base alla configurazione del supporto dei server perimetrali. Per controllare le comunicazioni, è possibile configurare uno o più criteri nonché impostazioni che definiscono il modo in cui gli utenti all'interno e all'esterno del firewall comunicano tra loro. I criteri e le impostazioni includono il criterio globale predefinito per l'accesso degli utenti esterni, oltre ai criteri sito e utente che è possibile creare e configurare per abilitare uno o più tipi di accesso degli utenti esterni per siti o utenti specifici.

## Argomenti della sezione

  - [Gestire i criteri di accesso esterno per l'organizzazione in Lync Server 2013](lync-server-2013-manage-external-access-policy-for-your-organization.md)

  - [Gestire la configurazione Access Edge per l'organizzazione in Lync Server 2013](lync-server-2013-manage-access-edge-configuration-for-your-organization.md)

  - [Gestire i domini federati SIP per l'organizzazione in Lync Server 2013](lync-server-2013-manage-sip-federated-domains-for-your-organization.md)

  - [Gestire i provider federati SIP per l'organizzazione in Lync Server 2013](lync-server-2013-manage-sip-federated-providers-for-your-organization.md)

  - [Gestire i partner federati XMPP per l'organizzazione in Lync Server 2013](lync-server-2013-manage-xmpp-federated-partners-for-your-organization.md)

  - [Configurazione del supporto della federazione per un cliente di Lync Server 2013](lync-server-2013-configuring-federation-support-for-a-lync-online-customer.md)

