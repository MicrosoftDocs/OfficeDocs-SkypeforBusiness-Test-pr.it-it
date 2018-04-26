---
title: "Lync Server 2013: Esclusioni dall'analisi antivirus"
TOCTitle: Esclusioni dall'analisi antivirus per Lync Server 2013
ms:assetid: 71e1f1cc-2d16-4111-9864-9276bf24dfe0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn440138(v=OCS.15)
ms:contentKeyID: 59602739
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Esclusioni dall'analisi antivirus per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-02-26_

Per assicurarsi che il programma antivirus non interferisca con il funzionamento di Lync Server 2013, è necessario escludere determinati processi e directory per ciascun ruolo o ruolo server di Lync Server 2013 su cui viene eseguito il programma antivirus. Devono essere esclusi i processi e le directory seguenti:


> [!NOTE]
> I percorsi dei file e delle cartelle elencati di seguito sono i percorsi predefiniti per Lync Server 2013. Nel caso di percorsi per i quali non è stata usata l'impostazione predefinita, invece di quelli elencati in questo argomento escludere i percorsi specificati per la propria organizzazione.



  - Processi di Lync Server 2013:
    
      - ABServer.exe
    
      - AcpMcuSvc.exe
    
      - ASMCUSvc.exe
    
      - AVMCUSvc.exe
    
      - ChannelService.exe
    
      - ClsAgent.exe
    
      - ComplianceService.exe
    
      - DataMCUSvc.exe
    
      - DataProxy.exe
    
      - FileTransferAgent.exe
    
      - IMMCUSvc.exe
    
      - LysSvc.exe
    
      - MasterReplicatorAgent.exe
    
      - MediaRelaySvc.exe
    
      - MediationServerSvc.exe
    
      - MRASSvc.exe
    
      - OcsAppServerHost.exe
    
      - ReplicaReplicatorAgent.exe
    
      - ReplicationApp.exe
    
      - RtcHost.exe
    
      - RTCSrv.exe
    
      - XmppProxy.exe
    
      - XmppTGW.exe

  - Processi del servizio host Windows Fabric:
    
      - Fabric.exe
    
      - FabricDCA.exe
    
      - FabricHost.exe

  - Processi IIS:
    
      - %systemroot%\\system32\\inetsrv\\w3wp.exe
    
      - %systemroot%\\SysWOW64\\inetsrv\\w3wp.exe

  - Processi back-end di SQL Server:
    
      - %ProgramFiles%\\Microsoft SQL Server\\MSSQL11.MSSQLSERVER\\MSSQL\\Binn\\SQLServr.exe
    
      - %ProgramFiles%\\Microsoft SQL Server\\MSRS11.MSSQLSERVER\\Reporting Services\\ReportServer\\Bin\\ReportingServicesService.exe
    
      - %ProgramFiles%\\Microsoft SQL Server\\MSAS11.MSSQLSERVER\\OLAP\\Bin\\MSMDSrv.exe

  - Processi front-end di SQL Server:
    
      - %ProgramFiles%\\Microsoft SQL Server\\MSSQL11.LYNCLOCAL\\MSMQL\\Binn\\SQLServr.exe
    
      - %ProgramFiles%\\Microsoft SQL Server\\MSSQL11.RTCLOCAL\\MSMQL\\Binn\\SQLServr.exe

  - Directory e file:
    
      - %systemroot%\\System32\\LogFiles
    
      - %systemroot%\\SysWow64\\LogFiles
    
      - %systemroot%\\Microsoft.NET\\assembly\\GAC\_MSIL
    
      - %programfiles%\\Microsoft Lync Server 2013
    
      - %programfiles%\\Common Files\\Microsoft Lync Server 2013\\Watcher Node
    
      - %programfiles%\\Common Files\\Microsoft Lync Server 2013
    
      - %SystemDrive%\\RtcReplicaRoot
    
      - Archivio condivisione file (specificato in Generatore di topologie). Gli archivi file sono specificati in Generatore di topologie.
    
      - File di dati e di log di SQL Server, compresi quelli per database back-end, archivio utenti, archivio di archiviazione, archivio di monitoraggio e archivio applicazione. I file di database e di log possono essere specificati in Generatore di topologie. Per informazioni sui file di dati e di log per ciascun database, compresi i nomi predefiniti, vedere [Posizionamento dei file di log e dei file di dati di SQL Server per Lync Server 2013](lync-server-2013-sql-server-data-and-log-file-placement.md) nella documentazione relativa alla distribuzione.
    
      - File di dati e di log di SQL Server, compresi quelli per il database front-end, l'archivio Lync e l'archivio RtcDatabase. Questi si trovano in genere nel percorso %UnitàLocale%\\CSData.

