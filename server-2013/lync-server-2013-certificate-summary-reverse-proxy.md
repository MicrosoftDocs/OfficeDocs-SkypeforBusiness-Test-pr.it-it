---
title: 'Lync Server 2013: Riepilogo dei certificati - proxy inverso'
TOCTitle: Riepilogo dei certificati - proxy inverso
ms:assetid: f2b9a53f-aead-413d-81e9-4a294a010fbb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205381(v=OCS.15)
ms:contentKeyID: 49302440
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo dei certificati - proxy inverso in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

I requisiti relativi ai certificati per il proxy inverso sono molto più semplici rispetto a quelli per i server perimetrali. Il diagramma di flusso descrive i requisiti necessari. La tabella corrispondente illustra il nome soggetto del certificato e i nomi alternativi del soggetto in relazione agli scenari illustrati nelle informazioni sul server perimetrale. Per ulteriori informazioni sugli scenari del server perimetrale, vedere [Scenari per l'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-scenarios-for-external-user-access.md).

**Diagramma di flusso dei certificati per proxy inverso**

![Diagramma di flusso Certificati per Edge Server](images/JJ205381.026045d7-1b4b-4651-b32f-2d43a7161198(OCS.15).jpg "Diagramma di flusso Certificati per Edge Server")

### Proxy inverso: interfaccia esterna

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente</th>
<th>Nome soggetto</th>
<th>Ordine/nome alternativo soggetto (SAN)</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Proxy inverso</p></td>
<td><p>webext.contoso.com</p></td>
<td><p>webext.contoso.com</p>
<p>webdirext.contoso.com</p>
<p>dialin.contoso.com</p>
<p>meet.contoso.com</p>
<p>officewebapps01.contoso.com</p>
<p>lyncdiscover.contoso.com</p>
<p>(Facoltativo):*.contoso.com</p></td>
<td><p>Il certificato deve essere emesso da una CA pubblica e con utilizzo chiavi avanzato del server. I servizi includono Servizio Rubrica, espansione dei gruppi di distribuzione di Office Web Apps per conferenza e regole di pubblicazione dei dispositivi IP Lync. Il nome alternativo del soggetto include:</p>
<ul>
<li><p>FQDN servizi Web esterni per Front End Server o pool Front End</p></li>
<li><p>FQDN servizi Web esterni per Server Director o pool di server Director</p></li>
<li><p>Conferenza telefonica con accesso esterno</p></li>
<li><p>Regola di pubblicazione per riunioni online</p></li>
<li><p>Office Web Apps per conferenza</p></li>
<li><p>Lyncdiscover (individuazione automatica)</p></li>
</ul>
<p>Il carattere jolly facoltativo sostituisce il nome alternativo del soggetto meet e dialin</p></td>
</tr>
</tbody>
</table>

