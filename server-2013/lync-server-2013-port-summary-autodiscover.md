---
title: Riepilogo porte - Individuazione automatica in Lync Server 2013
TOCTitle: Riepilogo porte - Individuazione automatica in Lync Server 2013
ms:assetid: 8bd16363-5e18-4e4b-be99-b3e6457b4c99
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945642(v=OCS.15)
ms:contentKeyID: 52062195
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Riepilogo porte - Individuazione automatica in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il servizio di individuazione automatica di Lync Server 2013 viene eseguito nei server Director e pool Front End e, se pubblicato in DNS tramite i record host `lyncdiscover.<domain>` e `lyncdiscoverinternal.<domain>`, può essere utilizzato dai client per individuare le funzionalità di Lync Server. Affinché i dispositivi mobili che eseguono Lync Mobile possano utilizzare il servizio di individuazione automatica, è innanzitutto necessario modificare gli elenchi di nomi alternativi soggetto in qualsiasi Server Director e Front End Server che esegue il servizio di individuazione automatica. Potrebbe essere inoltre necessario modificare gli elenchi di nomi alternativi soggetto nei certificati utilizzati per le regole di pubblicazione dei servizi Web esterni nei proxy inversi.

La decisione relativa all'utilizzo degli elenchi dei nomi alternativi del soggetto nei proxy inversi dipende dal fatto che il servizio di individuazione automatica venga pubblicato sulla porta 80 o sulla porta 443:

  - **Pubblicato sulla porta 80**   Per i dispositivi mobili non sono necessarie modifiche relative ai certificati se la query iniziale inviata al servizio di individuazione automatica avviene sulla porta 80. Questo è dovuto al fatto che i dispositivi mobili che eseguono Lync accederanno al proxy inverso sulla porta 80 esternamente e quindi verranno reindirizzati a un Server Director o a un Front End Server sulla porta 8080 internamente.

  - **Pubblicato sulla porta 443**   L'elenco dei nomi alternativi soggetto nei certificati utilizzati dalla regola di pubblicazione dei servizi Web esterni deve contenere una voce `lyncdiscover.<sipdomain>` per ogni dominio SIP all'interno dell'organizzazione.
    
    > [!important]  
    > Per le nuove installazioni o gli aggiornamenti da Lync Server 2010 in cui si distribuisce il servizio Mobility, è possibile scegliere di utilizzare la porta 80 per l'individuazione automatica del servizio Mobility oppure di riemettere i certificati con il nome soggetto e i nomi alternativi soggetto appropriati. Controllare i certificati nel Server Director e nel Front End Server per verificare quale dei due percorsi è stato scelto.

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
<td><p>(Facoltativo) Reindirizzamento a HTTPS se l'utente immette http://<em>&lt;FQDNsitopubblicato&gt;</em>. Necessario inoltre se si utilizza Office Web Apps per le conferenze e il servizio di individuazione automatica per i dispositivi mobili che eseguono Lync in situazioni in cui l'organizzazione non desidera modificare il certificato nella regola di pubblicazione dei servizi Web esterni.</p></td>
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
<td><p>Front End Server, pool Front End, Server Director, pool di server Director, Office Web Apps per le conferenze</p></td>
<td><p>Necessario se si utilizza il servizio di individuazione automatica per i dispositivi mobili che eseguono Lync nei casi in cui l'organizzazione non desidera modificare il certificato nella regola di pubblicazione dei servizi Web esterni. Il traffico inviato alla porta 80 nell'interfaccia esterna del proxy inverso viene reindirizzato a un pool sulla porta 8080 dall'interfaccia interna del proxy inverso, in modo che i servizi Web del pool possano distinguerlo dal traffico Web interno.</p></td>
</tr>
<tr class="even">
<td><p>HTTPS/TCP/4443</p></td>
<td><p>Interfaccia interna del proxy inverso</p></td>
<td><p>Front End Server, pool Front End, Server Director, pool di server Director, Office Web Apps per le conferenze</p></td>
<td><p>Il traffico inviato alla porta 443 nell'interfaccia esterna del proxy inverso viene reindirizzato a un pool sulla porta 4443 dall'interfaccia interna del proxy inverso, in modo che i servizi Web del pool possano distinguerlo dal traffico Web interno.</p></td>
</tr>
</tbody>
</table>

