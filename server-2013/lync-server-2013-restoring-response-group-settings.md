---
title: Ripristino delle impostazioni di Response Group
TOCTitle: Ripristino delle impostazioni di Response Group
ms:assetid: 4f8e1949-925d-4538-be1d-9ac7c06b2aca
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh202174(v=OCS.15)
ms:contentKeyID: 52062150
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ripristino delle impostazioni di Response Group

 

_**Ultima modifica dell'argomento:** 2013-02-18_

Se è stata distribuita l'applicazione Response Group ed è necessario ripristinare un Back End Server o un server Standard Edition, è inoltre necessario ripristinare le impostazioni di configurazione di Response Group.

## Per ripristinare le impostazioni di configurazione di Response Group

1.  Nella riga di comando digitare:
    
        Import-CsRgsConfiguration -Destination "service:ApplicationServer:<pool FQDN>" -OverwriteOwner -FileName "<path and file name of the backed up file at $Backup>"
    
    Ad esempio:
    
        Import-CsRgsConfiguration -Destination "service: ApplicationServer:pool01.contoso.com" -OverwriteOwner -FileName "C:\RgsConfiguration.zip"

