---
title: Riepilogo dei certificati - connettività per messaggistica istantanea pubblica
TOCTitle: Riepilogo dei certificati - connettività per messaggistica istantanea pubblica
ms:assetid: 2b3687ee-50c2-4c1c-880e-8dcf8bd4f309
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ618370(v=OCS.15)
ms:contentKeyID: 49300019
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo dei certificati - connettività per messaggistica istantanea pubblica

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per configurare i certificati per la connettività per la messaggistica istantanea pubblica, è innanzitutto necessario osservare che non ci sono differenze rispetto ad altri tipi di federazione SIP o certificati del server perimetrale standard, con l'unica eccezione che America Online (AOL) richiede la configurazione di un certificato univoco. Oltre al normale utilizzo chiavi avanzato (EKU, Enhanced Key Usage) del server, America Online richiede che il certificato o i certificati (in presenza di un pool di server perimetrali) contengano anche l'EKU del client, ovvero un'integrazione al certificato che fa parte del certificato pubblico esterno assegnato al server perimetrale.

## Riepilogo dei certificati - Connettività per la messaggistica istantanea pubblica


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
<th>Nomi alternativi soggetto (SAN)/Ordine</th>
<th>Commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Esterno/Access Edge</p></td>
<td><p>sip.contoso.com</p></td>
<td><p>sip.contoso.com</p>
<p>webcon.contoso.com</p>
<p>sip.fabrikam.com</p></td>
<td><p>Il certificato deve essere stato emesso da un'autorità di certificazione pubblica e deve includere l'EKU del server e del client se si intende distribuire la connettività per la messaggistica istantanea pubblica con AOL. Il certificato viene assegnato alle interfacce del server perimetrale esterno per:</p>
<ul>
<li><p>servizio Access Edge</p></li>
<li><p>servizio Web Conferencing Edge</p></li>
<li><p>servizio A/V Edge</p></li>
</ul>
<p>Tenere presente che i nomi SAN vengono aggiunti automaticamente al certificato in base alle definizioni presenti nel Generatore di topologie. Le voci SAN vengono aggiunte se necessario per domini SIP aggiuntivi e altre voci da supportare. Il nome soggetto viene replicato nel nome SAN e deve essere presente per garantire un corretto funzionamento.</p></td>
</tr>
</tbody>
</table>


## Vedere anche

#### Concetti

[Scenari per l'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-scenarios-for-external-user-access.md)

