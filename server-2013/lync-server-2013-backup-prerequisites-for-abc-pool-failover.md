---
title: Prerequisiti per il backup per failover del pool ABC
TOCTitle: Prerequisiti per il backup per failover del pool ABC
ms:assetid: 652046f5-6086-4592-902d-d5789581977d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945634(v=OCS.15)
ms:contentKeyID: 52062175
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Prerequisiti per il backup per failover del pool ABC

 

_**Ultima modifica dell'argomento:** 2013-03-26_

Per ottenere il massimo dalla procedura di failover del pool ABC, è necessario eseguire specifici backup prima che si verifichino la situazione di emergenza e il failover:

  - È necessario eseguire regolarmente il backup dei dati di configurazione LIS (Location Information Service) dal pool A tramite il cmdlet **Export-CsLISConfiguration**.
    
        Export-csLisConfiguration -FileName <C:\LISExportPrimary.zip>

  - È necessario eseguire regolarmente il backup dei dati di configurazione di Response Group nel pool A tramite il cmdlet **Export-CsRgsConfiguration**.
    
        Export-CsRgsConfiguration -Source "service:ApplicationServer:<Pool A FQDN>" -FileName "C:\RgsExportPrimary.zip"
    
    In generale, è consigliabile eseguire backup giornalieri, ma in presenza di un volume elevato di modifiche è possibile pianificare backup più frequenti. La quantità di informazioni che è possibile perdere in caso di emergenza varia in base alla frequenza dei backup, oltre che alla frequenza e al volume di modifiche.
    
    L'applicazione Response Group consente di archiviare un solo set di impostazioni a livello di applicazione per pool. Queste impostazioni sono accessibili tramite i cmdlet **Get-CsRgsConfiguration** e includono la configurazione della musica di attesa predefinita, il file audio della musica di attesa predefinita, il periodo di tolleranza per la richiamata dell'agente e la configurazione del contesto di chiamata. Queste impostazioni possono essere trasferite da un pool all'altro tramite il cmdlet **Import-CsRgsConfiguration** utilizzando il parametro **ReplaceExistingSettings**, ma questa operazione comporterà la sostituzione delle eventuali impostazioni a livello di applicazione nel pool di destinazione.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Conservare in una posizione separata una copia di backup di tutti i file audio originali utilizzati per configurare l'applicazione Response Group , ovvero eventuali registrazioni o file della musica di attesa.</td>
    </tr>
    </tbody>
    </table>
    
    Se sono disponibili file di musica di attesa personalizzati caricati per il parcheggio di chiamata in un pool, è consigliabile conservarne una copia in un'altra posizione. Questi file non vengono inclusi nel backup durante il processo di ripristino di emergenza di Lync Server 2013 e verranno persi se i file caricati nel pool vengono danneggiati o cancellati.
    
        Xcopy  <Source: Pool A CPS File Store Path>  <Destination>
        Example: Xcopy  "<Pool A File Store Path>\LyncFileStore\coX-ApplicationServer-X\AppServerFiles\CPS\"  "<Destination:  Backup location 1>"
    

    > [!NOTE]
    > L'applicazione Parcheggio di chiamata consente di archiviare un solo set di impostazioni e un file audio della musica di attesa personalizzata. È possibile accedere a tali impostazioni tramite il cmdlet <STRONG>Get-CsCpsConfiguration</STRONG>. Dato che il meccanismo di ripristino di emergenza per il parcheggio di chiamata si basa sull'applicazione Parcheggio di chiamata del pool di backup, in caso di emergenza le impostazioni del pool principale non vengono incluse in un backup o preservate. Se si perde il pool principale, queste impostazioni non possono essere recuperate e quando si distribuisce un nuovo pool per sostituire quello principale, sarà necessario riconfigurare le impostazioni del parcheggio di chiamata ed eventuali file audio della musica di attesa personalizzata.



  - Se si configurano eventuali annunci per la funzionalità dei numeri non assegnati, è consigliabile conservare in un'altra posizione una copia del file audio originale utilizzato durante la configurazione iniziale. In caso contrario, si può ottenere una copia dei file audio configurati nell'archivio file del server o del pool in cui sono stati importati i file audio. Questi file non vengono inclusi nel backup durante il processo di ripristino di emergenza di Lync Server 2013 e verranno persi se i file caricati nel pool vengono danneggiati o cancellati. Per copiare tutti i file audio utilizzati per la configurazione dei numeri non assegnati dall'archivio file di un server o un pool, utilizzare:
    
        Use: Xcopy  <Source: Pool A Announcement Service File Store Path>  <Destination>
        Example Usage:  Xcopy  "<Pool A File Store Path>\X-ApplicationServer-X\AppServerFiles\RGS\AS"  "<Destination: Backup location>"

  - Se in un pool esistono database di monitoraggio e archiviazione, è necessario utilizzare gli strumenti di gestione di SQL Server per eseguirne il backup. Nella procedura di failover ABC, i database di monitoraggio e archiviazione non vengono preservati se collocati nel pool A, perché tali database non sono inclusi nel backup eseguito tramite il servizio di backup di Lync Server.

