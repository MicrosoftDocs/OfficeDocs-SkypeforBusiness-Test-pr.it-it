---
title: 'Lync Server 2013: Rapporto Elenco errori'
TOCTitle: Rapporto Elenco errori
ms:assetid: b6f3a605-e0c6-461e-b17a-41d8039ace9d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615446(v=OCS.15)
ms:contentKeyID: 49301752
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rapporto Elenco errori in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Nel Rapporto Elenco errori vengono fornite informazioni sui singoli partecipanti che hanno preso parte a una sessione di conferenza o peer-to-peer in cui si sono verificati problemi. Tali informazioni includono l'URI dell'utente che ha riscontrato il problema, nonché il codice di risposta SIP e l'ID diagnostica associati all'errore.

## Accesso al Rapporto Elenco errori

È possibile accedere al Rapporto Elenco errori facendo clic su una qualsiasi delle metriche seguenti nel [Rapporto distribuzione errori in Lync Server 2013](lync-server-2013-failure-distribution-report.md):

  - Motivi diagnostica principali (sessioni)

  - Modalità principali (sessioni)

  - Pool principali (sessioni)

  - Origini principali (sessioni)

  - Componenti principali (sessioni)

  - Utenti di origine principali (sessioni)

  - Utenti di destinazione principali (sessioni)

  - Agenti utenti di origine principali (sessioni)

Dal Rapporto Elenco errori è possibile accedere al [Rapporto Dettagli sessione peer-to-peer in Lync Server 2013](lync-server-2013-peer-to-peer-session-detail-report.md) facendo clic sulla metrica Dettagli sessione per una sessione peer-to-peer. È inoltre possibile accedere al Rapporto Dettagli conferenza facendo clic sulla metrica Conferenza per una conferenza.

## Utilizzo ottimale del Rapporto Elenco errori

Nel Rapporto Elenco errori è possibile visualizzare una descrizione di ogni codice di risposta o di ogni ID diagnostica semplicemente posizionando il puntatore del mouse sul valore desiderato. Se ad esempio si posiziona il puntatore del mouse su Diagnostic ID 7025, in una descrizione comando verrà visualizzato quanto segue:

Internal server error creating media for user.

È importante notare che il Rapporto Elenco errori non consente di recuperare direttamente un elenco di tutti gli utenti che hanno partecipato ad almeno una sessione con problemi, né consente di determinare quali utenti hanno partecipato più spesso a una sessione con problemi. Tale rapporto innanzitutto non dispone di funzionalità di filtro. Se però i dati vengono esportati e convertiti in un file con valori delimitati da virgole, è possibile utilizzare Windows PowerShell per trovare le risposte a domande come queste. Si supponga ad esempio di salvare i dati in un file CSV denominato C:\\Data\\Failure\_List.csv. In base ai dati salvati in tale file, questo comando elencherà tutti gli utenti che hanno partecipato ad almeno una sessione con problemi:

    $failures = Import-Csv -Path " C:\Data\Failure_List.csv"
    $failure |Sort-Object "From user" | Select-Object "From user" -Unique

Tale comando restituirà un elenco simile al seguente:

    From user
    ----
    Pilar.Ackerman@litwareinc.com
    Henrik.Jensen@litwareinc.com
    Gilead.Amosnino@litwareinc.com
    David.Ahs@litwareinc.com
    Ken.Myer@litwareinc.com

Questi due comandi restituiscono il numero totale di sessioni con problemi a cui ha partecipato ogni utente:

    $failures = Import-Csv -Path "C:\Data\Failure_List.csv"
    $failures | Group-Object "From user" | Select-Object Count, Name | Sort-Object -Property Count -Descending

Verranno restituiti dati simili ai seguenti:

    Count    Name
     -----    ----
        20    Pilar.Ackerman@litwareinc.com
        20    David.Ahs@litwareinc.com
        16    Gilead.Amosnino@litwareinc.com
        16    Ken.Myero@litwareinc.com
        14    Henrik.Jensen@litwareinc.com

## Filtri

Nessuno. Non è possibile filtrare il Rapporto elenco errori.

## Metriche

Nella tabella seguente sono elencate le informazioni disponibili nel Rapporto elenco errori per ogni chiamata non riuscita.

### Metriche del Rapporto elenco errori

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
<td><p><strong>Ora rapporto</strong></p></td>
<td><p>No</p></td>
<td><p>Data e ora di registrazione del rapporto.</p></td>
</tr>
<tr class="even">
<td><p><strong>Richiesta</strong></p></td>
<td><p>No</p></td>
<td><p>Tipo di richiesta SIP non riuscita. Ad esempio, INVITE o BYE.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Codice di risposta</strong></p></td>
<td><p>No</p></td>
<td><p>Codice di risposta SIP inviato per la conferenza non riuscita.</p></td>
</tr>
<tr class="even">
<td><p><strong>ID diagnostica</strong></p></td>
<td><p>No</p></td>
<td><p>Identificatore univoco (in forma di intestazione ms-diagnostics) associato a un messaggio SIP che spesso fornisce informazioni utili per la risoluzione dei problemi e degli errori.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Tempo costo partecipazione (ms)</strong></p></td>
<td><p>No</p></td>
<td><p>Intervallo di tempo, in millisecondi, necessario all'utente per partecipare alla conferenza.</p></td>
</tr>
<tr class="even">
<td><p><strong>Da utente</strong></p></td>
<td><p>No</p></td>
<td><p>Indirizzo SIP dell'utente che ha avviato la chiamata.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Da agente utente</strong></p></td>
<td><p>No</p></td>
<td><p>Software utilizzato dall'endpoint dell'utente che ha avviato la chiamata.</p></td>
</tr>
<tr class="even">
<td><p><strong>A utente</strong></p></td>
<td><p>No</p></td>
<td><p>Indirizzo SIP dell'utente chiamato.</p></td>
</tr>
</tbody>
</table>

