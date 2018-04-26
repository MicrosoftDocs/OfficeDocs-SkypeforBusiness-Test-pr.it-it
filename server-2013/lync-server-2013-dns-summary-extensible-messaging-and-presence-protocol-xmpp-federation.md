---
title: Riepilogo di DNS - federazione di XMPP (Extensible Messaging and Presence Protocol)
TOCTitle: Riepilogo di DNS - federazione di XMPP (Extensible Messaging and Presence Protocol)
ms:assetid: 0f720a2a-8ab5-43cc-882a-ab595ed3cec7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ618368(v=OCS.15)
ms:contentKeyID: 49299700
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo di DNS - federazione di XMPP (Extensible Messaging and Presence Protocol)

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per configurare il protocollo XMPP (Extensible Messaging and Presence Protocol) per la distribuzione, creare due record DNS (Domain Name System) in un server DNS esterno che risolverà i record nel servizio Access Edge del server perimetrale o pool di server perimetrali.

## Riepilogo DNS per il protocollo XMPP (Extensible Messaging and Presence Protocol)


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
<th>Mapping a/Commenti</th>
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
<td><p>xmpp.contoso.com (ad esempio)</p></td>
<td><p>Indirizzo IP del servizio Access Edge nel server perimetrale o pool di server perimetrali che ospita il proxy XMPP</p></td>
<td><p>Punta al servizio Access Edge o pool di server perimetrali che ospita il servizio proxy XMPP. In genere, il record SRV creato punta a questo record host (A oppure AAAA)</p></td>
</tr>
</tbody>
</table>


## Vedere anche

#### Attività

[Configurazione della federazione di XMPP in Lync Server 2013](lync-server-2013-setting-up-xmpp-federation.md)  

#### Concetti

[Determinare i requisiti di DNS per Lync Server 2013](lync-server-2013-determine-dns-requirements.md)

