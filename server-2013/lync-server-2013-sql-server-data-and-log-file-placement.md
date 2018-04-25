---
title: 'Lync Server 2013: Posizionamento dei file di log e dei file di dati di SQL Server'
TOCTitle: Posizionamento dei file di log e dei file di dati di SQL Server
ms:assetid: 67aa525b-8aa3-474f-827e-8e1d4697f30f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398479(v=OCS.15)
ms:contentKeyID: 49300833
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Posizionamento dei file di log e dei file di dati di SQL Server per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Durante la pianificazione e la distribuzione di Microsoft SQL Server 2012 o Microsoft SQL Server 2008 R2 SP1 per il  pool Front End di Lync Server 2013, un aspetto importante da considerare è il posizionamento dei dati e dei file di log nei dischi rigidi fisici per le prestazioni. La configurazione dei dischi consigliata prevede l'implementazione di un set 1+0 RAID con 6 assi. Il posizionamento di tutti i database e tutti i file di log utilizzati dal pool Front End e dai ruoli server e servizi associati (ovvero Server di archiviazione e Monitoring Server, Lync Server, Response Group Service, servizio Parcheggio di chiamata di Lync Server) nel set di unità RAID tramite il Distribuzione guidata di Lync Server consentirà di ottenere una configurazione testata per offrire buone prestazioni. I file di database e i loro scopi sono descritti in dettagli nella tabella seguente.


> [!NOTE]
> Se i criteri e le configurazioni di SQL Server specifici rendono necessaria un'installazione più specialistica, i database e i file di log possono essere installati in qualsiasi posizione predefinite tramite Lync Server Management Shell. Per ulteriori dettagli, vedere <A href="lync-server-2013-database-installation-using-lync-server-management-shell.md">Installazione di database mediante Lync Server Management Shell in Lync Server 2013</A>.



### File di dati e di log per l'archivio di gestione centrale

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>File di database dell' archivio di gestione centrale</th>
<th>Scopi del file di dati o di log</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Xds.ldf</p></td>
<td><p>File di log delle transazioni per l' archivio di gestione centrale</p></td>
</tr>
<tr class="even">
<td><p>Xds.mdf</p></td>
<td><p>Mantiene la configurazione della topologia di Lync Server 2013 corrente, come definita e pubblicata da Generatore di topologie</p></td>
</tr>
<tr class="odd">
<td><p>Lis.mdf</p></td>
<td><p>File di dati del servizio Informazioni percorso</p></td>
</tr>
<tr class="even">
<td><p>Lis.ldf</p></td>
<td><p>Log delle transazioni per il file di dati del servizio Informazioni percorso</p></td>
</tr>
</tbody>
</table>


### File di dati e di log per utenti, conferenze e Rubrica

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>File di database principali di Lync Server 2013</th>
<th>Scopi del file di dati o di log</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Rtc.mdf</p></td>
<td><p>Dati utente permanenti, ad esempio elenchi di controllo di accesso (ACL), contatti e conferenze pianificate</p></td>
</tr>
<tr class="even">
<td><p>Rtc.ldf</p></td>
<td><p>Log delle transazioni per i dati Rtc</p></td>
</tr>
<tr class="odd">
<td><p>Rtcdyn.mdf</p></td>
<td><p>Contiene i dati utente temporanei (dati di runtime sulla presenza)</p></td>
</tr>
<tr class="even">
<td><p>Rtcdyn.ldf</p></td>
<td><p>Log delle transazioni per i dati Rtcdyn</p></td>
</tr>
<tr class="odd">
<td><p>Rtcab.mdf</p></td>
<td><p>Il database della rubrica per la comunicazione in tempo reale è l'archivio di SQL Server in cui sono memorizzate le informazioni per il servizio Rubrica</p></td>
</tr>
<tr class="even">
<td><p>Rtcab.ldf</p></td>
<td><p>Log delle transazioni per il servizio Rubrica</p></td>
</tr>
<tr class="odd">
<td><p>Rtclocal.mdb</p></td>
<td><p>Ospita la directory conferenze</p></td>
</tr>
<tr class="even">
<td><p>Rtcxds.mdf</p></td>
<td><p>Gestisce il backup per i dati utente</p></td>
</tr>
<tr class="odd">
<td><p>Rtcxds.ldf</p></td>
<td><p>Log delle transazioni per dati Rtcxds</p></td>
</tr>
</tbody>
</table>


### File di dati e di log per Parcheggio di chiamata e Response Group

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>database applicazione</th>
<th>Scopi del file di dati o di log</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cpsdyn.mdf</p></td>
<td><p>Database di informazioni dinamiche per l' applicazione Parcheggio di chiamata</p></td>
</tr>
<tr class="even">
<td><p>Cpsdyn.ldf</p></td>
<td><p>Log delle transazioni per il file di dati dell' applicazione Parcheggio di chiamata</p></td>
</tr>
<tr class="odd">
<td><p>Rgsconfig.mdf</p></td>
<td><p>File di dati del servizio Response Group di Lync Server per la configurazione dei servizi</p></td>
</tr>
<tr class="even">
<td><p>Rgsconfig.ldf</p></td>
<td><p>File di log delle transazioni per la configurazione dell' applicazione Response Group</p></td>
</tr>
<tr class="odd">
<td><p>Rgsdyn.mdf</p></td>
<td><p>File di dati del servizio Response Group per le operazioni di runtime</p></td>
</tr>
<tr class="even">
<td><p>Rgsdyn.ldf</p></td>
<td><p>Log delle transazioni per il file di dati del runtime del servizio Response Group</p></td>
</tr>
</tbody>
</table>


### File di dati e di log per il server di archiviazione e Monitoring Server

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>File dei database di archiviazione e monitoraggio</th>
<th>Scopi del file di dati o di log</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>LcsCdr.mdf</p></td>
<td><p>Archivio dati per il processo di registrazione dettagli chiamata del Monitoring Server</p></td>
</tr>
<tr class="even">
<td><p>LcsCdr.ldf</p></td>
<td><p>Log delle transazioni per i dati di registrazione dettagli chiamata</p></td>
</tr>
<tr class="odd">
<td><p>QoEMetrics.mdf</p></td>
<td><p>File di dati QoE archiviato dal Monitoring Server</p></td>
</tr>
<tr class="even">
<td><p>QoEMetrics.ldf</p></td>
<td><p>Log delle transazioni per i dati di monitoraggio</p></td>
</tr>
<tr class="odd">
<td><p>Lcslog.mdf</p></td>
<td><p>File di dati per il mantenimento dei dati relativi a messaggistica istantanea e conferenze in un server di archiviazione</p></td>
</tr>
<tr class="even">
<td><p>Lcslog.ldf</p></td>
<td><p>Log delle transazioni per l'archiviazione dei dati</p></td>
</tr>
</tbody>
</table>


In questo argomento si fa riferimento a set di dischi e RAID. Si noti che per la configurazione delle risorse di SQL Server, i riferimenti a un disco indicano un singolo dispositivo hardware. Un'unità disco rigido con due partizioni, una per i file di log e l'altra per i file di dati, non equivale a due dischi ognuno dedicato ai file di log o ai file di dati.

Per quanto riguarda i set RAID, esistono numerose tecnologie RAID diverse da vari fornitori. Con la proliferazione delle reti SAN (Storage Area Network), inoltre, i set RAID dedicati a un singolo sistema sono più rari. È consigliabile consultarsi con il fornitore dei sistemi RAID o SAN per determinare la configurazione ottimale per il layout dei dischi, durante la configurazione del sistema per le prestazioni di SQL Server con Lync Server 2013.

Si noti inoltre che non tutte le unità disco vengono create in modo uguale e alcune offrono prestazioni migliori di altre. Anche unità dello stesso produttore possono offrire prestazioni variabili a seconda di velocità di rotazione, dimensioni della cache hardware e altri fattori.

