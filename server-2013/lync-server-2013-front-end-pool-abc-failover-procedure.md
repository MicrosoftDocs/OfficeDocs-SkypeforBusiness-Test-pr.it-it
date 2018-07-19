---
title: 'Lync Server 2013: Procedura di failover del pool ABC front-end'
TOCTitle: Procedura di failover del pool ABC front-end
ms:assetid: 67763ad3-6796-45eb-a486-901f21ac1a95
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945635(v=OCS.15)
ms:contentKeyID: 52062178
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Procedura di failover del pool ABC front-end in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-05-22_

Utilizzare i passaggi seguenti per eseguire la procedura di failover ABC. Nella procedura è disponibile una descrizione di alto livello di ogni passaggio, seguita dai comandi e dai cmdlet da eseguire per ogni passaggio.

Per eseguire i cmdlet, aprire Lync Server Management Shell con Esegui come amministratore.

## Per eseguire un failover ABC

1.  Controllare se il pool A è l'host per il server di gestione centrale.
    
      - Eseguire il cmdlet seguente:
        
            Get-CsService -CentralManagement
        
        Se il campo dell'identità del server di gestione centrale attivo punta al nome di dominio completo (FQDN) del pool A, è possibile utilizzare i passaggi 2 e 3 della procedura per eseguire prima di tutto il failover del server di gestione centrale. In caso contrario, procedere al passaggio 4.

2.  Eseguire il failover del server di gestione centrale al pool B in modalità di ripristino di emergenza eseguendo il cmdlet seguente:
    
        Invoke-CsManagementServerFailover -BackupSqlServerFqdn <Pool B BE FQDN> -BackupSqlInstanceName <Pool B BE instance name> [-BackupMirrorSqlServerFqdn <Pool B Mirror BE FQDN> -BackupMirrorSqlInstanceName <Pool B Mirror BE Instance name>] -Force -Verbose
    
    È quindi consigliabile spostare il server di archivio centrale dal pool B in un altro pool accoppiato esistente per ottenere ulteriore resilienza. Per informazioni dettagliate, vedere [Move-CsManagementServer](https://docs.microsoft.com/en-us/powershell/module/skype/Move-CsManagementServer).

3.  Se il pool A contiene il server di gestione centrale, importare la configurazione LIS dal database LIS (Lis.mdf) del pool A a quello del pool B. Ciò funzionerà solo se è stato eseguito un backup regolare dei dati LIS. Per importare la configurazione LIS, eseguire i cmdlet seguenti:
    
        Import-CsLisConfiguration -FileName <String> 
        Publish-CsLisConfiguration

4.  Importare i flussi di lavoro di backup del servizio Response Group di Lync Server dal pool A al pool B.
    

    > [!NOTE]
    > Attualmente, per il cmdlet <STRONG>Import-CsRgsConfiguration</STRONG> è necessario che i nomi delle code e dei flussi di lavoro nel pool A siano distinti da quelli nel pool B. In caso contrario, verrà visualizzato un errore quando si esegue il cmdlet <STRONG>Import-CsRgsConfiguration</STRONG> e le code e i flussi di lavoro dovranno essere rinominati nel pool B prima di procedere con il cmdlet <STRONG>Import-CsRgsConfiguration</STRONG>.

    
    Per importare la configurazione di Response Group dal pool A al pool B esistono due opzioni. La scelta dipende dal fatto che si desideri o meno sovrascrivere le impostazioni a livello di applicazione del pool B con quelle nel pool A.
    
      - Se si desidera sovrascrivere le impostazioni del pool B, eseguire il cmdlet **Import-CsRgsConfiguration** con l'opzione **ReplaceExistingSettings** :
        
            Import-CsRgsConfiguration -Destination "service:ApplicationServer:<Pool B FQDN>" -FileName "C:\RgsExportPrimary.zip"  -ReplaceExistingRgsSettings
    
      - Se non si desidera sovrascrivere le impostazioni del pool B, utilizzare il cmdlet **Import-CsRgsConfiguration** senza l'opzione **ReplaceExistingSettings** :
        
            Import-CsRgsConfiguration -Destination "service:ApplicationServer:<Pool B FQDN>" -FileName "C:\RgsExportPrimary.zip"
    

    > [!WARNING]
    > Tenere presente che se non si desidera sovrascrivere le impostazioni a livello di applicazione del pool di backup (pool B) con le impostazioni del pool principale (pool A), le impostazioni a livello di applicazione del pool A andranno perdute, perché l'applicazione Response Group può archiviare un solo set di impostazioni a livello di applicazione per pool. Quando si distribuisce il pool C per sostituire il pool A, le impostazioni a livello di applicazione devono essere riconfigurate, incluso il file audio della musica di attesa predefinita.



5.  Verificare che l'importazione della configurazione di Response Group sia stata eseguita correttamente eseguendo i cmdlet seguenti per visualizzare i Response Group importati. Notare che tali Response Group sono ancora di proprietà del pool A.
    
        Get-CsRgsWorkflow -Identity "service:ApplicationServer:<Pool B FQDN>" -Owner "service:ApplicationServer:<Pool A FQDN>"
        
        Get-CsRgsQueue -Identity "service:ApplicationServer:<Pool B FQDN>" -Owner "service:ApplicationServer:<Pool A FQDN>"
        
        Get-CsRgsAgentGroup -Identity "service:ApplicationServer:<Pool B FQDN>" -Owner "service:ApplicationServer:<Pool A FQDN>"

6.  Per i numeri non assegnati, spostare gli intervalli di numeri non assegnati che utilizzano "Annuncio" come servizio annuncio selezionato dal pool A al pool B. A tale scopo:
    
      - Ricreare tutti gli annunci distribuiti nel pool A nel pool B. Se durante la distribuzione degli annunci nel pool A sono stati utilizzati eventuali file audio, tali file saranno necessari per ricreare gli annunci nel pool B. Per ricreare gli annunci nel pool B, utilizzare i cmdlet **New-CsAnnouncement**, con il pool B come servizio padre.
    
      - Riassegnare tutti gli intervalli di numeri non assegnati che sono associati a un annuncio nel pool A agli annunci appena distribuiti nel pool B. Eseguire il cmdlet seguente per ogni intervallo di numeri non assegnati riferito a un annuncio del pool A:
        
            Set-CsUnassignedNumber -Identity "<Range Name>" -AnnouncementService "<Pool B FQDN>" -AnnouncementName "<New Announcement in pool B>"
    

    > [!NOTE]
    > Questo passaggio non è necessario per gli intervalli di numeri non assegnati che utilizzano "Messaggistica unificata di Exchange" come servizio annuncio selezionato.



7.  Eseguire il failover del pool A al pool B in modalità di ripristino di emergenza eseguendo il cmdlet seguente:
    
        Invoke-CsPoolFailover -PoolFqdn <Pool A FQDN> -DisasterMode

8.  Creare il pool C, ma non avviare alcun servizio nel pool C.
    
    Notare che questo passaggio può essere eseguito in contemporanea con i passaggi 5 e 6.

9.  Forzare lo spostamento degli utenti ospitati nel pool A al pool C eseguendo il cmdlet seguente:
    
        Get-csuser -Filter {RegistrarPool -eq "<Pool A FQDN>"} | Move-CsUser -Target <Pool C FQDN> -Force
    
    A questo punto, gli utenti ospitati nel pool A inizieranno a sperimentare un'interruzione dei servizi, che continuerà fino al passaggio 16, quando i servizi verranno avviati nel pool C.

10. Forzare lo spostamento della directory conferenze dal pool A al pool C eseguendo il cmdlet seguente:
    
        Move-CsConferenceDirectory -Identity <Conference Directory ID of Pool A> -TargetPool <Pool C FQDN> -Force

11. Forzare lo spostamento dell'oggetto contatto di Operatore automatico conferenza dal pool A al pool C eseguendo il cmdlet seguente:
    
        Move-csApplicationEndpoint -Identity "<Pool A CAA Uri>" -targetApplicationPool <Pool C FQDN> -force

12. Copiare il contenuto delle conferenze dal pool B al pool C.

13. Esportare i dati utente dal pool B e importarli nel pool C eseguendo i cmdlet seguenti:
    
        Export-CsUserData -PoolFqdn <Pool B Fqdn> -FileName <String>
        Import-CsUserData -PoolFqdn <Pool C Fqdn> -FileName <String>

14. Ripristinare i dati di backup dell'applicazione Parcheggio di chiamata dal pool A al pool C e assegnare al pool C l'intervallo di codici orbit del parcheggio di chiamata del pool A.
    
      - È possibile riassegnare un intervallo di codici orbit del parcheggio di chiamata del pool A al pool C tramite il Pannello di controllo di Lync Server o Lync Server Management Shell. Da Lync Server Management Shell eseguire il cmdlet seguente per ogni intervallo di codici orbit del parcheggio di chiamata assegnato al pool A (si noti che il parametro Identity fa riferimento agli intervalli di codici orbit del parcheggio di chiamata appartenenti al pool A):
        
            Set-CsCallParkOrbit -Identity "<Call Park Orbit Identity>" -CallParkService "service:ApplicationServer:<Pool C FQDN>"
    
      - Se per il parcheggio di chiamata nel pool A è stata configurata una musica di attesa personalizzata, ripristinare il file della musica di attesa personalizzata nel pool C.
        
            Xcopy <Source> <Destination: Pool C CPS File Store Path>
        
        Ad esempio:
        
            Xcopy "Source Path" "<Pool C File Store Path>\OcsFileStore\coX-ApplicationServer-X\AppServerFiles\CPS\"
    
      - Riconfigurare infine le impostazioni del parcheggio di chiamata nel pool C utilizzando il cmdlet **Set-CsCpsConfiguration**. L'applicazione Parcheggio di chiamata consente l'archiviazione di un solo set di impostazioni e un solo file audio della musica di attesa personalizzata per pool e tali impostazioni non vengono incluse nei backup o preservate in caso di emergenza.

15. Se il pool hop successivo per Chat persistente punta al pool A, modificare la topologia e pubblicare le modifiche, in modo che il server hop successivo punti al pool C.
    
      - Nel Generatore di topologie modificare il pool di Chat persistente in modo che punti al pool C come hop successivo. A tale scopo, fare clic con il pulsante destro del mouse sul pool di Chat persistente, fare clic sulla scheda **Generale** e quindi digitare il nome del pool C in **Pool hop successivo** .
    
      - Avviare i servizi nel pool C eseguendo il cmdlet seguente:
        
            Start-csWindowsService
    
    A questo punto, l'interruzione dei servizi termina per gli utenti originalmente ospitati nel pool A.

16. Esportare i flussi di lavoro del servizio Response Group di Lync Server dal pool B di proprietà del pool A per importarli nel pool C eseguendo i cmdlet seguenti:
    
        Export-CsRgsConfiguration -Source "service:ApplicationServer:<Pool B FQDN>" -Owner "service:ApplicationServer:<Pool A FQDN>" -FileName "C:\RgsExportPrimaryUpdated.zip" 

17. Importare i flussi di lavoro del servizio Response Group di Lync Server nel pool C dal pool B.
    
    Per importare la configurazione di Response Group dal pool B al pool C esistono due opzioni. La scelta dipende dal fatto che si desideri o meno sovrascrivere le impostazioni a livello di applicazione del pool C con quelle nel pool B.
    
      - Se si desidera sovrascrivere le impostazioni del pool C, eseguire il cmdlet **Import-CsRgsConfiguration** con l'opzione **ReplaceExistingSettings** :
        
            Import-CsRgsConfiguration -Destination "service:ApplicationServer:<Pool C FQDN>" -FileName "C:\RgsExportPrimary.zip"  -ReplaceExistingRgsSettings
    
      - Se non si desidera sovrascrivere le impostazioni del pool C, utilizzare il cmdlet **Import-CsRgsConfiguration** senza l'opzione **ReplaceExistingSettings** :
        
            Import-CsRgsConfiguration -Destination "service:ApplicationServer:<Pool B FQDN>" -FileName "C:\RgsExportPrimary.zip"
    

    > [!WARNING]
    > Tenere presente che se non si desidera sovrascrivere le impostazioni a livello di applicazione del pool C con le impostazioni del pool di backup (pool B), le impostazioni a livello di applicazione del pool B andranno perdute, perché l'applicazione Response Group può archiviare un solo set di impostazioni a livello di applicazione per pool.



18. Verificare che l'importazione della configurazione di Response Group sia stata eseguita correttamente eseguendo i cmdlet seguenti per visualizzare i Response Group importati nel pool C.
    
        Get-CsRgsWorkflow -Identity "service:ApplicationServer:<Pool C FQDN>" -ShowAll
         Get-CsRgsQueue -Identity "service:ApplicationServer:<Pool C FQDN>" -ShowAll
        Get-CsRgsAgentGroup -Identity "service:ApplicationServer:<Pool C FQDN>" -ShowAll

19. Dopo aver verificato la configurazione importata nel pool C, rimuovere dal pool B i Response Group di proprietà del pool principale. Verrà così ridotto al minimo il tempo di inattività dei Response Group.
    
    Questo passaggio consente di creare un nuovo file con la configurazione esportata e quindi di rimuoverlo dal pool B.
    
        Export-CsRgsConfiguration -Source "service:ApplicationServer:<Pool B FQDN>" -Owner "service:ApplicationServer:<Pool A FQDN>" -FileName "C:\RgsExportPrimaryUpdated.zip" -RemoveExportedConfiguration

20. Spostare nel pool C gli intervalli di numeri non assegnati spostati dal pool A al pool B.
    
      - Ricreare nel pool C tutti gli annunci ricreati dal pool A nel pool B. Se durante la distribuzione degli annunci da spostare sono stati utilizzati eventuali file audio, sarà necessario utilizzare tali file per ricreare gli annunci nel pool C. Per ricreare gli annunci nel pool C, utilizzare i cmdlet **New-CsAnnouncement**, con il pool C come servizio padre.
    
      - Riassegnare al pool C tutti gli intervalli di numeri non assegnati riassegnati dal pool A al pool B. Eseguire il cmdlet seguente per ogni intervallo di numeri non assegnati che deve essere riassegnato:
        
            Set-CsUnassignedNumber -Identity "<Range Name>" -AnnouncementService "<Pool C FQDN>" -AnnouncementName "<New Announcement in pool C>"
    
      - (Facoltativo) Rimuovere dal pool B gli annunci ricreati nel pool C se non sono più in uso nel pool B. Per rimuovere gli annunci, utilizzare il cmdlet **Remove-CsAnnouncement**.
        

        > [!NOTE]
        > Questo passaggio non è necessario per gli intervalli di numeri non assegnati che utilizzano "Messaggistica unificata di Exchange" come servizio annuncio.



21. Pulire i dati utente del pool A nel pool B eseguendo il cmdlet seguente:
    
        Remove-CsUserStoreBackupData -PoolFqdn <Pool B FQDN> -Verbose

22. Eseguire le operazioni seguenti in Generatore di topologie:
    
      - Rimuovere l'accoppiamento tra il pool A e il pool B, quindi accoppiare i pool B e C. Rimuovere il pool A dalla topologia e pubblicarla. A tale scopo:
        
          - In Generatore di topologie fare clic con il pulsante destro del mouse sul pool B e quindi scegliere **Modifica proprietà** .
        
          - Fare clic su **Resilienza** nel riquadro sinistro.
        
          - Nella casella sotto **Pool di backup associato** selezionare il pool C. Notare che nella casella di selezione Pool di backup associato sarà inizialmente visualizzato il pool A, perché il pool B era precedentemente associato a questo pool.
        
          - Selezionare **Failover e failback automatico per VoIP** , quindi fare clic su **OK** .
            
            Quando vengono visualizzati i dettagli su questo pool, il pool associato apparirà nel riquadro a destra sotto **Resilienza** .
        
          - Nell'albero della console fare clic con il pulsante destro del mouse sul pool A e quindi scegliere Elimina.
        
          - Pubblicare la topologia.

23. Eseguire l'applicazione di avvio nel pool C per installare l'applicazione del servizio di backup, quindi avviare l'applicazione del servizio di backup eseguendo il comando seguente dalla cartella di distribuzione in un computer locale nel pool C:
    
        Run "%SYSTEMROOT%\Program Files\Microsoft Lync Server 2013\Deployment\Bootstrapper.exe"
        Start-CsWindowsService -name LyncBackup

24. Riavviare l'applicazione del servizio di backup nel pool B eseguendo i cmdlet seguenti:
    
        Stop-CsWindowsService -name LyncBackup
        Start-CsWindowsService -name LyncBackup

25. Se il pool C è un pool Standard Edition e nel pool B è installato il server di gestione centrale, installare manualmente il database del server di gestione centrale nel pool C eseguendo il cmdlet seguente:
    
        Install-CsDatabase -CentralManagementDatabase -SqlServerFqdn <Pool C FQDN> -SqlInstanceName rtc

26. Richiamare il servizio di backup per sincronizzare il contenuto delle conferenze precedente dal pool B al pool C generato dopo l'accoppiamento di B e C, nonché per sincronizzare il nuovo contenuto delle conferenze dal pool C al pool B generato dopo l'avvio del pool C e prima dell'accoppiamento di B e C. A tale scopo, eseguire i cmdlet seguenti:
    
        Invoke-CsBackupServiceSync -PoolFqdn <Pool C FQDN>
        Invoke-CsBackupServiceSync -PoolFqdn <Pool B FQDN>

27. Per ogni Survivable Branch Appliance X associato al pool A:
    
      - Arrestare Survivable Branch Appliance X eseguendo il cmdlet seguente:
        
            Stop-CsWindowsService
    
      - Creare un file contenente un elenco di utenti ospitati in Survivable Branch Appliance X. L'elenco sarà necessario quando gli utenti verranno spostati di nuovo in Survivable Branch Appliance X nel passaggio 30. A tale scopo, eseguire il cmdlet seguente:
        
            Get-CsUser -Filter {RegistrarPool -eq "<SBA X FQDN>"} | Export-Csv d:\sbaxusers.txt
    
      - Forzare lo spostamento degli utenti ospitati nel Survivable Branch Appliance X al pool C eseguendo il cmdlet seguente:
        
            Get-CsUser -Filter {RegistrarPool -eq "<SBA X FQDN>"} | Move-CsUser -Target <Pool C FQDN> -Force -Verbose
    
      - Aggiornare i dati di questi utenti eseguendo prima di tutto i cmdlet seguenti:
        
            Convert-csUserData -InputFile <Data file exported from PoolB> -OutputFile c:\Logs\ExportedUserData.xml -TargetVersionLync2010 
            $a=get-csuser -Filter {RegistrarPool -eq "FQDN of SBA X"} | select SipAddress
            foreach($x in $a) {$x.SipAddress.Substring(4) >> users.txt}
        
        Quindi eseguire questo script:
        
            $users=gc c:\logs\users.txt
            foreach ($user in $users)
            {
            Update-CsUserData -FileName c:\logs\exportedUserDAta.xml -UserFilter $user - 
            }
        

        > [!NOTE]
        > Si verificherà un'interruzione dei servizi per gli utenti ospitati in Survivable Branch Appliance associati al pool A, fino a quando non viene completato lo spostamento di questi utenti nel pool C.



28. In Generatore di topologie, per ogni Survivable Branch Appliance X precedentemente associato al pool A, eseguire le operazioni seguenti:
    
      - Impostare l'associazione al pool C. A tale scopo, fare clic sul sito di succursale, espandere il nodo Survivable Branch Appliance o Server e fare clic su **Survivable Branch Appliance** . Selezionare quindi il pool Front End e pool Servizi utente a cui verrà connesso questo Survivable Branch Appliance come pool C, quindi fare clic su **Avanti** .
    
      - Pubblicare la topologia. A tale scopo, nell'albero della console fare clic con il pulsante destro del mouse sul nuovo **Survivable Branch Appliance** , scegliere **Topologia** e quindi fare clic su **Pubblica** .

29. Per ogni Survivable Branch Appliance X ora associato al pool C:
    
      - Avviare Survivable Branch Appliance X eseguendo il cmdlet seguente nel Survivable Branch Appliance:
        
            Start-CsWindowsService
    
      - Spostare gli utenti originalmente ospitati nel Survivable Branch Appliance X dal pool C al Survivable Branch Appliance X eseguendo il cmdlet seguente:
        
            Import-Csv d:\sbaxusers.txt | Move-CsUser -Target <SBA X FQDN> -Force

