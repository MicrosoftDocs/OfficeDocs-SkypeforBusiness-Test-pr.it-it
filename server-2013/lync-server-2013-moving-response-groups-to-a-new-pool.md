---
title: Spostamento dei Response Group in un nuovo pool
TOCTitle: Spostamento dei Response Group in un nuovo pool
ms:assetid: da0db765-41e5-430b-b5a7-5418ec5ff2a7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205298(v=OCS.15)
ms:contentKeyID: 49302150
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Spostamento dei Response Group in un nuovo pool

 

_**Ultima modifica dell'argomento:** 2012-11-01_

In Lync Server 2013 è stato introdotto il supporto di nuovi cmdlet per lo spostamento di Response Group da un pool a un altro, anche con nomi di dominio completo (FQDN) diversi.

Eseguire i passaggi della procedura seguente per spostare i Response Group da un pool Front End a un altro pool Front End con FQDN diverso.


> [!NOTE]
> In un ambiente di coesistenza è possibile spostare i Response Group solo tra pool Front Enddi Lync Server 2013.



## Per spostare i Response Group in un pool con un FQDN diverso

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Esportare i Response Group del pool di origine. Nella riga di comando digitare:
    
        Export-CsRgsConfiguration -Source "service:ApplicationServer:<source FQDN>" -FileName "<export file name>"
    
    Ad esempio:
    
        Export-CsRgsConfiguration -Source "service:ApplicationServer:source.contoso.com" -FileName "C:\RgsExportSource.zip"
    
    Per rimuovere i Response Group dal pool di origine durante l'esportazione, includere il parametro -RemoveExportedConfiguration, ad esempio:
    
        Export-CsRgsConfiguration -Source ApplicationServer:source.contoso.com -FileName "C:\RgsExportSource.zip" -RemoveExportedConfiguration

3.  Importare i Response Group nel pool di destinazione e assegnare il pool di destinazione come nuovo proprietario. Nella riga di comando digitare:
    
        Import-CsRgsConfiguration -Destination "service:ApplicationServer:<destination pool>" -FileName "<export file name>" -OverwriteOwner
    
    Se inoltre si desidera copiare le impostazioni a livello di applicazione di Response Group dal pool di origine nel pool di destinazione, includere il parametro -ReplaceExistingSettings. È possibile definire un solo insieme di impostazioni a livello di applicazione per ogni pool. Se si copiano le impostazioni a livello di applicazione dal pool di origine nel pool di destinazione, le impostazioni del pool di origine sostituiranno quelle del pool di destinazione. Se invece non si copiano le impostazioni a livello di applicazione dal pool di origine, le impostazioni esistenti del pool di destinazione si applicheranno ai Response Group importati.
    
    Ad esempio:
    
        Import-CsRgsConfiguration -Destination "service:ApplicationServer:destination.contoso.com" -FileName "C:\RgsExportSource.zip" -OverwriteOwner -ReplaceExistingSettings
    

    > [!NOTE]
    > Le impostazioni a livello di applicazione includono la configurazione della musica di attesa predefinita, il file audio della musica di attesa predefinito, il periodo di tolleranza di richiamata degli agenti e la configurazione del contesto chiamata. Per visualizzare queste impostazioni di configurazione, eseguire il cmdlet <STRONG>Get-CsRgsConfiguration</STRONG>. Per informazioni dettagliate su questo cmdlet, vedere <A href="get-csrgsconfiguration.md">Get-CsRgsConfiguration</A>.



4.  Verificare che l'importazione sia stata eseguita correttamente visualizzando la configurazione dei Response Group importati. A tale scopo:
    
      - Verificare che siano stati importati tutti i flussi di lavoro. Nella riga di comando digitare quanto segue:
        
            Get-CsRgsWorkflow -Identity "service:ApplicationServer:<destination pool FQDN>"
    
      - Verificare che siano state importate tutte le code. Nella riga di comando digitare quanto segue:
        
            Get-CsRgsQueue -Identity "service:ApplicationServer:<destination pool FQDN>"
    
      - Verificare che siano stati importati tutti i gruppi di agenti. Nella riga di comando digitare quanto segue:
        
            Get-CsRgsAgentGroup -Identity "service:ApplicationServer:<destination pool FQDN>"
    
      - Verificare che siano stati importati tutti gli orari di ufficio. Nella riga di comando digitare quanto segue:
        
            Get-CsRgsHoursOfBusiness -Identity "service:ApplicationServer:<destination pool FQDN>" 
    
      - Verificare che siano stati importati tutti i set di festività. Nella riga di comando digitare quanto segue:
        
            Get-CsRgsHolidaySet -Identity "service:ApplicationServer:<destination pool FQDN>" 

5.  Verificare che l'importazione sia stata eseguita correttamente effettuando una chiamata a uno dei Response Group e controllando che la chiamata venga gestita correttamente.

6.  Richiedere agli agenti membri di gruppi di agenti formali di eseguire l'accesso ai gruppi di agenti corrispondenti nel pool di destinazione.

7.  Se i Response Group non sono stati precedentemente rimossi dal pool di origine, procedere in tal senso. Nella riga di comando digitare:
    
        Export-CsRgsConfiguration -Source "service:ApplicationServer:<source pool FQDN> -RemoveExportedConfiguration -FileName "<temporary export file name>"
    
    Ad esempio:
    
        Export-CsRgsConfiguration -Source "service:ApplicationServer:source.contoso.com" -RemoveExportedConfiguration -FileName "C:\TempRGsConfiguration.zip"

