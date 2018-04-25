---
title: 'Lync Server 2013: Panoramica dei tipi di indirizzi IP'
TOCTitle: Panoramica dei tipi di indirizzi IP per Lync Server
ms:assetid: ee9a695f-5cf5-441e-94fb-6adeca50e8d8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205363(v=OCS.15)
ms:contentKeyID: 49302386
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Panoramica dei tipi di indirizzi IP per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Quando si configurano gli indirizzi IP in Lync Server 2013 sono disponibili tre opzioni. È possibile configurare Lync Server 2013 in modo da supportare solo il protocollo IP versione 4 (IPv4), solo il protocollo IP versione 6 (IPv6) o una combinazione dei due (nota come *dual stack* ). Per ogni tipo di configurazione è necessario considerare diversi problemi:

  - **Solo IPv4**   IPv6 è stato creato perché la disponibilità mondiale di indirizzi IPv4 è in esaurimento. In futuro IPv6 sarà completamente supportato in tutto il mondo, ma al momento molte aziende e molti dispositivi con cui potrebbe essere necessario comunicare non lo supportano ancora. Con una configurazione Solo IPv4 è più probabile che l'implementazione di Lync Server possa comunicare con la maggior parte dei dispositivi esistenti.

  - **Solo IPv6**   Ad oggi, un'implementazione che supporta solo IPv6 non consentirebbe la comunicazione con molti dispositivi esistenti.

  - **Dual Stack**   Dual stack è una rete che supporta sia gli indirizzi IPv4 che gli indirizzi IPv6. Questa configurazione è supportata in Lync Server 2013 perché nella maggior parte dei casi la transizione dalla modalità IPv4 alla modalità IPv6 impiegherà diversi anni.

Nelle sezioni seguenti verrà esaminata la compatibilità di queste tre configurazioni con diverse caratteristiche di Lync Server.


> [!NOTE]
> La configurazione client o server con il solo protocollo IPv6 è supportata solo per fini di ricerca e di convalida. La configurazione Solo IPv6 non è supportata nella distribuzione di produzione.



## Registrazione client


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Rete endpoint client</th>
<th>Rete server</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IPv4</p></td>
<td><p>IPv4</p></td>
</tr>
<tr class="even">
<td><p>IPv4</p></td>
<td><p>Dual stack</p></td>
</tr>
<tr class="odd">
<td><p>Dual stack</p></td>
<td><p>IPv4</p></td>
</tr>
<tr class="even">
<td><p>Dual stack</p></td>
<td><p>Dual stack</p></td>
</tr>
<tr class="odd">
<td><p>Dual stack</p></td>
<td><p>IPv6</p></td>
</tr>
<tr class="even">
<td><p>IPv6</p></td>
<td><p>Dual stack</p></td>
</tr>
<tr class="odd">
<td><p>IPv6</p></td>
<td><p>IPv6</p></td>
</tr>
</tbody>
</table>


## Client peer-to-peer

La comunicazione peer-to-peer include audio, audio/video, condivisione di applicazioni e trasferimento di file. Dopo la corretta registrazione di entrambi i client, sono supportate le combinazioni seguenti.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Endpoint client 1</th>
<th>Endpoint client 2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IPv4</p></td>
<td><p>IPv4</p></td>
</tr>
<tr class="even">
<td><p>IPv4</p></td>
<td><p>Dual stack</p></td>
</tr>
<tr class="odd">
<td><p>Dual stack</p></td>
<td><p>Dual stack</p></td>
</tr>
<tr class="even">
<td><p>IPv6</p></td>
<td><p>Dual stack</p></td>
</tr>
<tr class="odd">
<td><p>IPv6</p></td>
<td><p>IPv6</p></td>
</tr>
</tbody>
</table>


## Servizi di conferenza

Servizi di conferenza include audio/video, condivisione di applicazioni e collaborazione dati (condivisione file e lavagna).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Rete endpoint client</th>
<th>Rete server</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IPv4</p></td>
<td><p>IPv4</p></td>
</tr>
<tr class="even">
<td><p>IPv4</p></td>
<td><p>Dual stack</p></td>
</tr>
<tr class="odd">
<td><p>Dual stack</p></td>
<td><p>IPv4</p></td>
</tr>
<tr class="even">
<td><p>Dual stack</p></td>
<td><p>Dual stack</p></td>
</tr>
<tr class="odd">
<td><p>Dual stack</p></td>
<td><p>IPv6</p></td>
</tr>
<tr class="even">
<td><p>IPv6</p></td>
<td><p>Dual stack</p></td>
</tr>
<tr class="odd">
<td><p>IPv6</p></td>
<td><p>IPv6</p></td>
</tr>
</tbody>
</table>


## Mediation Server/PSTN

Lync Server 2013 non supporta il bypass multimediale per le chiamate PSTN (Public Switched Telephone Network) se il traffico si sposta attraverso un'interfaccia IPv6. Se il bypass multimediale è necessario, è consigliabile configurare il gateway PSTN su IPv4.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Interfaccia principale*</th>
<th>Interfaccia PSTN (in Mediation Server)</th>
<th>Impostazioni del gateway PSTN</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IPv4</p></td>
<td><p>Dual stack</p></td>
<td><p>IPv4</p></td>
</tr>
<tr class="even">
<td><p>Dual stack</p></td>
<td><p>Dual stack</p></td>
<td><p>IPv4</p></td>
</tr>
<tr class="odd">
<td><p>Dual stack</p></td>
<td><p>Dual stack</p></td>
<td><p>IPv6</p></td>
</tr>
</tbody>
</table>


\* L'interfaccia principale è quella che comunica con i componenti di Lync Server.

## Comunicazioni peer-to-peer con utenti remoti

La comunicazione peer-to-peer con utenti remoti include messaggistica istantanea, audio/video, condivisione di applicazioni e trasferimento di file.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Rete utenti remoti</th>
<th>Server perimetrale (perimetro esterno)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IPv4</p></td>
<td><p>IPv4</p></td>
</tr>
<tr class="even">
<td><p>Dual stack</p></td>
<td><p>IPv4</p></td>
</tr>
<tr class="odd">
<td><p>Dual stack</p></td>
<td><p>Dual stack</p></td>
</tr>
<tr class="even">
<td><p>IPv6</p></td>
<td><p>Dual stack</p></td>
</tr>
<tr class="odd">
<td><p>IPv6</p></td>
<td><p>IPv6</p></td>
</tr>
</tbody>
</table>


## Configurazione di pool Front End e di pool di server perimetrali

Nella tabella seguente viene illustrata la matrice di supporto tra il pool Front End Server e il pool di server perimetrale interno.

### Matrice di pool Front End e di pool di server perimetrali (perimetro interno)

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p><strong>Pool di server perimetrali: IPv4</strong></p></td>
<td><p><strong>Pool di server perimetrali: Dual Stack</strong></p></td>
<td><p><strong>Pool di server perimetrali: IPv6</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>Pool Front End: IPv4</strong></p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p><strong>Pool Front End: Dual Stack</strong></p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p><strong>Pool Front End: IPv6</strong></p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>Sì*</p></td>
</tr>
</tbody>
</table>


\* Utilizzare questa combinazione solo in un ambiente lab.

La tabella seguente è una matrice delle combinazioni supportate di interfacce di server perimetrali interni ed esterni.

### Matrice di pool di server perimetrali (perimetro interno) e di pool di server perimetrali (perimetro esterno)

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p><strong>Pool di server perimetrali (perimetro esterno): IPv4</strong></p></td>
<td><p><strong>Pool di server perimetrali (perimetro esterno): Dual Stack</strong></p></td>
<td><p><strong>Pool di server perimetrali (perimetro esterno): IPv6</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>Pool di server perimetrali (perimetro interno): IPv4</strong></p></td>
<td><p>Sì</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p><strong>Pool di server perimetrali (perimetro interno): Dual Stack</strong></p></td>
<td><p>No</p></td>
<td><p>Sì</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p><strong>Pool di server perimetrali (perimetro interno): IPv6</strong></p></td>
<td><p>No</p></td>
<td><p>No</p></td>
<td><p>Sì*</p></td>
</tr>
</tbody>
</table>


\* Utilizzare questa combinazione solo in un ambiente lab.

## Supporto vocale aziendale avanzato per IPv6

Le distribuzioni che includono il servizio Controllo di ammissione di chiamata, Enhanced 9-1-1 (E9-1-1) o il bypass multimediale devono essere configurate come implementazioni Solo IPv4 o Dual Stack.


> [!NOTE]
> In una distribuzione Dual Stack, anche se un client Lync si connette a un Lync Server utilizzando IPv6, Lync tenterà di mappare un indirizzo IPv4 appropriato per supportare E9-1-1.



Il servizio Informazioni percorso con indirizzi IPv6 non è supportato.

La messaggistica unificata di Exchange non supporta IPv6. Per la messaggistica unificata di Exchange, assicurasi che la risoluzione DNS non restituisca un indirizzo IPv6. L'utilizzo di IPv6 può causare errori quando le chiamate vengono inviate alla segreteria telefonica.

## Supporto IPv6 in altre caratteristiche di Lync Server 2013

Oltre alle caratteristiche e ai componenti sopra menzionati, Lync Server 2013 supporta IPv6 per le seguenti caratteristiche:

  - **Chat persistente**
    
    Il protocollo IPv6 per la Chat persistente viene configurato utilizzando Generatore di topologie. Per informazioni dettagliate sulla configurazione della Chat persistente, vedere la documentazione relativa alla distribuzione del server chat persistente.

  - **Rapporti qualità percepita dagli utenti (QoE) e registrazione dettagli chiamata (CDR)**
    
    Le relazioni di monitoraggio includono l'indirizzo IP così com'è archiviato nel database di Monitoring Server, che sia di tipo IPv4 o IPv6.

