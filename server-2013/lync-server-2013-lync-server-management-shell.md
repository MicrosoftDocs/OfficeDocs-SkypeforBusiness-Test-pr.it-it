---
title: Lync Server Management Shell
TOCTitle: Lync Server Management Shell
ms:assetid: 674b523b-c0b7-4ed6-9e67-afa6e8ac7e12
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398474(v=OCS.15)
ms:contentKeyID: 49300822
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Server Management Shell

 

_**Ultima modifica dell'argomento:** 2012-06-20_

In Microsoft Lync Server 2010 è stata introdotta una vasta gamma di funzionalità nuove e migliorate rispetto a quelle disponibili in Microsoft Office Communications Server 2007 R2. Uno di questi miglioramenti riguarda la modalità di gestione dell'implementazione. Ad esempio, è disponibile una nuova interfaccia utente, denominata Pannello di controllo di Lync Server, che rappresenta una vera rivoluzione rispetto all'interfaccia a cui gran parte degli utenti è abituato in Microsoft Management Console. L'altro miglioramento importante in termini di gestibilità è rappresentato dall'inclusione di Windows PowerShell.

Windows PowerShell consente di gestire le applicazioni Microsoft dalla riga di comando. Include un ambiente da riga di comando, comandi specifici del prodotto e un linguaggio di script completo. Windows PowerShell è stato introdotto inizialmente con versione scaricabile per il sistema operativo Windows alla fine del 2006 ed è stato incorporato come interfaccia delle riga di comando per la gestibilità di Microsoft Exchange Server 2007. Da quel momento è stato continuamente esteso e incorporato nella maggior parte dei prodotti server Microsoft, il più recente dei quali è Microsoft Lync Server 2013. In Lync Server 2010 sono stati introdotti quasi 550 cmdlet specifici per il prodotto, utilizzabili per gestire ogni aspetto della distribuzione.

Nelle sezioni seguenti è disponibile un elenco dei cmdlet e relative descrizioni. Queste informazioni sono disponibili anche direttamente dalla riga di comando. È sufficiente digitare il comando seguente al prompt dei comandi di Lync Server Management Shell:

    Get-Help <cmdlet name> -Full

Per recuperare le informazioni della Guida dal prompt dei comandi nel cmdlet **New-CsVoicePolicy**, ad esempio, digitare il comando seguente:

    Get-Help New-CsVoicePolicy -Full

Aspetti da tenere presente relativamente a Windows PowerShell in Lync Server 2013:

  - Per eseguire i cmdlet di Lync Server, aprire Lync Server Management Shell.
    

    > [!WARNING]
    > Se si apre una finestra di Windows PowerShell anziché Lync Server Management Shell, per impostazione predefinita non sarà possibile eseguire i cmdlet di Lync Server. Per eseguire i cmdlet di Lync Server da Windows PowerShell, digitare innanzitutto il comando seguente al prompt dei comandi di Windows PowerShell:<BR>Import-Module Lync



  - Lync Server Management Shell viene installato automaticamente in tutti i server Lync Server Enterprise Edition Front End Server o Standard Edition.

  - Informazioni nuove e aggiornare, script di esempio e informazioni della Guida introduttive e approfondite sui cmdlet di Windows PowerShell e Microsoft Lync Server 2013 sono disponibili nel blog di Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/?linkid=203150\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x410).

