---
title: Monitoraggio dei file di registro di traccia delle richieste IIS
TOCTitle: Monitoraggio dei file di registro di traccia delle richieste IIS
ms:assetid: b6730e92-6d74-4fa7-a83f-50b7bdadbffa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690034(v=OCS.15)
ms:contentKeyID: 49301741
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Monitoraggio dei file di registro di traccia delle richieste IIS

 

_**Ultima modifica dell'argomento:** 2013-02-14_

Quando si abilita la traccia delle richieste di Internet Information Services (IIS) per il servizio per dispositivi mobili di Lync Server, i file di log generati possono occupare fino a 3 gigabyte di spazio su disco al giorno. La registrazione della traccia IIS è abilitata per impostazione predefinita. È consigliabile monitorare i Front End Server per assicurarsi che lo spazio su disco non diventi insufficiente.

Per impostazione predefinita, in IIS i file di registro vengono archiviati in %SystemDrive%\\inetpub\\logs\\LogFiles.

Per disattivare la traccia delle richieste di IIS per un intero server, digitare il comando seguente alla riga di comando:

    %SystemDrive%\Windows\System32\inetsrv\appcmd set config /section:httpLogging /dontLog:True

Per informazioni dettagliate sul comando **httpLogging**, vedere [http://go.microsoft.com/fwlink/?linkid=234927\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=234927%26clcid=0x410).

