---
title: Aggiornare un server back-end o un server Standard Edition in Lync Server 2013
TOCTitle: Aggiornare un server back-end o un server Standard Edition in Lync Server 2013
ms:assetid: f95f8d3a-e039-484e-97bd-d727db21a12b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721942(v=OCS.15)
ms:contentKeyID: 49887836
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Aggiornare un server back-end o un server Standard Edition in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

In questo argomento viene illustrato come aggiornare un server back-endEnterprise Edition o un server Standard Edition.

Se un server back-end non è disponibile per almeno 30 minuti durante l'esecuzione dell'aggiornamento, gli utenti potrebbero passare alla modalità di resilienza. Al termine dell'aggiornamento, i server back-end si connettono di nuovo ai Front End Server nel pool e vengono ripristinate tutte le funzionalità per gli utenti. Se l'aggiornamento richiede meno di 30 minuti, non avrà alcun effetto sugli utenti.

## Per aggiornare un server back-end o un server Standard Edition

1.  Eseguire l'accesso al server da aggiornare come membro del ruolo CsAdministrator.

2.  Scaricare l'aggiornamento ed estrarlo nel disco rigido locale.

3.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

4.  Arrestare i servizi di Lync Server. Nella riga di comando digitare:
    
        Stop-CsWindowsService

5.  Arrestare il servizio World Wide Web. Nella riga di comando digitare:
    
        net stop w3svc

6.  Chiudere tutte le finestre di Lync Server Management Shell.

7.  Installare l'aggiornamento.

8.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

9.  Arrestare di nuovo i servizi di Lync Server per raccogliere gli assembly -d della Global Assembly Cache (GAC). Nella riga di comando digitare:
    
        Stop-CsWindowsService

10. Riavviare il servizio World Wide Web. Nella riga di comando digitare:
    
        net start w3svc

11. Applicare le modifiche apportate da LyncServerUpdateInstaller.exe ai database di SQL Server eseguendo una delle operazioni seguenti:
    
      - Se il sistema è un server back-endEnterprise Edition e non sono presenti database installati nel server, ad esempio database di archiviazione o di monitoraggio, nella riga di comando digitare quanto segue:
        
            Install-CsDatabase -Update -ConfiguredDatabases -SqlServerFqdn <SQL Server FQDN>
    
      - Se il sistema è un server back-endEnterprise Edition e sono presenti database installati nel server, nella riga di comando digitare quanto segue:
        
            Install-CsDatabase -Update -ConfiguredDatabases -SqlServerFqdn <SQL Server FQDN>  -ExcludeCollocatedStores
    
      - Se il sistema è un server Standard Edition, nella riga di comando digitare quanto segue:
        
            Install-CsDatabase -Update -LocalDatabases

