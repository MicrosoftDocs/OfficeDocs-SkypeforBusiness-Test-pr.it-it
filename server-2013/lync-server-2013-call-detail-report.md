---
title: 'Lync Server 2013: Rapporto dettagli chiamata'
TOCTitle: Rapporto dettagli chiamata
ms:assetid: 38862e35-3fec-41b9-a035-0b301942d446
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558637(v=OCS.15)
ms:contentKeyID: 49300221
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rapporto dettagli chiamata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il Rapporto dettagli chiamata fornisce informazioni dettagliate su una chiamata singola. Il rapporto include quasi tutte le metriche e le statistiche QoE raccolte da Lync Server, suddivise in sezioni quali:

  - Informazioni chiamata

  - Metrica dispositivi e segnale chiamante

  - Metrica dispositivi e segnale destinatario chiamata

  - Evento client chiamante

  - Evento client destinatario chiamata

  - Flusso audio (da chiamante a destinatario chiamata)

  - Flusso video (da chiamante a destinatario chiamata)

  - Flusso audio (da destinatario chiamata a chiamante)

  - Flusso video (da destinatario chiamata a chiamante)

Tenere presente che le categorie e le metriche incluse in un rapporto specifico dipendono da due fattori: il tipo di sessione e il tipo di endpoint usato nella sessione. Ad esempio in una chiamata solo audio non saranno presenti metriche per i flussi video, in quanto la chiamata non presenta alcun flusso video. Analogamente, si potrebbe avere un rapporto in cui sono elencate statistiche del chiamante ma non del destinatario della chiamata. Questa situazione si verifica generalmente quando il destinatario della chiamata non usa un dispositivo compatibile con SIP. Gli endpoint sono responsabili della segnalazione delle statistiche alla fine di una chiamata, ma ad esempio un telefono cellulare (che non ha nulla a che vedere con SIP o statistiche SIP) non è in grado di produrre un rapporto su questo tipo di informazioni. Se si chiama qualcuno che risponde dal telefono cellulare, non verrà prodotto alcun rapporto da quel telefono al termine della chiamata.

Il Rapporto dettagli chiamata risulta utile soprattutto quando si prova a stabilire in modo preciso la causa dei problemi di qualità multimediale in una chiamata.

## Accesso al Rapporto dettagli chiamata

Si può accedere al Rapporto dettagli chiamata da uno dei rapporti seguenti:

  - [Rapporto percorsi in Lync Server 2013](lync-server-2013-location-report.md) (facendo clic sulla metrica Volume chiamata o Percentuale chiamate di livello insufficiente)

  - [Rapporto riepilogativo qualità multimediale in Lync Server 2013](lync-server-2013-media-quality-summary-report.md) (facendo clic sulla metrica Volume chiamata o Percentuale chiamate di livello insufficiente)

  - [Rapporto di confronto qualità multimediale in Lync Server 2013](lync-server-2013-media-quality-comparison-report.md) (facendo clic sul [Rapporto Elenco chiamate in Lync Server 2013](lync-server-2013-call-list-report.md), quindi sulla metrica Dettaglio).

  - [Rapporto prestazioni dei server in Lync Server 2013](lync-server-2013-server-performance-report.md) (facendo clic sulla metrica Volume chiamata o Percentuale chiamate di livello insufficiente)

  - [Rapporto Elenco chiamate in Lync Server 2013](lync-server-2013-call-list-report.md) (facendo clic sulla metrica Dettaglio)

Dal Rapporto dettagli chiamata è possibile accedere al [Rapporto dispositivi in Lync Server 2013](lync-server-2013-device-report.md) facendo clic su una delle metriche seguenti:

  - Dispositivo di acquisizione

  - Dispositivo di rendering

È inoltre possibile accedere al Rapporto tendenze qualità multimediale server facendo clic sulla metrica A/V Edge Server.

## Utilizzo ottimale del Rapporto dettagli chiamata

Il Rapporto dettagli chiamata include generalmente oltre 250 metriche diverse, tra cui Deviazione timestamp microfono, Tempo rapporto segnale/rumore basso e Tempo rapporto segnale near-end/eco. Se non si ricorda la misura effettiva di tutte queste metriche, provare a posizionare il mouse sull'etichetta della metrica per visualizzare un a descrizione comando della metrica.

In caso di problemi nell'individuazione di una metrica, digitare parte dell'etichetta della metrica nella casella di ricerca e fare clic su Trova. Se ad esempio non si riesce a trovare la metrica Tempo rapporto segnale/rumore basso, digitare SNR nella casella di ricerca e fare clic su Trova.

Si noti che questo rapporto tiene traccia solo delle informazioni su una chiamata. La chiamata in quanto tale non viene registrata.

## Filtri

Nessuno. Non è possibile applicare filtri nel Rapporto dettagli chiamata.

## Metriche

Nella tabella riportata di seguito vengono elencate le informazioni fornite nel Rapporto dettagli chiamata per ogni chiamata.

### Metrica del Rapporto dettagli chiamata

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>Elemento utilizzabile per eseguire l'ordinamento?</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>PAI chiamante</strong></p></td>
<td><p>No</p></td>
<td><p>PAI (P-Asserted-Identity) dell'utente che ha avviato la chiamata. Questo valore viene utilizzato per trasmettere l'identità comprovata di un utente in una rete attendibile.</p></td>
</tr>
<tr class="even">
<td><p><strong>URI chiamante</strong></p></td>
<td><p>No</p></td>
<td><p>Indirizzo SIP dell'utente che ha avviato la chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Endpoint chiamante</strong></p></td>
<td><p>No</p></td>
<td><p>Dispositivo utilizzato per effettuare la chiamata.</p></td>
</tr>
<tr class="even">
<td><p><strong>Agente utente chiamante</strong></p></td>
<td><p>No</p></td>
<td><p>Software utilizzato nel dispositivo con cui è stata effettuata la chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Inizio chiamata</strong></p></td>
<td><p>No</p></td>
<td><p>Data e ora di inizio della chiamata.</p></td>
</tr>
<tr class="even">
<td><p><strong>Chiamata di bypass a Mediation Server</strong></p></td>
<td><p>No</p></td>
<td><p>Indica l'eventuale connessione della chiamata a un gateway vocale PSTN o IP-PBX qualificato senza passare attraverso il Mediation Server.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Sistema operativo chiamante</strong></p></td>
<td><p>No</p></td>
<td><p>Sistema operativo del computer del chiamante.</p></td>
</tr>
<tr class="even">
<td><p><strong>CPU chiamante</strong></p></td>
<td><p>No</p></td>
<td><p>CPU installata nel computer dell'utente che ha avviato la chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Numero di core CPU chiamante</strong></p></td>
<td><p>No</p></td>
<td><p>Numero di processori nel computer utilizzato dalla persona che ha avviato la chiamata.</p></td>
</tr>
<tr class="even">
<td><p><strong>Velocità CPU chiamante</strong></p></td>
<td><p>No</p></td>
<td><p>Velocità di clock della CPU del computer utilizzato dalla persona che ha avviato la chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Virtualizzazione CPU chiamante</strong></p></td>
<td><p>No</p></td>
<td><p>Eventuale virtualizzazione nel computer utilizzato dalla persona che ha avviato la chiamata.</p></td>
</tr>
<tr class="even">
<td><p><strong>PAI destinatario chiamata</strong></p></td>
<td><p>No</p></td>
<td><p>PAI (P-Asserted-Identity) dell'utente che ha inviato l'invito a partecipare alla chiamata. Questo valore viene utilizzato per trasmettere l'identità comprovata di un utente in una rete attendibile.</p></td>
</tr>
<tr class="odd">
<td><p><strong>URI destinatario chiamata</strong></p></td>
<td><p>No</p></td>
<td><p>Indirizzo SIP dell'utente chiamato.</p></td>
</tr>
<tr class="even">
<td><p><strong>Endpoint destinatario chiamata</strong></p></td>
<td><p>No</p></td>
<td><p>Dispositivo utilizzato per ricevere la chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Agente utente destinatario chiamata</strong></p></td>
<td><p>No</p></td>
<td><p>Software utilizzato nel dispositivo con cui è stata ricevuta la chiamata.</p></td>
</tr>
<tr class="even">
<td><p><strong>Durata</strong></p></td>
<td><p>No</p></td>
<td><p>Durata della chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Flag di avviso bypass multimediale</strong></p></td>
<td><p>No</p></td>
<td><p>Avviso generato quando è stato ignorato il Mediation Server.</p></td>
</tr>
<tr class="even">
<td><p><strong>Sistema operativo destinatario chiamata</strong></p></td>
<td><p>No</p></td>
<td><p>Sistema operativo del computer dell'utente chiamato.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CPU destinatario chiamata</strong></p></td>
<td><p>No</p></td>
<td><p>CPU installata nel computer dell'utente chiamato.</p></td>
</tr>
<tr class="even">
<td><p><strong>Numero di core CPU destinatario chiamata</strong></p></td>
<td><p>No</p></td>
<td><p>Numero di processori nel computer utilizzato dalla persona chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Velocità CPU destinatario chiamata</strong></p></td>
<td><p>No</p></td>
<td><p>Velocità di clock della CPU del computer utilizzato dalla persona chiamata.</p></td>
</tr>
<tr class="even">
<td><p><strong>Virtualizzazione CPU destinatario chiamata</strong></p></td>
<td><p>No</p></td>
<td><p>Eventuale virtualizzazione nel computer utilizzato dalla persona chiamata.</p></td>
</tr>
</tbody>
</table>

