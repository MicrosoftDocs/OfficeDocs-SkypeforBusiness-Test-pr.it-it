---
title: Panoramica del routing in base alla posizione per le conferenze
TOCTitle: Panoramica del routing in base alla posizione per le conferenze
ms:assetid: 8b86740e-db95-4304-bb83-64d0cbb91d47
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362815(v=OCS.15)
ms:contentKeyID: 56269937
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Panoramica del routing in base alla posizione per le conferenze

 

_**Ultima modifica dell'argomento:** 2015-03-09_

L'applicazione per conferenze con routing in base alla posizione offre un meccanismo per impedire il bypass delle chiamate a tariffa PSTN nelle conferenze Lync. L'applicazione monitora le conferenze attive e applica le limitazioni del routing in base alla posizione in funzione dell'ubicazione degli utenti Lync partecipanti.

Questa applicazione determina se a una riunione Lync vanno applicate le limitazioni del routing in base alla posizione se sono soddisfatti i criteri seguenti:

  - L'organizzatore del meeting è abilitato per il routing in base alla posizione. Le limitazioni del routing in base alla posizione verranno applicate solo alle conferenze organizzate da utenti abilitati per tale funzionalità.

  - Almeno un partecipante alla riunione è un endpoint PSTN. Le limitazioni del routing in base alla posizione sono applicabili solo alle conferenze che includono endpoint PSTN.

  - Il sito di rete in cui si trova il gateway PSTN usato per il bridging della conferenza al PSTN è lo stesso da cui si connettono gli organizzatori e i partecipanti.

L'applicazione per conferenze con routing in base alla posizione impedisce la partecipazione alla stessa conferenza di utenti Lync ed endpoint PSTN provenienti da siti diversi. Se l'organizzatore di una riunione è abilitato per il routing in base alla posizione, l'applicazione impone le limitazioni seguenti:

  - Gli endpoint che possono partecipare a una riunione Lync dipendono dagli endpoint che si sono già uniti alla conferenza. La limitazione si adatta in base agli endpoint che abbandonano la conferenza e ai nuovi endpoint che vi si uniscono. Se organizzatori e partecipanti si uniscono a una riunione Lync dallo stesso sito di rete, sarà consentito l'accesso anche a un endpoint PSTN, a un altro partecipante dallo stesso sito di rete, un altro partecipante da un sito di rete diverso o un partecipante da un sito di rete sconosciuto.

  - Se organizzatori e partecipanti si uniscono alla riunione Lync da siti di rete diversi o sconosciuti, non sarà consentito l'accesso a un PSTN se la chiamata PSTN effettua l'ingresso da un trunk SIP abilitato per il routing in base alla posizione.

  - Se organizzatori e partecipanti si uniscono alla riunione Lync dallo stesso sito di rete e vi sono partecipanti che accedono alla stessa riunione dalla rete PSTN, non sarà consentito l'accesso a un endpoint Lync proveniente da un sito di rete diverso.

Le limitazioni per le conferenze imposte dal routing in base alla posizione sono riepilogate nella tabella seguente.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Utenti presenti in una conferenza in uno specifico momento</p></td>
<td><p>Utenti autorizzati a partecipare alla conferenza</p></td>
<td><p>Utenti non autorizzati a partecipare alla conferenza</p></td>
</tr>
<tr class="even">
<td><p>Utenti del client VoIP Lync da un unico sito di rete</p></td>
<td><p>Utente del client VoIP Lync dallo stesso sito di rete</p>
<p>Utente del client VoIP Lync da un diverso sito di rete</p>
<p>Utente del client VoIP Lync da un sito di rete sconosciuto</p>
<p>Utente del client VoIP Lync federato</p>
<p>Utente che partecipa tramite un endpoint PSTN</p></td>
<td><p>Nessuno</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Utenti del client VoIP Lync da un sito di rete sconosciuto</p></td>
<td><p>Utente del client VoIP Lync da qualsiasi sito</p>
<p>Utente del client VoIP Lync da un sito sconosciuto</p>
<p>Utente del client VoIP Lync federato</p></td>
<td><p>Utente che partecipa tramite un endpoint PSTN</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>Utenti del client VoIP Lync da siti di rete diversi</p></td>
<td><p>Utente del client VoIP Lync da qualsiasi sito di rete</p>
<p>Utente del client VoIP Lync da un sito di rete sconosciuto</p>
<p>Utente del client VoIP Lync federato</p></td>
<td><p>Utente che partecipa tramite un endpoint PSTN</p></td>
</tr>
<tr class="odd">
<td><p>Utenti del client VoIP Lync da un unico sito di rete e utenti che si uniscono da un endpoint PSTN</p></td>
<td><p>Utente del client VoIP Lync dallo stesso sito di rete</p>
<p></p></td>
<td><p>Utente del client VoIP Lync da un diverso sito di rete</p>
<p>Utente del client VoIP Lync da un sito di rete sconosciuto</p>
<p>Utente del client VoIP Lync federato</p></td>
</tr>
</tbody>
</table>


Di seguito sono illustrate alcune caratteristiche aggiuntive dell'applicazione per conferenze con routing in base alla posizione:

  - Quando un utente non è autorizzato a partecipare a una conferenza in base alle limitazioni del routing in base alla posizione, la chiamata alla conferenza da parte dell'utente verrà rifiutata e il client Lync segnalerà che la chiamata non è stata completata o è terminata.

  - A un endpoint PSTN che si unisce a una conferenza in cui sono applicate le limitazioni del routing in base alla posizione non verrà impedito di partecipare alla conferenza, indipendentemente dallo stato, se partecipa da un trunk non abilitato per il routing in base alla posizione.

  - A un sistema PBX connesso a un Mediation Server tramite un trunk SIP che non invia le chiamate alla rete PSTN saranno applicate le stesse regole valide per gli utenti Lync situati nello stesso sito di rete in cui è definito il trunk SIP. Ad esempio, un endpoint PSTN potrà partecipare a una conferenza con un utente PBX e un utente Lync se questi si trovano nello stesso sito di rete. Il contrario, se l'utente PBX si trova in un sito di rete diverso rispetto all'utente Lync, all'endpoint PSTN non sarà consentito l'accesso alla conferenza.

