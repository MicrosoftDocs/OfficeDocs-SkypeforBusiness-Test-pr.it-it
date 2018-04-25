---
title: 'Lync Server 2013: Processo di distribuzione per il routing in base alla posizione'
TOCTitle: Processo di distribuzione per il routing in base alla posizione
ms:assetid: 9e923e72-83fc-4a4f-8937-28a55739ed3e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994055(v=OCS.15)
ms:contentKeyID: 52062257
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Processo di distribuzione per il routing in base alla posizione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

In questo argomento viene fornita una panoramica del processo di configurazione del routing in base alla posizione. Prima di eseguire questo processo, è necessario distribuire Lync ServerEnterprise Edition o Standard Edition con VoIP aziendale. I componenti richiesti dal routing in base alla posizione sono già installati e abilitati quando di distribuisce VoIP aziendale.

### Processo di distribuzione per il routing in base alla posizione

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Fase</th>
<th>Passaggi</th>
<th>Gruppi e ruoli obbligatori</th>
<th>Documentazione relativa alla distribuzione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Distribuire VoIP aziendale</p></td>
<td><ul>
<li><p>Configurare i trunk</p></li>
<li><p>Creare criteri vocali</p></li>
<li><p>Definire route vocali</p></li>
</ul></td>
<td><p>CSVoiceAdmins<br />
CsAdministrator<br />
CsServerAdministrator</p></td>
<td><p>Distribuzione di VoIP aziendale</p></td>
</tr>
<tr class="even">
<td><p>Verificare la distribuzione di VoIP aziendale</p></td>
<td><p></p></td>
<td><p>CSVoiceAdmins<br />
CsAdministrator<br />
CsServerAdministrator</p></td>
<td> </td>
</tr>
<tr class="odd">
<td><p>Configurare aree, siti e subnet di rete</p></td>
<td><ul>
<li><p>Creare aree di rete</p></li>
<li><p>Creare siti di rete</p></li>
<li><p>Associare subnet a siti di rete</p></li>
</ul></td>
<td><p>CSVoiceAdmins<br />
CsAdministrator<br />
CsServerAdministrator</p></td>
<td><p>Informazioni su aree di rete, siti e subnet<br />
Creare o modificare un'area di rete<br />
Creare o modificare un sito di rete<br />
Associare una subnet a un sito di rete</p></td>
</tr>
<tr class="even">
<td><p>Configurare il routing in base alla posizione</p></td>
<td><ul>
<li><p>Creare criteri di routing vocale</p></li>
<li><p>Definire una configurazione separata per ogni trunk</p></li>
<li><p>Modificare i criteri vocali</p></li>
<li><p>Abilitare la configurazione del routing in base alla posizione</p></li>
</ul></td>
<td><p>CSVoiceAdmins<br />
CsAdministrator<br />
CsServerAdministrator</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Esempio di distribuzione

La distribuzione seguente è utile per illustrare ulteriormente i meccanismi abilitati dal routing in base alla posizione.

![Topologia di routing in base alla posizione](images/JJ994055.e1bd2230-44da-4784-b359-24572b6ce02d(OCS.15).png "Topologia di routing in base alla posizione")

## Chiamate PSTN in arrivo

L'amministratore può abilitare il trunk definito per instradare le chiamate al gateway del sito 1 per il routing in base alla posizione e associare tale gateway al sito 1. Dopo l'abilitazione, le chiamate instradate tramite il gateway del sito 1 verranno instradate solo agli utenti che si trovano nel sito 1. Tutte le chiamate instradate tramite il trunk del gateway del sito 1 destinate a utenti in un sito diverso, ad esempio il sito 2, verranno bloccate per evitare il bypass delle chiamate a tariffa PSTN.

Tutte le chiamate PSTN in arrivo tramite il gateway del sito 1 potranno essere instradate solo agli endpoint situati nel sito 1. Se ad esempio l'utente Lync 1 si sposta nel sito 2, tutte le chiamate PSTN in arrivo tramite il gateway del sito 1 non verranno instradate agli endpoint dell'utente Lync 1 che si trova nel sito 2. La stessa regola si applica se l'utente Lync 1 si sposta in un sito di rete sconosciuto in cui non è possibile determinarne la posizione.

Nella tabella seguente viene illustrata l'esperienza dell'utente Lync 1 in questo contesto.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Endpoint dell'utente Lync 1 situati nel sito di rete 1</th>
<th>Endpoint dell'utente Lync 1 situati nel sito di rete 2</th>
<th>Endpoint dell'utente Lync 1 situati in un sito di rete sconosciuto</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Chiamate PSTN in arrivo all'utente Lync 1</p></td>
<td><p>Le chiamate vengono instradate agli endpoint in questa posizione</p></td>
<td><p>Le chiamate non vengono instradate agli endpoint in questa posizione</p></td>
<td><p>Le chiamate non vengono instradate agli endpoint in questa posizione</p></td>
</tr>
</tbody>
</table>


## Chiamate PSTN in uscita

Alle route vocali viene fatto riferimento sia nei criteri vocali assegnati direttamente agli utenti sia nei criteri di routing vocale assegnati ai siti di rete. Entrambi i criteri contengono riferimenti alle route, che possono essere utilizzate per instradare una chiamata in modo diverso. L'amministratore può ad esempio definire criteri di routing vocale per tutti gli utenti situati nel sito di rete 1 in modo da instradare tutte le chiamate in uscita tramite il gateway del sito 1, mentre i criteri vocali di alcuni utenti definiscono una route per tutte le chiamate in uscita tramite il gateway del sito 2. Quando questi utenti si trovano nel sito di rete 1, le loro chiamate in uscita verranno instradate tramite il gateway del sito 1.

Se un utente si trova in un sito di rete configurato per il routing in base alla posizione, la route dei criteri di routing vocale del sito di rete ha la precedenza sulla route dei criteri vocali dell'utente. Questa regola è particolarmente utile per gli utenti che si spostano temporaneamente in un sito diverso. In questo caso specifico, un utente utilizzerà sempre un gateway locale rispetto alla sua posizione. Se l'utente Lync 3 si trova nel sito 2, tutte le sue chiamate in uscita verranno instradate tramite il gateway del sito 2, ma se si sposta nel sito 1 tutte le chiamate in uscita effettuate mentre si trova in questo sito verranno instradate tramite il gateway del sito 1.

Nella tabella seguente viene illustrata l'esperienza dell'utente Lync 1 che effettua una chiamata in uscita dai siti di rete seguenti.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Sito di rete 1</th>
<th>Sito di rete 2</th>
<th>Sito di rete sconosciuto o non abilitato per il routing in base alla posizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Autorizzazione delle chiamate in uscita</p></td>
<td><p>Criteri vocali utente Lync 1</p></td>
<td><p>Criteri vocali utente Lync 1</p></td>
<td><p>Criteri vocali utente Lync 1</p></td>
</tr>
<tr class="even">
<td><p>Routing delle chiamate in uscita</p></td>
<td><p>Criteri di routing vocale sito 1</p></td>
<td><p>Criteri di routing vocale sito 2</p></td>
<td><p>Criteri vocali dell'utente e solo per i sistemi non abilitati per il routing in base alla posizione</p></td>
</tr>
</tbody>
</table>


## Trasferimento e inoltro di chiamate

Il routing in base alla posizione influisce sulle chiamate trasferite o inoltrate.

Nella tabella seguente viene illustrato l'utente Lync 1 che trasferisce o inoltra una chiamata PSTN a un altro utente Lync.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Utente che avvia il trasferimento o l'inoltro della chiamata</th>
<th>Utente Lync 2</th>
<th>Utente Lync 4</th>
<th>Utente Lync in un sito di rete non abilitato per il routing in base alla posizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utente Lync 1</p></td>
<td><p>L'inoltro o il trasferimento della chiamata è consentito</p></td>
<td><p>L'inoltro o il trasferimento della chiamata non è consentito</p></td>
<td><p>L'inoltro o il trasferimento della chiamata non è consentito</p></td>
</tr>
</tbody>
</table>

  
Nella tabella seguente vengono illustrati gli effetti del routing in base alla posizione sul modo in cui viene instradata la chiamata in base alla posizione dell'utente Lync da trasferire (utente Lync 2, utente Lync 4 e così via) in un endpoint PSTN


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Endpoint in cui viene trasferita o inoltrata la chiamata</th>
<th>Utente Lync 2</th>
<th>Utente Lync 4</th>
<th>Utente Lync in un sito di rete non abilitato per il routing in base alla posizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Endpoint PSTN</p></td>
<td><p>L'inoltro o il trasferimento della chiamata viene instradato attraverso il gateway del sito 1 tramite i criteri di routing vocale del sito 1</p></td>
<td><p>L'inoltro o il trasferimento della chiamata viene instradato attraverso il gateway del sito 2 tramite i criteri di routing vocale del sito 2</p></td>
<td><p>L'inoltro o il trasferimento della chiamata viene instradato attraverso un gateway non abilitato per il routing in base alla posizione (se disponibile) tramite i criteri vocali dell'utente Lync</p></td>
</tr>
</tbody>
</table>


## Squillo simultaneo

Dopo la configurazione del routing in base alla posizione nella topologia di esempio, vengono applicate le interazioni seguenti.

Nella tabella seguente viene illustrato se il routing in base alla posizione consente o meno lo squillo simultaneo tra diversi utenti Lync, ossia utente Lync 2, utente Lync 4 e così via.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Destinazione chiamata PSTN in arrivo</th>
<th>Utente Lync 2</th>
<th>Utente Lync 4</th>
<th>Utente Lync in un sito di rete non abilitato per il routing in base alla posizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Utente Lync 1</p></td>
<td><p>Squillo simultaneo consentito</p></td>
<td><p>Squillo simultaneo non consentito</p></td>
<td><p>Squillo simultaneo non consentito</p></td>
</tr>
</tbody>
</table>

  
Nella tabella seguente viene illustrato se il routing in base alla posizione consente o meno lo squillo simultaneo in un endpoint PSTN da diversi utenti Lync, ossia utente Lync 2, utente Lync 4 e così via.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Destinazione squillo simultaneo</th>
<th>Utente Lync 2</th>
<th>Utente Lync 4</th>
<th>Utente Lync in un sito di rete non abilitato per il routing in base alla posizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cellulare (endpoint PSTN) dell'utente Lync 1</p></td>
<td><p>La chiamata viene instradata attraverso il gateway del sito 1 tramite i criteri di routing vocale del sito 1</p></td>
<td><p>La chiamata viene instradata attraverso il gateway del sito 2 tramite i criteri di routing vocale del sito 2</p></td>
<td><p>La chiamata viene instradata attraverso un gateway PSTN non abilitato per il routing in base alla posizione tramite i criteri vocali del chiamante</p></td>
</tr>
</tbody>
</table>


## Vedere anche

#### Ulteriori risorse

[Pianificazione del routing in base alla posizione in Lync Server 2013](lync-server-2013-planning-for-location-based-routing.md)

