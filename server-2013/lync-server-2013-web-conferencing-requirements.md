---
title: Requisiti di Web Conferencing di Lync Server 2013
TOCTitle: Requisiti di Web Conferencing di Lync Server 2013
ms:assetid: 125f847c-58ab-450f-ae43-41219fd38477
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619171(v=OCS.15)
ms:contentKeyID: 49299740
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti di Web Conferencing di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-01-30_

Se si decide di abilitare le conferenze Web, è necessario pianificare quanto segue:

  -   
    Accesso all'archivio file utilizzato per l'archiviazione del contenuto delle conferenze Web.

  -   
    Integrazione con Server Office Web Apps, necessaria per condividere i file di PowerPoint durante una conferenza.

## Archivio file

Con il servizio per conferenze Web di Lync Server 2013, il contenuto condiviso durante le riunioni viene memorizzato nell'archivio file. Nell'ambito della distribuzione, è necessario specificare una condivisione file da utilizzare come archivio file per il server Standard Edition o il pool Front End di Enterprise Edition. È possibile utilizzare una condivisione di file esistente per l'archivio file oppure specificare una nuova condivisione di file indicando il nome di dominio completo (FQDN) del file server in cui deve essere posizionata la condivisione di file, nonché un nome di cartella per la nuova condivisione di file. Per ulteriori informazioni, vedere Generatore di topologie - Definire l'archivio file per il pool Front End. Il servizio per conferenze Web crittografa il contenuto prima di archiviarlo nell'archivio file.

Lync Server 2013 supporta l'utilizzo di condivisioni file su DAS (Direct Attached Storage) o su una rete di archiviazione (SAN), incluso file system distribuito (DFS), nonché su Redundant Array of Independent Disks (RAID) per gli archivi file. Dopo avere definito la posizione della condivisione file con Distribuzione guidata di Lync Server, Lync Server crea una struttura di cartelle analoga alla seguente all'interno della condivisione file:

  - 1-ApplicationServer-1

  - 1-CentralMgmt-1

  - 1-WebServices-1
    
      - CollabContent
    
      - CollabMetadata
    
      - DataConf

Il servizio di conferenza Web archivia quindi il contenuto, ad esempio diapositive di PowerPoint, lavagne, sondaggi e allegati, nelle cartelle CollabContent e CollabMetadata che si trovano nella cartella WebServices.

L'amministratore deve impostare le autorizzazioni sulla condivisione file in modo che i gruppi RTC dispongano delle necessarie autorizzazioni di accesso in lettura e scrittura.


> [!WARNING]
> In caso di problemi con le autorizzazioni, aprire il Generatore di topologie, scaricare e ripubblicare la topologia esistente. Durante la pubblicazione della topologia vengono verificate le autorizzazioni per la condivisione file e vengono reimpostate, se necessario.



È possibile utilizzare le impostazioni seguenti per gestire l'archiviazione del contenuto per una riunione:

  - **ContentGracePeriod**, in [Set-CsConferencingConfiguration](set-csconferencingconfiguration.md), imposta la durata della permanenza del contenuto delle conferenze Web sul server dopo la conclusione della riunione.

  - **MaxContentStorageMb**, in [Set-CsConferencingConfiguration](set-csconferencingconfiguration.md), imposta la quantità massima di spazio consentita per l'archiviazione del contenuto durante una singola riunione.

**MaxUploadFileSizeMb** non limita l'impostazione di caricamento dei file per Lync Web App. La dimensione massima di caricamento file per Lync Web App è impostata su circa 30 MB ed è controllata dal file web.config di IIS: /DataCollabWeb/Int\[Ext\]/Handler/web.config. Per configurare la dimensione massima per il caricamento di file per Lync Web App, aggiornare i valori `maxRequestLength` e `maxAllowedContentLength` nel file web.config come mostrato di seguito.

    <system.web>
        <!-- 
            Since this handler is used to upload files to DMCU the request size (in kilobytes) 
            has to fit max allowed file size uploaded by Lync Web App client.
            The timeout has to reflect the min client bandwidth. Timeout of 600 secs 
            and 512 Kbits of *client* bandwidth would result into aproximately 30 Mbytes 
            for Lync Web App upload size limit.
        -->
          <httpRuntime maxRequestLength="500000" executionTimeout="600" />
    
    
    
                    <security>
                    <requestFiltering>
                               <requestLimits maxAllowedContentLength="524288000" />
                    </requestFiltering>
                    </security>

È necessario aggiornare il file web.config per ogni Front End Server.

## Server Office Web Apps

Per utilizzare queste nuove funzionalità, gli amministratori devono installare Server Office Web Apps e configurare Lync Server 2013 per la comunicazione con Server Office Web Apps. In questa documentazione vengono fornite informazioni su come configurare Lync Server 2013 per il funzionamento con Server Office Web Apps. Non sono invece fornite informazioni sull'installazione di Server Office Web Apps. Per informazioni dettagliate sull'installazione, visitare il sito Web dedicato alla distribuzione di Microsoft Office Web Apps all'indirizzo <http://go.microsoft.com/fwlink/?linkid=257525>. In questa guida sono riportate informazioni complete sui prerequisiti per Server Office Web Apps. Tenere presente che è necessario che Server Office Web Apps sia installato in un computer autonomo che non esegue Lync Server, SQL Server o altre applicazioni server (in tale computer non deve essere installata alcuna versione di Office). Nei computer utilizzati per eseguire Server Office Web Apps deve inoltre essere installato uno specifico set di software, tra cui .NET Framework 4.5 e Windows PowerShell 3.0. Questi requisiti, insieme alle informazioni per la configurazione dei certificati e di Internet Information Services (IIS), sono illustrati in dettaglio nel sito Web dedicato alla distribuzione di Microsoft Office Web Apps all'indirizzo <http://go.microsoft.com/fwlink/?linkid=257525>.

## Vedere anche

#### Concetti

[Panoramica di Web Conferencing in Lync Server 2013](lync-server-2013-web-conferencing-overview.md)  
[Elenco di controllo di distribuzione per Web Conferencing](lync-server-2013-deployment-checklist-for-web-conferencing.md)

