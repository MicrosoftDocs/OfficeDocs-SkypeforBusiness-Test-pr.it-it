---
title: 'Lync Server 2013: Supporto per il software di database'
TOCTitle: Supporto per il software di database
ms:assetid: e05d0032-bbea-4e61-987d-d07b1c045fd5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398990(v=OCS.15)
ms:contentKeyID: 49302231
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Supporto per il software di database in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-12-01_

Lync Server 2013 supporta i sistemi di gestione di database seguenti:

  - **Database back-end di un pool Front End, database di archiviazione, database di monitoraggio, database di chat persistente e database di conformità di chat persistente**
    
      - Software di database di Microsoft SQL Server 2008 R2 Enterprise (edizione a 64 bit). È inoltre consigliabile eseguire il Service Pack più recente.
    
      - Microsoft SQL Server 2008 R2 Standard (edizione a 64 bit). È inoltre consigliabile eseguire il Service Pack più recente.
    
      - Microsoft SQL Server 2012 Enterprise (edizione a 64 bit). È inoltre consigliabile eseguire il Service Pack più recente.
    
      - Microsoft SQL Server 2012 Standard (edizione a 64 bit). È inoltre consigliabile eseguire il Service Pack più recente.

  - **Database server Standard Edition e database Front End Server**
    
      - Microsoft SQL Server 2012 Express (edizione a 64 bit). È inoltre consigliabile eseguire il Service Pack più recente.
        
        L'installazione della patch e l'aggiornamento di Microsoft SQL Server sono supportati nei Front End Server e nei server Standard Edition. Tuttavia, quando si installa qualsiasi tipo di aggiornamento o patch nei Front End Server, è necessario tenere in considerazione i requisiti quorum. Per altre informazioni, vedere [Eseguire l'aggiornamento dei Front End Server in Lync Server 2013](lync-server-2013-upgrade-or-update-front-end-servers.md) e [Topologie e componenti per Front End Server, messaggistica istantanea e presenza in Lync Server 2013](lync-server-2013-topologies-and-components-for-front-end-servers-instant-messaging-and-presence.md).
    

    > [!NOTE]
    > Microsoft SQL Server 2012 Express (edizione a 64 bit) viene installato automaticamente da Lync Server 2013 in ogni server Standard Edition e in ogni server Front End Server.



<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Lync Server 2013 non supporta l'edizione a 32 bit di SQL Server. È necessario utilizzare l'edizione a 64 bit.</p></li>
<li><p>SQL Server Web Edition e SQL Server Workgroup Edition nono sono supportati e non è possibile utilizzarli con Lync Server 2013.</p></li>
<li><p>Lync Server 2013 supporta il mirroring di database nativi.</p></li>
<li><p>Per utilizzare il ruolo Monitoring Server, è necessario installare SQL Server Reporting Services.</p></li>
</ul></td>
</tr>
</tbody>
</table>


In un pool Front End, il database back-end può essere un singolo computer SQL Server.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Se i database di Lync Server vengono installati nella stessa posizione di altri database, è consigliabile valutare tutti i fattori che potrebbero influire su disponibilità e prestazioni, oltre ad assicurarsi che, in caso di errore di un nodo, il nodo rimanente sia in grado di gestire il carico. Per verificare le funzionalità di failover, è consigliabile testare tutti i possibili scenari.</td>
</tr>
</tbody>
</table>


## Uso del mirroring e del clustering SQL

Lync Server 2013 supporta l'uso del mirroring o del clustering SQL per ogni database di Lync Server. È possibile configurare il mirroring SQL in modo semplice e rapido con lo strumento Generatore di topologie in Lync Server 2013. Per la configurazione del clustering di failover SQL, è necessario usare SQL Server.

Lync Server 2013 supporta sia le topologie con mirroring SQL che con clustering SQL per tutte le distribuzioni, incluse le distribuzioni vergini e le organizzazioni che hanno eseguito l'aggiornamento dalle versioni precedenti di Lync Server.

Il supporto per il clustering SQL è per una configurazione attiva o passiva. Per motivi legati alle prestazioni, il nodo passivo non deve essere condiviso con un'altra istanza SQL.

È incluso il supporto seguente:

  - Clustering di failover a due nodi per:
    
      - Microsoft SQL Server 2012 Standard (edizione a 64 bit). È inoltre consigliabile eseguire il Service Pack più recente.
    
      - Microsoft SQL Server 2008 R2 Standard (edizione a 64 bit). È inoltre consigliabile eseguire il Service Pack più recente.

  - Clustering di failover con fino a sedici nodi per:
    
      - Microsoft SQL Server 2012 Enterprise (edizione a 64 bit). È inoltre consigliabile eseguire il Service Pack più recente.
    
      - Software di database di Microsoft SQL Server 2008 R2 Enterprise (edizione a 64 bit). È inoltre consigliabile eseguire il Service Pack più recente.

Per altre informazioni sul mirroring SQL, vedere [Disponibilità elevata del server back-end in Lync Server 2013](lync-server-2013-back-end-server-high-availability.md). Per dettagli su come distribuire il clustering SQL, vedere [Configurare il clustering di SQL Server per Lync Server 2013](lync-server-2013-configure-sql-server-clustering.md).

Per altre informazioni e procedure consigliate per il clustering di failover in SQL Server 2012, vedere <http://technet.microsoft.com/it-it/library/hh231721.aspx>. Per il clustering di failover in SQL Server 2008, vedere <http://technet.microsoft.com/it-it/library/ms189134(v=sql.105).aspx>.

