---
title: "Lync Server 2013: Gestisce ripristino di emerg., disp. elevata e backup"
TOCTitle: Gestione di ripristino di emergenza, disponibilità elevata e servizio di backup di Lync Server 2013
ms:assetid: f4cd36fb-ffd6-48fa-b761-e11b3bcff91a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721939(v=OCS.15)
ms:contentKeyID: 49887827
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestione di ripristino di emergenza, disponibilità elevata e servizio di backup di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-12_

In questa sezione sono incluse le procedure per le operazioni di ripristino di emergenza e per la gestione del servizio di backup che esegue la sincronizzazione dei dati nei pool Front End abbinati.

Le procedure di ripristino di emergenza, sia di failover che di failback, sono manuali. In caso di emergenza, è necessario che l'amministratore richiami manualmente le procedure di failover. La stessa procedura si applica al failback dopo che il pool è stato ripristinato.

Per le procedure di ripristino di emergenza presenti nel resto della sezione vengono presupposti gli elementi seguenti:

  - È disponibile una distribuzione con pool Front End abbinati in siti diversi, come descritto in [Pianificazione per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md). Il servizio di backup è stato eseguito nei pool abbinati per mantenerli sincronizzati.

  - Se l' archivio di gestione centrale è ospitato in uno dei pool, è installato e in esecuzione in entrambi i pool abbinati, con uno dei pool che ospita il master attivo e l'altro pool quello in standby.

> [!IMPORTANT]  
> Nelle procedure seguenti il parametro <em>PoolFQDN</em> si riferisce al nome di dominio completo (FQDN) del pool interessato dall'emergenza, non al pool da cui gli utenti interessati dal problema vengono reindirizzati. Per lo stesso gruppo di utenti interessati dal problema, si riferisce allo stesso pool nei cmdlet di failover e failback (il pool che ospitava gli utenti prima del failover).<br />Si supponga ad esempio un caso in cui per tutti gli utenti ospitati in un pool P1 sia stato eseguito il failover nel pool di backup, P2. Se l'amministratore desidera spostare tutti gli utenti serviti da P2 in modo che siano serviti da P1, è necessario che esegua le procedure seguenti:
> <ol>
> <li><p>Eseguire il failback di tutti gli utenti originariamente ospitati in P1 da P2 a P1 utilizzando il cmdlet di failback. In tal caso, <em>PoolFQDN</em> è il nome di dominio completo (FQDN) di P1.</p></li>
> <li><p>Eseguire il failover di tutti gli utenti originariamente ospitati in P2 a P1 utilizzando il cmdlet di failover. In tal caso, <em>PoolFQDN</em> è il nome di dominio completo (FQDN) di P2.</p></li>
> <li><p>Se successivamente l'amministratore desidera eseguire il failback degli utenti P2 a P2, <em>PoolFQDN</em> è il nome di dominio completo (FQDN) di P2.</p></li></ol>
> Per preservare l'integrità del pool, è necessario eseguire la procedura 1 prima della procedura 2. Se si esegue la procedura 2 prima della procedura 1, il cmdlet della procedura 2 avrà esito negativo.</td>
</tr>
</tbody>
</table>


## Argomenti della sezione

  - [Configurazione e monitoraggio del servizio di backup in Lync Server 2013](lync-server-2013-configuring-and-monitoring-the-backup-service.md)

  - [Failover di un pool in Lync Server 2013](lync-server-2013-failing-over-a-pool.md)

  - [Failback di un pool in Lync Server 2013](lync-server-2013-failing-back-a-pool.md)

  - [Failover di un database con mirroring in Lync Server 2013](lync-server-2013-failing-over-a-mirrored-database.md)

  - [Failover del pool di server perimetrali utilizzato per la federazione di Lync Server in Lync Server 2013](lync-server-2013-failing-over-the-edge-pool-used-for-lync-server-federation.md)

  - [Failover del pool di server perimetrali utilizzato per la federazione di XMPP in Lync Server 2013](lync-server-2013-failing-over-the-edge-pool-used-for-xmpp-federation.md)

  - [Failback del pool di server perimetrali utilizzato per la federazione di Lync Server o di XMPP in Lync Server 2013](lync-server-2013-failing-back-the-edge-pool-used-for-lync-server-federation-or-xmpp-federation.md)

  - [Modifica del pool di server perimetrali associato a un pool Front End in Lync Server 2013](lync-server-2013-changing-the-edge-pool-associated-with-a-front-end-pool.md)

  - [Ripristino del contenuto delle conferenze tramite il servizio di backup in Lync Server 2013](lync-server-2013-restoring-conference-contents-using-the-backup-service.md)

## Vedere anche

#### Concetti

[Pianificazione per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md)

