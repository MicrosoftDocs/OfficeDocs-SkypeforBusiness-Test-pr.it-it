---
title: "Lync Server 2013: Supporto dell'infrastruttura DNS (Domain Name System)"
TOCTitle: Supporto dell'infrastruttura DNS (Domain Name System)
ms:assetid: 37777c16-94ce-436d-b517-bcf53a564513
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425850(v=OCS.15)
ms:contentKeyID: 49300207
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Supporto dell'infrastruttura DNS (Domain Name System) in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-03-08_

Lync Server 2013 richiede il sistema DNS (Domain Name System) e lo utilizza nei modi seguenti:

  - Per individuare i pool o i server interni per le comunicazioni server-server.

  - Per consentire ai client di individuare il pool Front End o il server Standard Edition utilizzato per diverse transazioni SIP.

  - Per associare gli URL semplici per conferenze ai server che ospitano le conferenze.

  - Per consentire ai server e ai client esterni di connettersi ai server perimetrali o al proxy inverso HTTP per i servizi di messaggistica istantanea o conferenza.

  - Per consentire ai dispositivi per comunicazioni unificate non connessi di individuare il pool Front End o il server Standard Edition che esegue il servizio Web Aggiornamento dispositivi, ottenere gli aggiornamenti e inviare i registri.

  - Per consentire ai client mobili di individuare automaticamente le risorse dei servizi Web senza richiedere agli utenti di immettere manualmente gli URL nelle impostazioni dei dispositivi.

  - Per il bilanciamento del carico DNS.


> [!NOTE]
> Lync Server 2013 non supporta IDN (Internationalized Domain Name).



<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Il nome specificato deve essere identico al nome del computer configurato nel server. Per impostazione predefinita, il nome di un computer non aggiunto a un dominio è un nome breve, non un nome di dominio completo (FQDN). Il Generatore di topologie usa i nomi di dominio completi, non i nomi brevi, pertanto è necessario aggiungere un suffisso DNS al nome di ogni computer non aggiunto a un dominio da distribuire come server perimetrale. Quando si assegnano i nomi di dominio completi dei server Lync, dei server perimetrali e dei pool è consigliabile <strong>usare solo i caratteri standard</strong> (inclusi i caratteri A-Z, a-z, 0-9 e i trattini). Non usare i caratteri Unicode e i caratteri di sottolineatura. I caratteri non standard di un FQDN spesso non sono supportati dal sistema DNS esterno e dalle CA pubbliche. Ciò accade quando l'FQDN deve essere assegnato al nome soggetto nel certificato.</td>
</tr>
</tbody>
</table>

