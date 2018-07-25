---
title: 'Lync Server 2013: Requisiti tecnici per il server Chat persistente'
TOCTitle: Requisiti tecnici per il server Chat persistente
ms:assetid: 692b7d99-1bc9-4c99-a050-2bc2be8688b2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398495(v=OCS.15)
ms:contentKeyID: 49300851
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti tecnici per il server Chat persistente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Ogni computer che ospita server Chat persistente deve disporre dell'accesso a una topologia di Lync Server 2013 esistente con i componenti seguenti:

  - **Lync Server 2013, Front End Server.** Il Front End Server rappresenta la base per il routing SIP (Session Initiation Protocol) che rende possibili le comunicazioni tra i computer che eseguono server Chat persistente e la funzionalità Chat persistente. Prima di iniziare a distribuire server Chat persistente, verificare la distribuzione di Lync Server 2013, Standard Edition o di un Lync Serverpool Front End e degli eventuali altri computer interni che eseguono Lync Server, in base alle esigenze specifiche dell'organizzazione.

Nelle sezioni seguenti vengono descritti i requisiti specifici per il server Chat persistente e il database in cui sono archiviati i dati relativi a Chat persistente.

## Requisiti per server Chat persistente

Per informazioni dettagliate sull'hardware consigliato per la distribuzione di Lync Server e dell'ultima versione di server Chat persistente, vedere [Piattaforme hardware server per Lync Server 2013](lync-server-2013-server-hardware-platforms.md) nella documentazione relativa alla supportabilità.

Per informazioni dettagliate sul supporto dei sistemi operativi per i server e gli strumenti per Lync Server e server Chat persistente, vedere [Supporto del sistema operativo per server e strumenti in Lync Server 2013](lync-server-2013-server-and-tools-operating-system-support.md) nella documentazione relativa alla supportabilità.

Per informazioni dettagliate sul software aggiuntivo richiesto per la distribuzione di server Chat persistente, vedere la tabella seguente.

### Prerequisiti software per server Chat persistente

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Software</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Accodamento messaggi</p></td>
<td><p>Utilizzato dal servizio di conformità di server Chat persistente e Chat persistente, se distribuito.</p></td>
</tr>
</tbody>
</table>


## Requisiti del database di server Chat persistente

server Chat persistente utilizza il database di Chat persistente per archiviare la cronologia delle chat, la configurazione e i dati di provisioning degli utenti. Facoltativamente, viene utilizzato il database di conformità di Chat persistente per archiviare i dati di conformità.

> [!important]  
> Il database di Chat persistente (mgc) e il database di conformità (mgccomp) possono essere posizionati nella stessa istanza di SQL Server o in istanze diverse di SQL Server.

Per preparare una piattaforma server di database, assicurarsi che ogni computer soddisfi i requisiti hardware e installare quindi il software prerequisito.

La piattaforma server dei server di database Chat persistente richiede lo stesso hardware del server di database back-end di Lync Server. Per informazioni dettagliate, vedere [Piattaforme hardware server per Lync Server 2013](lync-server-2013-server-hardware-platforms.md) nella documentazione relativa alla supportabilità.

Assicurarsi che nel server di database sia installata una delle applicazioni software seguenti:

  - Microsoft SQL Server 2012. Per informazioni dettagliate su come installare Microsoft SQL Server 2012, vedere "Installare SQL Server 2012" all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkID=248559](http://go.microsoft.com/fwlink/p/?linkid=248559).

  - Microsoft SQL Server 2008 R2. Per informazioni dettagliate su come installare Microsoft SQL Server 2008 R2, vedere "Installazione di SQL Server (SQL Server 2008 R2)" all'indirizzo [http://go.microsoft.com/fwlink/?LinkId=275702](http://go.microsoft.com/fwlink/?linkid=275702).

## Requisiti per i certificati di server Chat persistente

Per informazioni dettagliate sull'acquisizione dei certificati, la creazione del database di SQL Server e la creazione di archivi di file, vedere [Distribuzione di Lync Server 2013](lync-server-2013-deploying-lync-server.md) nella documentazione relativa alla distribuzione.

