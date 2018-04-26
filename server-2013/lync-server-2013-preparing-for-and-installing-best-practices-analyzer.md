---
title: Preparazione e installazione di Best Practices Analyzer
TOCTitle: Preparazione e installazione di Best Practices Analyzer
ms:assetid: 550613dd-dc08-482e-9980-a3fe187cd162
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg591347(v=OCS.15)
ms:contentKeyID: 49300600
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Preparazione e installazione di Best Practices Analyzer

 

_**Ultima modifica dell'argomento:** 2013-11-07_

Per eseguire le attività descritte in questo argomento è necessario accedere con un account membro del gruppo Administrators.

## Requisiti di sistema per l'installazione di Best Practices Analyzer

Per eseguire Best Practices Analyzer di Lync Server 2013 per eseguire l'analisi dell'ambiente, nel computer deve essere in esecuzione una versione a 64 bit di uno dei sistemi operativi seguenti:

  - Windows Server 2008 R2 Service Pack 1 (SP1) Standard

  - Windows Server 2008 R2 SP1 Enterprise

  - Windows Server 2008 R2 SP1 Datacenter

  - Windows Server 2012 Datacenter

  - Windows Server 2012 Standard

  - Windows Server 2012 Enterprise

  - Sistema operativo Windows Server 2012 R2 Datacenter

  - Sistema operativo Windows Server 2012 R2 Standard

  - Sistema operativo Windows Server 2012 R2 Enterprise

  - Windows 8' '

  - Windows 7' '

Nel computer deve inoltre essere in esecuzione il software seguente:

  - Microsoft .NET Framework 4.5. Per Lync Server 2013 è necessario installare manualmente la versione a 64 bit di Microsoft .NET Framework 4.5 nel server prima di installare Lync Server 2013.

  - Componenti di base di Lync Server 2013.

  - Pacchetto di compatibilità con le versioni precedenti di Strumentazione gestione Windows (WMI). Per informazioni dettagliate, vedere [Installare il pacchetto di compatibilità con le versioni precedenti di WMI](install-wmi-backward-compatibility-package.md) nella documentazione relativa alla migrazione.

  - Windows PowerShell 3.0. Per informazioni dettagliate, vedere [Installazione di Windows PowerShell 3.0 per Lync Server 2013](lync-server-2013-installing-windows-powershell-3-0.md) nella documentazione relativa alla distribuzione.

È possibile installare Best Practices Analyzer in computer con un sistema operativo supportato ma senza i componenti di base di Lync Server 2013 o senza il pacchetto di compatibilità con le versioni precedenti di Strumentazione gestione Windows (WMI), ma in questi computer si potrà usare Best Practices Analyzer solo per visualizzare rapporti e non per eseguire analisi.

## Scelta del computer per l'installazione

È consigliabile installare Best Practices Analyzer di Lync Server 2013 in un computer dedicato alla gestione di Lync Server 2013. È possibile installare lo strumento in un server che esegue Lync Server 2013 o in un computer di amministrazione che esegue Lync Server 2013. Se si installa lo strumento in un server che esegue Lync Server, è consigliabile usare lo strumento per analizzare solo il server in cui è installato.

## Installazione di Best Practices Analyzer

È possibile scaricare Best Practices Analyzer per Lync Server 2013 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=266539\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=266539%26clcid=0x410).

Per installare Best Practices Analyzer, avviare il file di Microsoft Installer RtcBPA.msi nel computer in cui si vuole installare lo strumento e quindi seguire le istruzioni sullo schermo. Il percorso predefinito per l'installazione dei file di programma è *\<unità sistema\>*\\Program Files\\Lync Server 2013\\BPA.

