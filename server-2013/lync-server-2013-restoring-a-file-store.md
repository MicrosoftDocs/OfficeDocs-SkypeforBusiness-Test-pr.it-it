---
title: Ripristino di un archivio file
TOCTitle: Ripristino di un archivio file
ms:assetid: 89916fc6-31d3-4c7f-9eaf-c02584761ef4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh202180(v=OCS.15)
ms:contentKeyID: 52062208
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ripristino di un archivio file

 

_**Ultima modifica dell'argomento:** 2013-02-18_

Gli archivi file per Standard Edition si trovano in genere nel server Standard Edition. Gli archivi file per Enterprise Edition si trovano in genere in un file server o in un cluster. La procedura seguente descrive come ripristinare un Archivio file.

## Per ripristinare un archivio file

1.  In caso di errore di un Archivio file, copiare l'Archivio file appropriato da $Backup\\ al percorso dell'Archivio file nel file server o nel server Standard Edition e quindi condividere la cartella.
    
    > [!important]  
    > Il percorso e il nome file dell'Archivio file ripristinato devono essere identici a quelli dell'Archivio file di cui è stato eseguito il backup, in modo che i componenti che utilizzano i file possano accedervi.

2.  Se necessario, impostare gli elenchi di controllo di accesso per l'Archivio file. Nella riga di comando digitare:
    
        Enable-CsTopology
    

    > [!NOTE]
    > È necessario eseguire questa operazione solo se Generatore di topologie non è stato eseguito in altro modo durante il processo di ripristino.


