---
title: Eventi UCWA
TOCTitle: Eventi UCWA
ms:assetid: 26cb409d-f4e4-43c7-873f-b694702d491d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945621(v=OCS.15)
ms:contentKeyID: 52062121
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eventi UCWA

 

_**Ultima modifica dell'argomento:** 2015-03-09_

    The information in this topic pertains to Cumulative Updates for Lync Server 2013: February 2013.

Lync Server 2013 utilizza l'API Web Unified Communications (UCWA) per vari scopi, dall'accesso a Microsoft Exchange per cercare i contatti all'aggiornamento della presenza per i client dei dispositivi mobili.

UCWA scriverà i record del comportamento operativo come eventi di tipo informativo, avviso ed errore. Nella tabella seguente vengono descritti gli eventi che possono essere scritti dai componenti UCWA.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>ID evento</th>
<th>Tipo di evento</th>
<th>Riepilogo</th>
<th>Causa e soluzione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>20001</p></td>
<td><p>Informativo</p></td>
<td><p>UCWA inizializzato</p></td>
<td><p>N/D</p>
<p>N/D</p></td>
</tr>
<tr class="even">
<td><p>20002</p></td>
<td><p>Errore</p></td>
<td><p>UCWA ha rilevato un'eccezione imprevista durante l'inizializzazione</p></td>
<td><p>Si è verificato un errore imprevisto durante l'inizializzazione</p>
<p>Esaminare i dettagli dell'eccezione nella voce del registro eventi associata per determinare la possibile causa</p></td>
</tr>
<tr class="odd">
<td><p>20003</p></td>
<td><p>Errore</p></td>
<td><p>UCWA ha rilevato un'eccezione non gestita</p></td>
<td><p>Si è verificata un'eccezione non gestita</p>
<p>Riavviare il server. Se il problema persiste, contattare il Servizio Supporto Tecnico Clienti Microsoft.</p></td>
</tr>
<tr class="even">
<td><p>20004</p></td>
<td><p>Errore</p></td>
<td><p>Impossibile accedere a Exchange per la foto ad alta definizione</p></td>
<td><p>La connessione a Exchange non è disponibile</p>
<p>Verificare che la connessione a Exchange sia disponibile</p></td>
</tr>
<tr class="odd">
<td><p>20005</p></td>
<td><p>Informativo</p></td>
<td><p>Recupero dall'errore di accesso ad Exchange per la foto ad alta definizione completato</p></td>
<td><p>N/D</p></td>
</tr>
<tr class="even">
<td><p>20006</p></td>
<td><p>Errore</p></td>
<td><p>Impossibile accedere a Exchange per la ricerca di contatti</p></td>
<td><p>La connessione a Exchange non è disponibile</p>
<p>Verificare che la connessione a Exchange sia disponibile</p></td>
</tr>
<tr class="odd">
<td><p>20007</p></td>
<td><p>Informativo</p></td>
<td><p>Recupero dall'errore di ricerca dei contatti in Exchange completato</p></td>
<td><p>N/D</p></td>
</tr>
<tr class="even">
<td><p>20008</p></td>
<td><p>Avviso</p></td>
<td><p>Tentativo di eseguire sottoscrizioni superiori al limite di sottoscrizioni relative alla presenza consentito per applicazione</p></td>
<td><p>Tentativo di eseguire sottoscrizioni superiori al limite di sottoscrizioni relative alla presenza consentito per applicazione</p>
<p>Controllare le sottoscrizioni non necessarie nei client</p></td>
</tr>
<tr class="odd">
<td><p>20009</p></td>
<td><p>Avviso</p></td>
<td><p>Tentativo di eseguire sottoscrizioni superiori al limite di sottoscrizioni relative alla presenza consentito per batch</p></td>
<td><p>Tentativo di eseguire sottoscrizioni superiori al limite di sottoscrizioni relative alla presenza consentito per batch</p>
<p>Controllare le sottoscrizioni non necessarie nei client</p></td>
</tr>
<tr class="even">
<td><p>20010</p></td>
<td><p>Errore</p></td>
<td><p>Impossibile recuperare i dati in banda</p></td>
<td><p>Impossibile recuperare i dati in banda</p>
<p>Se il problema persiste, contattare il Servizio Supporto Tecnico Clienti Microsoft.</p></td>
</tr>
<tr class="odd">
<td><p>20011</p></td>
<td><p>Errore</p></td>
<td><p>Impossibile eseguire la sottoscrizione della presenza</p></td>
<td><p>Non è possibile eseguire la sottoscrizione della presenza</p>
<p>Se il problema persiste, contattare il Servizio Supporto Tecnico Clienti Microsoft.</p></td>
</tr>
<tr class="even">
<td><p>20012</p></td>
<td><p>Errore</p></td>
<td><p>Non è possibile registrare l'endpoint</p></td>
<td><p>Impossibile registrare l'endpoint</p>
<p>Se il problema persiste, contattare il Servizio Supporto Tecnico Clienti Microsoft.</p></td>
</tr>
<tr class="odd">
<td><p>20013</p></td>
<td><p>Errore</p></td>
<td><p>Il servizio MCU dei messaggi istantanei non è disponibile</p></td>
<td><p>Il servizio MCU dei messaggi istantanei non è disponibile</p>
<p>Verificare che il servizio MCU dei messaggi istantanei sia in esecuzione</p></td>
</tr>
<tr class="even">
<td><p>20014</p></td>
<td><p>Informativo</p></td>
<td><p>Recupero dall'errore di connessione al servizio MCU dei messaggi istantanei completato</p></td>
<td><p>N/D</p></td>
</tr>
<tr class="odd">
<td><p>20015</p></td>
<td><p>Errore</p></td>
<td><p>Il servizio MCU AV non è disponibile</p></td>
<td><p>Il servizio MCU AV non è disponibile</p>
<p>Verificare che il servizio MCU AV sia in esecuzione</p></td>
</tr>
<tr class="even">
<td><p>20016</p></td>
<td><p>Informativo</p></td>
<td><p>Recupero dall'errore di connessione al servizio MCU AV completato</p></td>
<td><p>N/D</p></td>
</tr>
<tr class="odd">
<td><p>20017</p></td>
<td><p>Errore</p></td>
<td><p>Il servizio MCU AS non è disponibile</p></td>
<td><p>Il servizio MCU AS non è disponibile</p>
<p>Verificare che il servizio MCU AS sia in esecuzione</p></td>
</tr>
<tr class="even">
<td><p>20018</p></td>
<td><p>Informativo</p></td>
<td><p>Recupero dall'errore di connessione al servizio MCU AS completato</p></td>
<td><p>N/D</p></td>
</tr>
<tr class="odd">
<td><p>20019</p></td>
<td><p>Errore</p></td>
<td><p>Il servizio MCU dati non è disponibile</p></td>
<td><p>Il servizio MCU dati non è disponibile</p>
<p>Verificare che il servizio MCU dati sia in esecuzione</p></td>
</tr>
<tr class="even">
<td><p>20020</p></td>
<td><p>Informativo</p></td>
<td><p>Recupero dall'errore di connessione al servizio MCU dati completato</p></td>
<td><p>N/D</p></td>
</tr>
<tr class="odd">
<td><p>20021</p></td>
<td><p>Errore</p></td>
<td><p>Impossibile partecipare al servizio MCU dei messaggi istantanei</p></td>
<td><p>Impossibile partecipare al servizio MCU dei messaggi istantanei</p>
<p>Verificare che il servizio MCU dei messaggi istantanei sia in esecuzione</p></td>
</tr>
<tr class="even">
<td><p>20022</p></td>
<td><p>Errore</p></td>
<td><p>Impossibile partecipare al servizio MCU AV</p></td>
<td><p>Impossibile partecipare al servizio MCU AV</p>
<p>Verificare che il servizio MCU AV sia in esecuzione</p></td>
</tr>
<tr class="odd">
<td><p>20023</p></td>
<td><p>Errore</p></td>
<td><p>Impossibile partecipare al servizio MCU AS</p></td>
<td><p>Impossibile partecipare al servizio MCU AS</p>
<p>Verificare che il servizio MCU AS sia in esecuzione</p></td>
</tr>
<tr class="even">
<td><p>20024</p></td>
<td><p>Errore</p></td>
<td><p>Impossibile partecipare al servizio MCU dati</p></td>
<td><p>Impossibile partecipare al servizio MCU dati</p>
<p>Verificare che il servizio MCU dati sia in esecuzione</p></td>
</tr>
<tr class="odd">
<td><p>20025</p></td>
<td><p>Errore</p></td>
<td><p>Impossibile accedere ad Active Directory per la foto</p></td>
<td><p>La connessione ad Active Directory non è disponibile</p>
<p>Verificare che la connessione ad Active Directory sia disponibile</p></td>
</tr>
<tr class="even">
<td><p>20026</p></td>
<td><p>Informativo</p></td>
<td><p>Recupero dall'errore di accesso ad Active Directory per la foto completato</p></td>
<td><p>N/D</p></td>
</tr>
<tr class="odd">
<td><p>20027</p></td>
<td><p>Avviso</p></td>
<td><p>Impossibile deserializzare</p></td>
<td><p>Impossibile deserializzare</p>
<p>Se il problema persiste, contattare il Servizio Supporto Tecnico Clienti Microsoft.</p></td>
</tr>
</tbody>
</table>

