---
title: 'Lync Server 2013: Requisiti di sistema per i server Lync Server 2013'
TOCTitle: Requisiti di sistema per i server Lync Server 2013
ms:assetid: 781d487d-5958-416a-becb-904d9af3cc0a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398588(v=OCS.15)
ms:contentKeyID: 49301035
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti di sistema per i server Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-07-24_


> [!NOTE]
> Per dettagli sui requisiti hardware, vedere <A href="lync-server-2013-server-hardware-platforms.md">Piattaforme hardware server per Lync Server 2013</A>.



I server Standard Edition e Enterprise Edition condividono gli stessi requisiti software.

I server che eseguono Lync Server 2013 Enterprise Edition sono adatti per le organizzazioni di grandi dimensioni come principale distribuzione organizzativa. Il server Enterprise Edition è stato progettato per una scalabilità fino a circa 80.000 utenti ospitati per pool. I server che eseguono Lync Server 2013 Standard Edition sono concepiti per organizzazioni più piccole e località lontane dalla distribuzione dell'organizzazione principale. Una coppia di server Standard Edition può supportare fino a 5.000 utenti. Per altri dettagli sulla differenza tra server Standard Edition e server Enterprise Edition, vedere [Panoramica della distribuzione per Lync Server 2013](lync-server-2013-deployment-overview.md).

## Installazione del sistema operativo

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Lync Server 2013 è disponibile solo in un'edizione a 64 bit, per cui sono necessari hardware a 64 bit e l'edizione a 64 bit del sistema operativo Windows Server. Con questa versione non è disponibile un'edizione a 32 bit di Lync Server 2013.</td>
</tr>
</tbody>
</table>


Il server Standard Edition Enterprise può utilizzare uno dei sistemi operativi seguenti:

  - Windows Server 2008 R2 SP1 o service pack più recente

  - Windows Server 2012

  - Windows Server 2012 R2

Installare il software del sistema operativo sul server Standard Edition o in Enterprise Edition Front End Server. Applicare tutti gli aggiornamenti in ordine fino a installare il più recente e ottenere il livello di aggiornamento del sistema operativo necessario, coerente con gli standard dell'organizzazione. Per maggiori dettagli sui requisiti di funzionamento, vedere [Supporto del sistema operativo per server e strumenti in Lync Server 2013](lync-server-2013-server-and-tools-operating-system-support.md) nella documentazione relativa alla supportabilità.


> [!NOTE]
> Per garantire la compatibilità di Lync Server 2013 con Windows Server 2012 R2, potrebbe essere necessario modificare il valore di una chiave del Registro di sistema in Windows Server. Questa modifica può essere necessaria per il corretto funzionamento dei certificati e per la registrazione dei client a Survivable Branch Appliance. Per ulteriori informazioni, vedere <A class=uri href="http://support.microsoft.com/kb/2901554">http://support.microsoft.com/kb/2901554</A>.



## Software aggiuntivo per Lync Server 2013

Oltre agli aggiornamenti necessari per il sistema operativo, per il corretto funzionamento di Lync Server 2013 sono necessari altri ruoli del sistema operativo, caratteristiche e software specifici. Per informazioni dettagliate sul software aggiuntivo che deve essere installato prima di pubblicare la topologia e installare Lync Server 2013, vedere [Requisiti software aggiuntivi per Lync Server 2013](lync-server-2013-additional-software-requirements.md) nella documentazione relativa alla pianificazione.

## Software aggiuntivo necessario per tutti i ruoli del server

In tutti i ruoli del server è necessario verificare che siano installati interfaccia della riga di comando Windows PowerShell 3.0 e Microsoft .NET Framework 4.5.

Inoltre, interfaccia della riga di comando Windows PowerShell 3.0 e Microsoft .NET Framework 4.5 sono necessari su tutti i computer in cui saranno eseguiti gli strumenti amministrativi di Lync Server.

## Windows PowerShell 3.0

Lync Server 2013 richiede l'installazione di Windows PowerShell 3.0 su ciascun computer che appartiene alla topologia di Lync Server. Per informazioni sull'installazione di Windows PowerShell 3.0, vedere [Installazione di Windows PowerShell 3.0 per Lync Server 2013](lync-server-2013-installing-windows-powershell-3-0.md).


> [!NOTE]
> Su Windows Server&nbsp;2008&nbsp;R2 con SP1, non è possibile installare interfaccia della riga di comando Windows PowerShell 3.0 prima che sia installato Microsoft .NET Framework 4.5.



## Microsoft .NET Framework 4.5

Quando si installa Microsoft .NET Framework 4.5 su server che eseguiranno Lync Server 2013 in Windows Server 2012 o Windows Server 2012 R2, è necessario eseguire un ulteriore passaggio. Dopo l'installazione di .NET Framework 4.5, utilizzare Server Manager per installare il programma di attivazione di HTTP.

**Installazione del programma di attivazione di HTTP di .NET 4.5 in Windows Server 2012 o Windows Server 2012 R2**

1.  Dal menu **Start** , fare clic su **Programmi** , selezionare **Strumenti di amministrazione** e fare clic su **Server Manager**.

2.  In Server Manager, sotto **Riepilogo funzionalità** , selezionare **Aggiungi funzionalità**.

3.  Espandere **.NET Framework 4.5**.

4.  Se deselezionato, selezionare **Attivazione WCF** , quindi selezionare **Attivazione HTTP**.

5.  Fare clic su **Avanti** e completare i passaggi dell'installazione.

