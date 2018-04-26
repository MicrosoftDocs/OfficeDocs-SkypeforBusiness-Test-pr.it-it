---
title: Riepilogo di DNS - connettività per messaggistica istantanea pubblica
TOCTitle: Riepilogo di DNS - connettività per messaggistica istantanea pubblica
ms:assetid: ddf42a25-5ac4-4643-a10a-9fbd433fc2d2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ618375(v=OCS.15)
ms:contentKeyID: 49302210
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo di DNS - connettività per messaggistica istantanea pubblica

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Quando si configura DNS (Domain Name System) per la connettività per messaggistica istantanea pubblica, la configurazione che supporta gli utenti esterni supporterà la connettività per messaggistica istantanea pubblica. Se è stato già configurato il server perimetrale o il pool di server perimetrali, dovrebbero essere disponibili i record DNS necessari per supportare la connettività per messaggistica istantanea pubblica.

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
<th>Mapping a/Commenti</th>
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

#### Concetti

[Scenari per l'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-scenarios-for-external-user-access.md)

