---
title: 'Riepilogo DNS: SIP, federazione di XMPP e messaggistica istantanea pubblica'
TOCTitle: 'Riepilogo DNS: SIP, federazione di XMPP e messaggistica istantanea pubblica'
ms:assetid: 1ed24fb8-a849-44c0-a52e-7aef7527e644
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ618369(v=OCS.15)
ms:contentKeyID: 49299886
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo DNS: SIP, federazione di XMPP e messaggistica istantanea pubblica

 

_**Ultima modifica dell'argomento:** 2015-03-09_

I record DNS (Domain Name System) che saranno necessari per definire una federazione con partner Office Communications Server o Lync Server dipende dalla propria decisione di consentire o meno l'individuazione DNS automatica del dominio da altri partner. Se si pubblica il record SRV \_sipfederationtls.\_tcp. *\<nome di dominio SIP\>*, qualsiasi altro dominio federato SIP potrà "individuare" la propria federazione. È possibile stabilire con quali domini federati è possibile comunicare utilizzando le impostazioni per consentire e bloccare i domini nel Pannello di controllo di Lync Server oppure impostando la configurazione dei domini consentiti o bloccati utilizzando Lync Server Management Shell e i cmdlet di PowerShell **Get**, **Set**, **New**, **Remove-CsAllowedDomain** e **-CsBlockedDomain**. Per informazioni aggiuntive su come configurare queste impostazioni e sull'uso dei cmdlet di PowerShell, vedere **Argomenti correlati** alla fine dell'argomento.

La tabella di riepilogo dei record DNS indica le voci obbligatorie per una federazione aperta o individuabile. Se non si desidera implementare l'individuazione della federazione, è possibile decidere di non configurare il record \_sipfederationtls.\_tcp. *\<nome di dominio SIP\>*.

> [!important]  
> Esistono scenari specifici in cui si richiedere il record SRV _sipfederationtls._tcp. <em>&lt;nome di dominioSIP&gt;</em>, ma non si desidera disporre di una federazione individuabile, ed esempio quando è stata distribuita la mobilità per gli utenti. La federazione PNCH (push notification clearinghouse) della mobilità è un tipo speciale usato per i client Microsoft Lync Mobile su Apple iPhone o iPad usando il client Lync 2010 Mobile o su Windows Phone usando i client Lync 2010 Mobile o Lync 2013 Mobile. Il record SRV _sipfederationtls._tcp. <em>&lt;nome di dominio SIP&gt;</em> viene usato in caso di mobilità e notifiche push. Per attenuare il problema e controllare l'individuabilità, deselezionare l'impostazione <strong>Abilita individuazione dominio partner</strong> per disattivare l'individuazione.

Per configurare il protocollo XMPP (Extensible Messaging and Presence Protocol) per la distribuzione, creare due record DNS (Domain Name System) in un server DNS esterno che risolverà i record nel servizio Access Edge del server perimetrale o pool di server perimetrali.

Quando si configura il DNS (Domain Name System) per la connettività per messaggistica istantanea pubblica, la configurazione che supporta gli utenti esterni supporterà la connettività per messaggistica istantanea pubblica. Se è stato già configurato il server perimetrale o il pool di server perimetrali, dovrebbero essere disponibili i record DNS necessari per supportare la connettività per messaggistica istantanea pubblica.

## Riepilogo DNS - Federazione SIP


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Posizione/TIPO/Porta</th>
<th>FQDN</th>
<th>Indirizzo IP/Record host FQDN</th>
<th>Corrisponde a/Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DNS esterno/SRV/5061</p></td>
<td><p>_sipfederationtls._tcp.contoso.com</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>Interfaccia esterna servizio Access Edge Necessario per l'individuazione DNS automatica della federazione per altri partner federativi potenziali ed è noto come &quot;Domini SIP consentiti&quot; (federazione avanzata nelle versioni precedenti). Ripetere secondo necessità per tutti i domini SIP con utenti predisposti per Lync</p>
<div class="alert">
> [!important]  
> Questo record SRV è necessario per la mobilità e PNCH. Nei casi in cui sono presenti più domini SIP, creare e pubblicare un record SRV per ogni dominio che avrà client Lync Mobile. Il servizio notifica Push e il servizio notifica Push Apple potrebbero non funzionare come previsto nei casi in cui non sia presente un record SRV esplicito per ogni dominio SIP supportato dalla distribuzione.
</div></td>
</tr>
</tbody>
</table>


## Riepilogo di DNS - XMPP (Extensible Messaging and Presence Protocol)


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Posizione/TIPO/Porta</th>
<th>FQDN</th>
<th>Indirizzo IP/Record host FQDN</th>
<th>Corrisponde a/Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DNS esterno/SRV/5269</p></td>
<td><p>_xmpp-server._tcp.contoso.com</p></td>
<td><p>xmpp.contoso.com</p></td>
<td><p>Interfaccia esterna proxy XMPP servizio Access Edge o pool di server perimetrali. Se necessario, ripetere per tutti i domini SIP interni con utenti abilitati per Lync in cui la comunicazione con i contatti XMPP è consentita mediante la configurazione dei Criteri di accesso esterno attraverso un criterio globale, un criterio del sito in cui si trova l'utente o un criterio utente applicato all'utente abilitato per Lync. È inoltre necessario configurare un dominio XMPP nel criterio Partner federati XMPP. Per ulteriori informazioni, vedere gli argomenti indicati nella sezione <strong>Vedere anche</strong>.</p></td>
</tr>
<tr class="even">
<td><p>DNS esterno/A</p></td>
<td><p>xmpp.contoso.com (esempio)</p></td>
<td><p>Indirizzo IP del servizio Access Edge nel server perimetrale o nel pool di server perimetrali che ospita il proxy XMPP</p></td>
<td><p>Punta al servizio Access Edge o al pool di server perimetrali che ospita il servizio proxy XMPP. Il record SRV creato punterà a questo record host (A o AAAA).</p></td>
</tr>
</tbody>
</table>


## Riepilogo DNS - Connettività per messaggistica istantanea pubblica


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Posizione/TIPO/Porta</th>
<th>FQDN/Record DNS</th>
<th>Indirizzo IP/FQDN</th>
<th>Corrisponde a/Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DNS esterno/A</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>Interfaccia del servizio Access Edge</p></td>
<td><p>Interfaccia esterna del servizio Access Edge (Contoso). Ripetere in base alle esigenze per tutti i domini SIP con utenti abilitati per Lync.</p></td>
</tr>
</tbody>
</table>


## Vedere anche

#### Attività

[Configurazione della federazione di XMPP in Lync Server 2013](lync-server-2013-setting-up-xmpp-federation.md)  
[Configurazione delle notifiche push in Lync Server 2013](lync-server-2013-configuring-for-push-notifications.md)  
[Abilitare o disabilitare l'individuazione dei partner della federazione in Lync Server 2013](lync-server-2013-enable-or-disable-discovery-of-federation-partners.md)  

#### Concetti

[Scenari per l'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-scenarios-for-external-user-access.md)  
[Determinare i requisiti di DNS per Lync Server 2013](lync-server-2013-determine-dns-requirements.md)  

#### Ulteriori risorse

[Gestire i domini federati SIP per l'organizzazione in Lync Server 2013](lync-server-2013-manage-sip-federated-domains-for-your-organization.md)

