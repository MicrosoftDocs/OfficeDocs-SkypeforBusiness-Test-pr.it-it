---
title: Rapporto Dettagli conferenza
TOCTitle: Rapporto Dettagli conferenza
ms:assetid: 1d61cd81-dcfe-40b4-9a41-a73b038bc216
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204728(v=OCS.15)
ms:contentKeyID: 49299868
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rapporto Dettagli conferenza

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il Rapporto Dettagli conferenza offre informazioni dettagliate su tutti gli utenti che hanno partecipato a una conferenza. È ad esempio possibile conoscere la data e l'ora in cui un utente si è unito alla conferenza o in cui l'ha abbandonata e l'agente utente dell'endpoint utilizzato per connettere tale utente alla conferenza. È anche possibile visualizzare informazioni sul ruolo dell'utente in ciascuna conferenza (relatore o partecipante). E ancora più importante, è possibile sapere rapidamente quali utenti si sono uniti alla conferenza e l'hanno completata e quali non ci sono riusciti.

## Accesso al Rapporto Dettagli conferenza

Il Rapporto Dettagli conferenza è accessibile dai rapporti seguenti:

  - [Rapporto controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-call-admission-control-report.md) (facendo clic sulla metrica Dettaglio per una conferenza)

  - [Rapporto Elenco errori in Lync Server 2013](lync-server-2013-failure-list-report.md) (facendo clic sulla metrica Conferenza)

  - [Rapporto attività utente in Lync Server 2013](lync-server-2013-user-activity-report.md) (facendo clic sulla metrica URI conferenza)

Dal Rapporto Dettagli conferenza è possibile accedere al [Rapporto di diagnostica in Lync Server 2013](lync-server-2013-diagnostic-report.md) facendo clic sulla metrica Rapporto di diagnostica (Dettaglio).

## Filtri

Nessuno. Non è possibile applicare filtri al Rapporto Dettagli conferenza.

## Metriche

La tabella seguente elenca le informazioni contenute nella sezione Informazioni conferenza del Rapporto Dettagli conferenza.

### Metriche Informazioni conferenza

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>È possibile effettuare l'ordinamento in base a questo elemento?</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>URI conferenza</strong></p></td>
<td><p></p></td>
<td><p>URI assegnato alla conferenza, ad esempio:</p>
<p>sip:kmyer@litwareinc.com;gruu;opaque=app:conf:focus:id:drg2y8v4</p></td>
</tr>
<tr class="even">
<td><p><strong>FQDN pool</strong></p></td>
<td><p></p></td>
<td><p>Nome di dominio completo del pool di registrazione o del server perimetrale operativo in una sessione.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Ora di inizio</strong></p></td>
<td><p></p></td>
<td><p>Data e ora di inizio della conferenza.</p></td>
</tr>
<tr class="even">
<td><p><strong>Organizzatore</strong></p></td>
<td><p></p></td>
<td><p>Indirizzo SIP dell'utente che ha organizzato la conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Ora di fine</strong></p></td>
<td><p></p></td>
<td><p>Data e ora di fine della conferenza.</p></td>
</tr>
</tbody>
</table>


La tabella seguente elenca le informazioni fornite nella sezione Partecipazione conferenza del Rapporto Dettagli conferenza.

### Metriche di Partecipazione conferenza

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>È possibile effettuare l'ordinamento in base a questo elemento?</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Utente</strong></p></td>
<td><p></p></td>
<td><p>Indirizzo SIP dell'utente che ha partecipato alla conferenza.</p></td>
</tr>
<tr class="even">
<td><p><strong>Ruolo</strong></p></td>
<td><p></p></td>
<td><p>Ruolo, ad esempio Relatore, ricoperto dal partecipante alla conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Connettività</strong></p></td>
<td><p></p></td>
<td><p>Connettività di rete, solitamente Dall'interno o Dall'esterno, per il partecipante.</p></td>
</tr>
<tr class="even">
<td><p>Ora partecipazione</p></td>
<td><p></p></td>
<td><p>Data e ora in cui il partecipante si è unito alla conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Ora uscita</strong></p></td>
<td><p></p></td>
<td><p>Data e ora in cui il partecipante è uscito dalla conferenza.</p></td>
</tr>
<tr class="even">
<td><p><strong>Agente utente</strong></p></td>
<td><p></p></td>
<td><p>Identificatore del software utilizzato dall'endpoint del partecipante.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Rapporti di diagnostica</strong></p></td>
<td><p></p></td>
<td><p>Contiene informazioni relative alla diagnostica e alla risoluzione dei problemi, tra cui codici di risposta SIP, intestazioni di diagnostica, ore di partecipazione alla conferenza e ID diagnostica per le sessioni non riuscite.</p></td>
</tr>
</tbody>
</table>


La tabella seguente elenca le informazioni contenute nella sezione Modalità conferenza del Rapporto Dettagli conferenza.

### Metriche di Modalità conferenza

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Nome</th>
<th>È possibile effettuare l'ordinamento in base a questo elemento?</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Utente</strong></p></td>
<td><p></p></td>
<td><p>Indirizzo SIP dell'utente che ha partecipato alla conferenza.</p></td>
</tr>
<tr class="even">
<td><p><strong>Ora partecipazione</strong></p></td>
<td><p></p></td>
<td><p>Data e ora in cui il partecipante si è unito alla conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Ora uscita</strong></p></td>
<td><p></p></td>
<td><p>Data e ora in cui un partecipante è uscito dalla conferenza.</p></td>
</tr>
<tr class="even">
<td><p><strong>URI server per conferenze</strong></p></td>
<td><p></p></td>
<td><p>URI per il server per conferenze utilizzato nella conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Rapporti di diagnostica</strong></p></td>
<td><p></p></td>
<td><p>Contiene informazioni relative alla diagnostica e alla risoluzione dei problemi, tra cui codici di risposta SIP, intestazioni di diagnostica, ore di partecipazione alla conferenza e ID diagnostica per le sessioni non riuscite.</p></td>
</tr>
</tbody>
</table>

