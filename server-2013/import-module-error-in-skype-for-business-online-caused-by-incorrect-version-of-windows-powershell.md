---
title: Errore del modulo di importazione causato da una versione errata di Windows PowerShell
TOCTitle: Errore del modulo di importazione causato da una versione errata di Windows PowerShell
ms:assetid: 6c209f41-2b97-4dda-b0b7-e5b582d3e6b6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362802(v=OCS.15)
ms:contentKeyID: 56269922
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Errore del modulo di importazione causato da una versione errata di Windows PowerShell

 

_**Ultima modifica dell'argomento:** 2015-06-22_

II modulo del connettore di Skype for Business online può essere eseguito solo in Windows PowerShell 3.0. Se si cerca di importare il modulo in una versione precedente di Windows PowerShell, il processo di importazione non riesce e viene visualizzato un messaggio di errore analogo al seguente:

    Import-Module: La versione di Windows PowerShell caricata è '2.0'. Per eseguire il modulo 'D:\Programmi\File comuni\Microsoft Lync Server 2013\Modules\LyncOnlineConnector\LyncOnlineConnector.psd1' è necessaria almeno la versione '3.0' di Windows PowerShell. Verificare l'installazione di Windows PowerShell e riprovare.

L'unica soluzione a questo problema è l'installazione di Windows PowerShell 3.0, disponibile nell'Area download Microsoft all'indirizzo <http://www.microsoft.com/en-us/download/details.aspx?id=29939>.

## Vedere anche

#### Concetti

[Diagnosi e risoluzione dei problemi di connessione di Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

