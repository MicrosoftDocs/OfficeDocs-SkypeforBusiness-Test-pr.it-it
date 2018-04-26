---
title: Backup di impostazioni e dati di base
TOCTitle: Backup di impostazioni e dati di base
ms:assetid: 278bc95a-7b8d-4e01-a872-a844830459de
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh202170(v=OCS.15)
ms:contentKeyID: 52062123
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Backup di impostazioni e dati di base

 

_**Ultima modifica dell'argomento:** 2014-04-23_

Nelle procedure illustrate in questa sezione vengono utilizzati i cmdlet di Lync Server Management Shell per creare file di backup per le impostazioni e i dati dei servizi di base. Per informazioni dettagliate sugli strumenti utilizzati in questa sezione e sulla relativa posizione, vedere [Requisiti di backup e ripristino: strumenti e autorizzazioni](lync-server-2013-backup-and-restoration-requirements-tools-and-permissions.md). Per informazioni dettagliate su come eseguire il backup dei dati di archiviazione e di monitoraggio, vedere [Backup dei database di archiviazione e monitoraggio](lync-server-2013-backing-up-archiving-and-monitoring-databases.md).


> [!NOTE]
> La procedura di questa sezione per il backup dell'archivio di gestione centrale include le impostazioni e la configurazione dell'archiviazione e del monitoraggio.



È possibile eseguire i cmdlet descritti in questa sezione localmente o da postazione remota.

## Per eseguire il backup dei dati e delle impostazioni di base

1.  Eseguire l'accesso a un computer della distribuzione interna utilizzando un account utente membro del gruppo RTCUniversalServerAdmins.

2.  Per archiviare i backup creati nei passaggi seguenti, creare una nuova cartella condivisa e aggiornare il percorso utilizzato come riferimento da **$Backup** sostituendolo con la nuova cartella condivisa.

3.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

4.  Eseguire il backup del file di configurazione dell'archivio di gestione centrale. Nella riga di comando digitare il comando seguente:
    
        Export-CsConfiguration -FileName <path and file name for backup>
    
    Ad esempio:
    
        Export-CsConfiguration -FileName "C:\Config.zip"
    

    > [!NOTE]
    > Con questa operazione vengono esportati in un file la topologia, i criteri e le impostazioni di configurazione di Lync Server. Non sono richieste altre operazioni per il backup dei dati della topologia.



5.  Copiare il backup del file di configurazione dell'archivio di gestione centrale in $Backup\\.

6.  Eseguire il backup dei dati del servizio Informazioni percorso. Nella riga di comando digitare il comando seguente:
    
        Export-CsLisConfiguration -FileName <path and file name for backup>
    
    Ad esempio:
    
        Export-CsLisConfiguration -FileName "C:\E911Config.zip"

7.  Copiare il backup del file di configurazione del servizio Informazioni percorso in $Backup\\.

8.  Eseguire il backup dei dati utente di ogni database back-end di un pool Front End e di ogni server Standard Edition. Nella riga di comando digitare il comando seguente:
    
        Export-CsUserData -PoolFQDN <Fqdn> -FileName <String>
    
    Ad esempio:
    
        Export-CsUserData -PoolFQDN "atl-cs-001.litwareinc.com" -FileName "C:\Logs\ExportedUserData.zip"

9.  Copiare il backup del file dei dati utente in $Backup\\.

10. In ogni pool che esegue l'applicazione Response Group, eseguire il backup della configurazione di Response Group. Eseguire le operazioni seguenti:
    
    1.  Nella riga di comando digitare:
        
            Export-CsRgsConfiguration -Source "service:ApplicationServer:<pool FQDN>" -FileName <path and file name for backup>
        
        Ad esempio:
        
            Export-CsRgsConfiguration -Source ApplicationServer:pool01.contoso.com -FileName C:\RgsConfiguration.zip

11. Copiare il backup del file di configurazione di Response Group in $Backup\\.

