---
title: 'Lync Server 2013: Informazioni sui requisiti del firewall per SQL Server'
TOCTitle: Informazioni sui requisiti del firewall per SQL Server
ms:assetid: 31d7df2c-589f-465e-be74-cf6767db190d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425818(v=OCS.15)
ms:contentKeyID: 49300108
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Informazioni sui requisiti del firewall per SQL Server con Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Per una distribuzione di Standard Edition, le eccezioni del firewall vengono create automaticamente durante l'installazione di Lync Server 2013. Per le distribuzioni di Enterprise Edition, è invece necessario configurare manualmente le eccezioni del firewall nel server back-end Microsoft SQL Server. Il protocollo TCP/IP consente un solo uso di una determinata porta per un determinato indirizzo IP. Per il server basato su SQL Server, è pertanto possibile assegnare all'istanza di database predefinita la porta TCP predefinita 1433. Per qualsiasi altra istanza, sarà necessario usare Gestione configurazione SQL Server per assegnare porte univoche e inutilizzate. In questo argomento vengono trattati i temi seguenti:

  - Requisiti per un'eccezione del firewall nei casi in cui viene utilizzata l'istanza predefinita

  - Requisiti per un'eccezione del firewall per il servizio SQL Server Browser

  - Requisiti per le porte di attesa statiche nei casi in cui vengono utilizzate istanze denominate

## Requisiti per un'eccezione del firewall nei casi in cui viene utilizzata l'istanza predefinita

Se si usa l'istanza predefinita di SQL Server per qualsiasi database quando si distribuisce Lync Server 2013, verranno usati i requisiti di regole del firewall seguenti per garantire le comunicazioni dal pool Front End all'istanza predefinita di SQL Server.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Protocollo</th>
<th>Porta</th>
<th>Direzione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TCP</p></td>
<td><p>1433</p></td>
<td><p>In ingresso-SQL Server</p></td>
</tr>
</tbody>
</table>


## Requisiti per un'eccezione del firewall per il servizio SQL Server Browser

Il servizio SQL Server Browser individuerà le istanze di database e comunicherà la porta configurata per l'istanza (denominata o predefinita).


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Protocollo</th>
<th>Porta</th>
<th>Direzione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>UDP</p></td>
<td><p>1434</p></td>
<td><p>In ingresso</p></td>
</tr>
</tbody>
</table>


## Requisiti per le porte di attesa statiche nei casi in cui vengono utilizzate istanze denominate

Quando nella configurazione di SQL Server si usano istanze denominate per i database che supportano Lync Server 2013, è necessario configurare porte statiche usando Gestione configurazione SQL Server. Dopo l'assegnazione delle porte statiche a ogni istanza denominata, creare eccezioni per ogni porta statica nel firewall.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Protocollo</th>
<th>Porta</th>
<th>Direzione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TCP</p></td>
<td><p>Definita in modo statico</p></td>
<td><p>In ingresso</p></td>
</tr>
</tbody>
</table>


## Documentazione relativa a SQL Server

La documentazione relativa a Microsoft SQL Server 2012 contiene istruzioni accurate sulla configurazione dell'accesso attraverso il firewall per i database. Per informazioni dettagliate su Microsoft SQL Server 2012, vedere "Configurare Windows Firewall per consentire l'accesso a SQL Server" all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=218031](http://go.microsoft.com/fwlink/p/?linkid=218031).

