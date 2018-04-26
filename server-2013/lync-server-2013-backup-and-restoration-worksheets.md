---
title: Fogli di lavoro per il backup e il ripristino
TOCTitle: Fogli di lavoro per il backup e il ripristino
ms:assetid: 26c78155-0306-41ac-845b-7ad58000a1d6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh202169(v=OCS.15)
ms:contentKeyID: 52062116
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Fogli di lavoro per il backup e il ripristino

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il piano di backup e ripristino dell'organizzazione deve includere informazioni dettagliate su come e quando eseguire il backup dei dati e delle impostazioni. È possibile utilizzare i fogli di lavoro illustrati in questa sezione per prendere nota di queste informazioni per la propria distribuzione specifica e dei requisiti di backup e ripristino dell'organizzazione.

Utilizzare i fogli di lavoro seguenti per prendere nota delle informazioni necessarie per il backup e il ripristino dei dati relativi ai database, all'Archivio file e alle impostazioni di un pool di Lync Server o di un server Standard Edition. Conservare una o più copie di questi fogli di lavoro in un luogo sicuro in modo che siano immediatamente accessibili qualora sia necessario ripristinare Lync Server.


> [!NOTE]
> Nei fogli di lavoro di questa sezione si tiene conto solo delle informazioni necessarie per ripristinare i dati e le impostazioni dei database e dei server Lync Server. Se è necessario prendere nota di altre informazioni per il ripristino, ad esempio le informazioni per la reinstallazione dei sistemi operativi o di altro software, utilizzare i piani di distribuzione e i piani di backup e ripristino dell'organizzazione per tali requisiti.



## Foglio di lavoro per il backup e il ripristino dei database

Utilizzare la tabella seguente per prendere nota delle informazioni necessarie per il backup e il ripristino dei database di Lync Server.

### Informazioni dei database per il backup e il ripristino

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Database</th>
<th>Nome server (FQDN)</th>
<th>Pianificazione backup</th>
<th>Strumento di backup dei database</th>
<th>Set di backup</th>
<th>Destinazione backup</th>
<th>Note</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Database Rtc nel server back-end per i dati utente</p></td>
<td><p>                    </p></td>
<td><p>                    </p></td>
<td><p>Cmdlet <strong>Export-CsUserData</strong></p></td>
<td><p>Nome:</p>
<p>Scadenza:</p>
<p>                   </p></td>
<td><p>                    </p></td>
<td><p>                    </p></td>
</tr>
<tr class="even">
<td><p>Database LcsLog (nome predefinito) nel server di database di archiviazione</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>Strumento di gestione di SQL Server</p></td>
<td><p>Nome:</p>
<p>Scadenza:</p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>Database LcsCdr nel server di database di monitoraggio di registrazione dettagli chiamata (CDR)</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>Strumento di gestione di SQL Server</p></td>
<td><p>Nome:</p>
<p>Scadenza:</p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>Database QoEMetrics nel server di database di monitoraggio per dati di qualità percepita dagli utenti (QoE)</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>Strumento di gestione di SQL Server</p></td>
<td><p>Nome:</p>
<p>Scadenza:</p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>Database chat persistente</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>Strumento di gestione di SQL Server o cmdlet <strong>Export-CsPersistentChatData</strong></p></td>
<td><p>Nome:</p>
<p>Scadenza:</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


Non è necessario alcun backup o ripristino dei database seguenti:

  - Rtcdyn. I dati utente temporanei contenuti in questo database non sono necessari per il ripristino del servizio.

  - Rtcab. Il database della Rubrica viene ricreato automaticamente dall'Elenco indirizzi globale in Servizi di dominio Active Directory.

  - Rgsdyn. I dati utente temporanei di Response Group Service non sono necessari per il ripristino del servizio.

  - Cpsdyn. Le informazioni dinamiche per l'applicazione Parcheggio di chiamata non sono necessarie per il ripristino del servizio.

  - MgcComp. Il database di conformità per Chat persistente non è necessario per ripristinare il servizio.

## Foglio di lavoro per il backup e il ripristino degli archivi file

Utilizzare la tabella seguente per prendere nota delle informazioni necessarie per il backup e il ripristino degli archivi file. In questi archivi sono contenuti dati quali metadati del contenuto delle riunioni, log di conformità delle riunioni, log di aggiornamento per gli aggiornamenti dei dispositivi e file audio per le applicazioni Response Group, Parcheggio di chiamata e Annuncio.

### Informazioni degli archivi file per il backup e il ripristino

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Contenuto</th>
<th>Nome server (FQDN)</th>
<th>Pianificazione backup</th>
<th>Strumento di backup del file system</th>
<th>Condivisione file di cui eseguire il backup *</th>
<th>Destinazione backup</th>
<th>Note</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Archivio file di Lync Server</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>Strumento di backup standard, ad esempio Robocopy </p></td>
<td><p>In file server per Enterprise Edition. Per impostazione predefinita, nei server Standard Edition per la distribuzione di server Standard Edition. In genere ne esiste uno per sito.</p></td>
<td><p></p></td>
<td><p>Non eseguire il backup dei file denominati <strong>Meeting.Active</strong>. Questi file sono in uso e bloccati mentre è in corso una riunione.</p></td>
</tr>
</tbody>
</table>


## Foglio di lavoro per il backup e il ripristino delle impostazioni

Utilizzare la tabella seguente per prendere nota delle informazioni necessarie per il backup e il ripristino delle impostazioni.

### Informazioni delle impostazioni per il backup e il ripristino

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Database</th>
<th>Nome server (FQDN)</th>
<th>Pianificazione backup</th>
<th>Strumento di backup</th>
<th>Nome file di configurazione (xml)</th>
<th>Percorso backup</th>
<th>Note</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Database Xds nell'archivio di gestione centrale per la configurazione della topologia (globale)</p></td>
<td><p>                    </p></td>
<td><p>                    </p></td>
<td><p>Cmdlet <strong>Export-CsConfiguration</strong></p></td>
<td><p>                   </p></td>
<td><p>                    </p></td>
<td><p>                   </p></td>
</tr>
<tr class="even">
<td><p>Database Lis nell'archivio di gestione centrale per informazioni sulla posizione per E9-1-1 (globale)</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>Cmdlet <strong>Export-CsLisConfiguration</strong></p></td>
<td><p></p></td>
<td><p> </p></td>
<td><p>                    </p></td>
</tr>
<tr class="odd">
<td><p>Database RgsConfig nel server back-end per la configurazione di Response Group (pool)</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>Cmdlet <strong>Export-CsRgsConfiguration</strong></p></td>
<td><p></p></td>
<td><p> </p></td>
<td><p>                    </p></td>
</tr>
</tbody>
</table>

