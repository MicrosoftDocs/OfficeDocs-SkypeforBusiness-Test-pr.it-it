---
title: Preparazione al ripristino di Lync Server
TOCTitle: Preparazione al ripristino di Lync Server
ms:assetid: 857e4e02-908e-433a-96c6-be1795a9cb61
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh202179(v=OCS.15)
ms:contentKeyID: 52062191
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Preparazione al ripristino di Lync Server

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Prima di iniziare a ripristinare server e database dopo un errore, è necessario determinare gli aspetti seguenti:

  - Elementi da ripristinare.

  - Hardware, software, dati e strumenti necessari per il ripristino.

## Determinazione dei componenti da ripristinare

In questo argomento viene descritto come eseguire il ripristino in seguito a interruzioni di Lync Server che si verificano a livello di server, pool, o archivio di gestione centrale. In caso di errore dell'archivio di gestione centrale, la distribuzione di Lync Server continua a funzionare, ma non è possibile apportare modifiche alla configurazione. In caso di errore di un server back-end o Standard Edition, il pool di utenti smette di funzionare. In caso di errore di qualsiasi altro server, la gravità dell'errore dipende dal ruolo del server e dal fatto che il server ospiti uno o più database.

### Componenti da ripristinare

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>In caso di errore di</th>
<th>Vedere questa sezione:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Server Standard Edition</p></td>
<td><p><a href="lync-server-2013-restoring-a-standard-edition-server.md">Ripristino di un server Standard Edition</a></p></td>
</tr>
<tr class="even">
<td><p>archivio di gestione centrale</p></td>
<td><p><a href="lync-server-2013-restoring-the-server-hosting-the-central-management-store.md">Ripristino del server che ospita l'archivio di gestione centrale</a></p></td>
</tr>
<tr class="odd">
<td><p>Back-end Enterprise Edition</p></td>
<td><p><a href="lync-server-2013-restoring-an-enterprise-edition-back-end-server.md">Ripristino di un Server Enterprise back-end</a></p></td>
</tr>
<tr class="even">
<td><p>Server primario back-end con mirroring Enterprise Edition</p></td>
<td><p><a href="lync-server-2013-restoring-a-mirrored-enterprise-edition-back-end-server-primary.md">Ripristino di un server back-end Enterprise Edition con mirroring - Principale</a></p></td>
</tr>
<tr class="odd">
<td><p>Server secondario back-end con mirroring Enterprise Edition</p></td>
<td><p><a href="lync-server-2013-restoring-a-mirrored-enterprise-edition-back-end-server-mirror.md">Ripristino di un server back-end Enterprise Edition con mirroring - Mirroring</a></p></td>
</tr>
<tr class="even">
<td><p>Qualsiasi server Enterprise Edition che esegue un ruolo del server, ad esempio Front End Server, server perimetrale, Server Director, Mediation Server o server Chat persistente.</p></td>
<td><p><a href="lync-server-2013-restoring-an-enterprise-edition-member-server.md">Ripristino di un server membro Enterprise Edition</a></p></td>
</tr>
<tr class="odd">
<td><p>Un intero pool di Lync Server</p></td>
<td><p><a href="lync-server-2013-restoring-a-lync-server-pool.md">Ripristino di un pool di Lync Server</a></p></td>
</tr>
<tr class="even">
<td><p>Archivio file Enterprise Edition</p></td>
<td><p><a href="lync-server-2013-restoring-a-file-store.md">Ripristino di un archivio file</a></p></td>
</tr>
<tr class="odd">
<td><p>Un database di monitoraggio o di archiviazione autonomo</p></td>
<td><p><a href="lync-server-2013-restoring-monitoring-or-archiving-data.md">Ripristino dei dati di monitoraggio o archiviazione</a></p></td>
</tr>
<tr class="even">
<td><p>Un database di Chat persistente autonomo</p></td>
<td><p><a href="lync-server-2013-restoring-persistent-chat-data.md">Ripristino di dati di Chat persistente</a></p></td>
</tr>
</tbody>
</table>


## Raccolta di hardware, software e strumenti

Quando si ripristina un server, è necessario iniziare con un computer nuovo o pulito. È inoltre necessario disporre dei componenti hardware e software seguenti:

  - Un server nuovo o pulito con lo stesso nome di dominio completo (FQDN) del server in cui si è verificato l'errore.
    
    > [!important]  
    > Quando si installa il sistema operativo, fare attenzione a non eliminare l'account del computer in Servizi di dominio Active Directory e verificare che vengano mantenute le autorizzazioni di gruppo per l'account.

  - Software di installazione per il sistema operativo. Per installare il sistema operativo, è possibile utilizzare le procedure di distribuzione del server e le configurazioni stabilite dall'organizzazione. Quando si ripristina il servizio, è necessario avere a disposizione tali requisiti di configurazione e procedure.

  - Software di installazione per SQL Server 2012 o SQL Server 2008 R2. Per installare un server di database, utilizzare la versione appropriata di SQL Server, nonché le configurazioni e le procedure di distribuzione del server di database stabilite dall'organizzazione. Quando si ripristina il servizio, è necessario avere a disposizione tali requisiti di configurazione e procedure.
    

    > [!NOTE]
    > La Distribuzione guidata di Lync Server consente di installare automaticamente SQL Server 2012 Express in ogni server Standard Edition e qualsiasi altro server Lync Server durante l'installazione di un archivio di configurazione locale, a meno che nel server non siano preinstallati SQL Server 2012 o SQL Server 2008 R2.



  - Software per l'acquisizione di immagini di sistema.
    
    > [!tip]  
    > È consigliabile acquisire una copia dell'immagine del sistema dopo l'installazione del sistema operativo e di SQL Server e prima di iniziare il ripristino, in modo che sia possibile utilizzare questa immagine come punto di ripristino dello stato precedente in caso di problemi durante il ripristino.

  - Software di installazione di Lync Server 2013. La Distribuzione guidata di Lync Server è disponibile nella cartella o nel supporto di installazione di Lync Server in \\setup\\amd64\\Setup.exe.

Durante il ripristino, vengono utilizzati gli strumenti seguenti:

  - Cmdlet di Lync Server Management Shell

  - Import-CsUserData

  - Strumenti per il ripristino delle cartelle di Windows

  - Generatore di topologie

  - Utilità di database di SQL Server, ad esempio SQL Server Management Studio

## Preparazione al ripristino di un server

Prima di ripristinare il server, è necessario eseguire le operazioni seguenti:

1.  Installare il sistema operativo.

2.  Se il server è un server back-end, installare SQL Server 2012 o SQL Server 2008 R2.

3.  Ripristinare i certificati o eseguirne una nuova registrazione. Per informazioni dettagliate sui certificati, vedere la sezione relativa ai requisiti di backup aggiuntivi in [Requisiti di backup e ripristino: dati](lync-server-2013-backup-and-restoration-requirements-data.md).

4.  Acquisire un'immagine del sistema prima di iniziare il ripristino, da utilizzare come punto di ripristino dello stato precedente in caso di problemi durante il ripristino.


> [!NOTE]
> La Distribuzione guidata di Lync Server e i cmdlet descritti nelle procedure in questo argomento e negli argomenti correlati consentono di impostare tutti gli elenchi di controllo di accesso (ACL) necessari.



Verificare che l'hardware e il software necessari per i componenti che si desidera ripristinare siano disponibili prima di iniziare il ripristino. Dopo aver installato il sistema operativo e SQL Server, la maggior parte delle operazioni delle procedure di ripristino seguenti può essere eseguita in modalità remota. Le eccezioni sono segnalate nelle procedure.

È inoltre necessario avere a disposizione il piano di backup e ripristino dell'organizzazione e le informazioni dell'ultimo backup, ad esempio le informazioni contenute nei fogli di lavoro in questo documento (per informazioni dettagliate, vedere [Fogli di lavoro per il backup e il ripristino](lync-server-2013-backup-and-restoration-worksheets.md)), prima di iniziare il ripristino.

