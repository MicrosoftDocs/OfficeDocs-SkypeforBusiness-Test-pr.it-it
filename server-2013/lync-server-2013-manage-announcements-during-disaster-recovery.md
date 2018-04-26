---
title: 'Lync Server 2013: Gestire gli annunci durante il ripristino di emergenza'
TOCTitle: Gestire gli annunci durante il ripristino di emergenza
ms:assetid: c33e51ea-421f-42d2-826b-b73968f6bd5b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721874(v=OCS.15)
ms:contentKeyID: 49887738
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestire gli annunci durante il ripristino di emergenza in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Lync Server 2013 supporta durante un'interruzione dei servizi gli annunci per le chiamate a numeri non assegnati. Il ripristino della funzionalità degli annunci durante un'interruzione dei servizi è facoltativo. Se si sceglie di ripristinare gli annunci durante un'interruzione dei servizi, è necessario ricreare la configurazione degli annunci nel pool di backup. In questa sezione vengono descritte le operazioni da eseguire se si sceglie di ripristinare gli annunci durante il ripristino di emergenza.

Questa sezione si applica agli intervalli di numeri non assegnati che si basano sull' applicazione Annuncio e non si applica invece agli intervalli di numeri non assegnati basati su Operatore automatico di Messaggistica unificata di Exchange.

## Prima di un'interruzione dei servizi

Indipendentemente dalla decisione di utilizzare gli annunci durante le interruzioni dei servizi, è consigliabile eseguire backup separati dei file audio personalizzati configurati per l' applicazione Annuncio. Nel processo di ripristino di emergenza di Lync Server infatti non viene eseguito il backup degli annunci personalizzati. I file andranno perduti se non si eseguono backup separati e le copie caricate nel server o nel pool vengono danneggiate o cancellate.

Se non si dispone di copie di backup di file audio personalizzati e i file audio originali non sono più disponibili, è possibile reperire i file audio configurati per un' applicazione Annuncio nell'archivio file del server o del pool a partire dal quale sono stati importati. È possibile copiare dall'archivio file tutti i file audio configurati per l' applicazione Annuncio.

**Per copiare i file audio dall'archivio file**

1.  Nella riga di comando digitare il comando seguente:
    
        Xcopy <Source: Pool Announcement Service File Store path> <Destination>
    
    Ad esempio:
    
        Xcopy "<Pool File Store Path>\X-ApplicationServer-X\AppServerFiles\RGS\AS" "<Destination: Backup location>"
    
    Dove X-ApplicationServer-X indica l'ID servizio del server applicazioni del pool, ad esempio 1-ApplicationServer-1.


## Durante un'interruzione dei servizi

Per utilizzare l' applicazione Annuncio durante un'interruzione dei servizi, è necessario ricreare la configurazione degli annunci nel pool di backup eseguendo le attività descritte in questa sezione.


> [!NOTE]
> È consigliabile eseguire queste attività dopo il failover al pool di backup, poiché nel momento in cui si esegue il passaggio 2, il pool di backup assume la proprietà degli intervalli di numeri non assegnati.




> [!NOTE]
> Queste operazioni non sono necessarie per gli intervalli di numeri in cui viene utilizzato un numero di telefono di Operatore automatico di Messaggistica unificata di Exchange.



**Per ricreare la configurazione degli annunci nel pool di backup**

1.  Eseguire le operazioni seguenti per ricreare nel pool di backup gli annunci distribuiti nel pool principale:
    
    1.  Importare nel pool di backup i file audio utilizzati nel pool principale utilizzando il cmdlet **Import-CsAnnouncementFile** e specificando il pool di backup per il parametro Parent.
    
    2.  Ricreare ogni annuncio utilizzando il cmdlet **New-CsAnnouncement** e specificando il pool di backup per il parametro Parent.
    

    > [!NOTE]
    > Per informazioni dettagliate sull'utilizzo di questi parametri per la creazione di annunci nel pool di backup, vedere <A href="lync-server-2013-create-an-announcement.md">Creare un annuncio in Lync Server 2013</A>.



2.  Dopo aver ricreato tutti gli annunci nel pool di backup, reindirizzare agli annunci ricreati nel pool di backup tutti gli intervalli di numeri non assegnati in cui vengono utilizzati gli annunci nel pool principale.
    
    Eseguire il comando seguente per ogni intervallo di numeri non assegnati in cui viene utilizzato un annuncio nel pool principale:
    
        Set-CsUnassignedNumber -Identity "<name of number range>" -AnnouncementService "<FQDN of backup pool>" -AnnouncementName "<announcement name in backup pool>"

## Dopo l'interruzione dei servizi

Quando diventa disponibile il pool principale, è necessario reindirizzare gli intervalli di numeri non assegnati modificati per l'interruzione dei servizi di nuovo al pool principale.


> [!NOTE]
> Queste operazioni non sono necessarie per gli intervalli di numeri in cui viene utilizzato un numero di telefono di Operatore automatico di Messaggistica unificata di Exchange.



**Per ripristinare gli annunci nel pool principale**

1.  Se è stato necessario rigenerare il pool principale durante il ripristino, sarà necessario ricreare gli annunci nel pool principale importando i file audio e creando gli annunci, esattamente come per il pool di backup ma specificando in questo caso il pool principale per il parametro Parent. Per informazioni dettagliate, vedere la sezione "Durante un'interruzione dei servizi" più indietro in questo argomento.

2.  Eseguire il comando seguente per ogni intervallo di numeri non assegnati modificato per l'interruzione dei servizi:
    
        Set-CsUnassignedNumber [-Identity "<name of number range>"] -AnnouncementService "<FQDN of primary pool>" -AnnouncementName "<announcement name in primary pool>"

3.  Facoltativamente, rimuovere gli annunci ricreati nel pool di backup. Ottenere un elenco di annunci per l' applicazione Annuncio del pool di backup. A tale scopo, nella riga di comando digitare il comando seguente:
    
        Get-CsAnnouncement -Identity "<Service:service ID>"
    
    Ad esempio:
    
        Get-CsAnnouncement -Identity "ApplicationServer:redmond.contoso.com
    
    Nell'elenco ottenuto individuare gli annunci che si desidera rimuovere e copiare i GUID. Eseguire il comando seguente per ogni annuncio che si desidera rimuovere:
    
        Remove-CsAnnouncement -Identity "<Service:service ID/guid>"
    
    Ad esempio:
    
        Remove-CsAnnouncement -Identity "ApplicationServer:redmond.contoso.com/1951f734-c80f-4fb2-965d-51807c792b90"


