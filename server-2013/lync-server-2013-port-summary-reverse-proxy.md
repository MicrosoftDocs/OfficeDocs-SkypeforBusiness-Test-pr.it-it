---
title: 'Lync Server 2013: Riepilogo delle porte - proxy inverso'
TOCTitle: Riepilogo delle porte - proxy inverso
ms:assetid: 59b9ac3c-3e6f-4776-b366-174f0dd1f2eb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204932(v=OCS.15)
ms:contentKeyID: 49300640
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo delle porte - proxy inverso in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per il proxy inverso sono previsti requisiti minimi per il firewall, la porta e il protocollo.

  - I requisiti per il firewall esterno sono HTTPS/TCP/443 e l'impostazione facoltativa HTTP/TCP/80. HTTPS viene utilizzato per le comunicazioni sicure SSL e TLS tramite il proxy inverso. HTTP viene utilizzato se si sceglie di consentire l'accesso al servizio di individuazione automatica quando la modifica dei certificati potrebbe risultare difficoltosa o i costi correlati non sono giustificati.

  - I client si aspettano di contattare Server Office Web Apps tramite HTTPS. Server Office Web Apps si aspetta le comunicazioni dai client interni su HTTPS/TCP/443. La configurazione consigliata prevede di consentire HTTPS/TCP/443 dal proxy inverso a Server Office Web Apps.

  - La porta 8080 è utilizzata per instradare il traffico dall'interfaccia interna del proxy inverso al Front End Server, all'indirizzo IP virtuale (VIP, Virtual IP Address) del pool Front End oppure all'indirizzo VIP del Server Director o del pool di server Director facoltativo. La porta 8080 è obbligatoria per i dispositivi mobili che eseguono Lync per rilevare il servizio di individuazione automatica nei casi in cui la modifica del certificato della regola di pubblicazione su servizio Web esterno non è appropriata, ad esempio se è presente un numero elevato di domini SIP. Se si sceglie di acquisire nuovi certificati con le voci SAN necessarie, la porta TCP 8080 non è necessaria ed è facoltativa.

  - La porta 4443 è usata per instradare il traffico dall'interfaccia interna del proxy inverso al Front End Server, all'indirizzo IP virtuale (VIP) del pool Front End oppure all'indirizzo VIP del Server Director o del pool di server Director facoltativo.
    
    ![Proxy inverso e servizi Web esterni](images/JJ204932.13142405-d5c9-45b7-a8b7-a8c89f09c97c(OCS.15).jpg "Proxy inverso e servizi Web esterni")  
    
    > [!Caution]  
    > Non confondere la porta 4443 su TCP dal proxy inverso alla distribuzione interna con il traffico della porta 4443 su TCP dal server Standard Edition al pool Front End che gestisce il ruolo archivio di gestione centrale.

## Informazioni dettagliate relative a porta e protocollo

### Dettagli del firewall per il server proxy inverso: interfaccia esterna

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Protocollo/TCP o UDP/porta</th>
<th>Indirizzo IP di origine</th>
<th>Indirizzo IP di destinazione</th>
<th>Note</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>HTTP/TCP/80</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Listener proxy inverso</p></td>
<td><p>(Facoltativo) Reindirizzamento a HTTPS se l'utente immette http:// <em>&lt;FQDNsitopubblicato&gt;</em> .</p>
<p>Necessario inoltre se si utilizza Office Web Apps per le conferenze e il servizio di individuazione automatica per i dispositivi mobili che eseguono Lync in situazioni in cui l'organizzazione non desidera modificare il certificato nella regola di pubblicazione dei servizi Web esterni.</p></td>
</tr>
<tr class="even">
<td><p>HTTPS/TCP/443</p></td>
<td><p>Qualsiasi</p></td>
<td><p>Listener proxy inverso</p></td>
<td><p>Download della Rubrica, servizio query Web della Rubrica, individuazione automatica, aggiornamenti client, contenuto delle riunioni, aggiornamenti dei dispositivi, espansione dei gruppi, Office Web Apps per le conferenze, conferenze telefoniche con accesso esterno e riunioni.</p></td>
</tr>
</tbody>
</table>


### Dettagli del firewall per il server proxy inverso: interfaccia interna

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Protocollo/TCP o UDP/porta</th>
<th>Indirizzo IP di origine</th>
<th>Indirizzo IP di destinazione</th>
<th>Note</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>HTTP/TCP/8080</p></td>
<td><p>Interfaccia interna del proxy inverso</p></td>
<td><p>Front End Server, pool Front End, Server Director, pool di server Director</p></td>
<td><p>Necessario se si utilizza il servizio di individuazione automatica per i dispositivi mobili che eseguono Lync nei casi in cui l'organizzazione non desidera modificare il certificato nella regola di pubblicazione dei servizi Web esterni.</p>
<p>Il traffico inviato alla porta 80 nell'interfaccia esterna del proxy inverso viene reindirizzato a un pool sulla porta 8080 dall'interfaccia interna del proxy inverso, in modo che i servizi Web del pool possano distinguerlo dal traffico Web interno.</p></td>
</tr>
<tr class="even">
<td><p>HTTPS/TCP/4443</p></td>
<td><p>Interfaccia interna del proxy inverso</p></td>
<td><p>Front End Server, pool Front End, Server Director, pool di server Director</p></td>
<td><p>Il traffico inviato alla porta 443 nell'interfaccia esterna del proxy inverso viene reindirizzato a un pool sulla porta 4443 dall'interfaccia interna del proxy inverso, in modo che i servizi Web del pool possano distinguerlo dal traffico Web interno.</p></td>
</tr>
<tr class="odd">
<td><p>HTTPS/TCP/443</p></td>
<td><p>Interfaccia interna del proxy inverso</p></td>
<td><p>Office Web Apps per conferenza</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>

