---
title: 'Lync Server 2013: Riepilogo di DNS - proxy inverso'
TOCTitle: Riepilogo di DNS - proxy inverso
ms:assetid: 3073affa-4d92-4453-9974-3a82ca0c6445
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204781(v=OCS.15)
ms:contentKeyID: 49300085
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo di DNS - proxy inverso in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

È possibile configurare due schede di rete all'interno del proxy inverso in questo modo:

## Requisiti relativi alla scheda di rete per proxy inverso

  - Esempio di **scheda di rete 1 (interfaccia interna)**
    
    Interfaccia interna con indirizzo 172.25.33.40 assegnato.
    
    Nessun gateway predefinito definito.
    
    Verificare che esista una route dalla rete in cui si trova l'interfaccia interna del proxy inverso alle reti in cui sono presenti server per pool Front End di Lync Server, ad esempio da 172.25.33.0 a 192.168.10.0.

  - Esempio di **scheda di rete 2 (interfaccia esterna)**
    
    A questa scheda di rete viene assegnato almeno un indirizzo IP pubblico.
    
    Il gateway viene definito in modo da puntare al router o al firewall integrato nel perimetro esterno (10.45.16.1 in questi esempi di scenario).

### Record DNS necessari per il proxy inverso

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
<th>Indirizzo IP</th>
<th>Mapping/commenti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DNS/A esterno</p></td>
<td><p>webext.contoso.com</p></td>
<td><p>Listener assegnato per risorse pubblicate esternamente</p></td>
<td><p>Servizi Web esterni dalla distribuzione interna. È possibile definire e creare altri record per tutti i pool e singoli server per un dominio SIP che userà questo proxy inverso e dispone di servizi Web esterni definiti.</p></td>
</tr>
<tr class="even">
<td><p>DNS/A esterno</p></td>
<td><p>webdirext.contoso.com</p></td>
<td><p>Listener assegnato per risorse pubblicate esternamente</p></td>
<td><p>Servizi Web esterni per i Director o i pool di Server Director all'interno della distribuzione. È possibile definire qualsiasi numero di Director perché si tratta di Director distinti, associabili ad altri domini SIP.</p>

> [!IMPORTANT]
> La definizione dei record DNS e la pubblicazione dei Director non è una decisione che spetta al pool Front End né al Server Director. Se si usano i Director, è necessario definire e pubblicare sia il Server Director che i servizi Web esterni del pool Front End. Tipi di traffico specifici (per l'autenticazione e altri usi) verranno inviati prima al Server Director, se definito nella topologia.

</td>
</tr>
<tr class="odd">
<td><p>DNS/A esterno</p></td>
<td><p>dialin.contoso.com</p></td>
<td><p>Listener assegnato per risorse pubblicate esternamente</p></td>
<td><p>Conferenza telefonica con accesso remoto pubblicata esternamente</p></td>
</tr>
<tr class="even">
<td><p>DNS/A esterno</p></td>
<td><p>meet.contoso.com</p></td>
<td><p>Listener assegnato per risorse pubblicate esternamente</p></td>
<td><p>Conferenze pubblicate esternamente</p></td>
</tr>
<tr class="odd">
<td><p>DNS/A esterno</p></td>
<td><p>officewebapps01.contoso.com</p></td>
<td><p>Listener assegnato per Server Office Web Apps</p></td>
<td><p>Server Office Web Apps distribuito internamente o nel perimetro e pubblicato per l'accesso client esterno</p></td>
</tr>
<tr class="even">
<td><p>DNS/A esterno</p></td>
<td><p>lyncdiscover.contoso.com</p></td>
<td><p>Listener assegnato per risorse pubblicate esternamente</p></td>
<td><p>Record esterno della funzione di individuazione di Lync per l'individuazione automatica pubblicata esternamente; include Dispositivi mobili, Microsoft Lync Web App e un'applicazione Web per la pianificazione</p></td>
</tr>
</tbody>
</table>

