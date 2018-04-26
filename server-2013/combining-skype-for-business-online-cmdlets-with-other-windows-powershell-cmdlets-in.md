---
title: Combinazione di cmdlet di Lync Online con altri cmdlet di Windows PowerShell
TOCTitle: Combinazione di cmdlet di Lync Online con altri cmdlet di Windows PowerShell
ms:assetid: 8bb8800a-f966-4570-8c8b-db87a91ad783
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362816(v=OCS.15)
ms:contentKeyID: 56269938
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Combinazione di cmdlet di Lync Online con altri cmdlet di Windows PowerShell

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Quando ci si connette a Skype for Business online usando Windows PowerShell, saranno disponibili per l'uso circa 40 cmdlet di Skype for Business online. Nella gestione di Skype for Business online, tuttavia, non si è limitati all'uso di questi soli 40 cmdlet. Oltre ai cmdlet di Skype for Business online è possibile usare qualsiasi altro cmdlet di Windows PowerShell installato nel computer. Quando si installa Windows PowerShell 3.0 vengono infatti installati anche centinaia di cmdlet di sistema di Windows PowerShell. I comandi possono combinare i cmdlet di Skype for Business online e qualsiasi altro cmdlet disponibile nel computer.

Anche se un corso completo sull'uso di Windows PowerShell 3.0 esula dall'ambito di questo articolo, ecco alcuni esempi che illustrano i motivi per cui può essere utile combinare i cmdlet. Innanzitutto, nessun cmdlet di Skype for Business online include un comando di stampa e tale comando non è disponibile neanche nella console di Windows PowerShell. Se si vogliono stampare le informazioni recuperate da un cmdlet, è possibile recuperare le informazioni e quindi inviarle al cmdlet **Out-Printer**:

    Get-CsTenant | Out-Printer

Poiché non sono inclusi altri parametri, tutte le informazioni restituite dal cmdlet **the Out-Printer** verranno stampate sulla stampante predefinita.

Analogamente, nessun cmdlet di Skype for Business online include un parametro che consenta di salvare i dati in un file. Il comando seguente usa il cmdlet **Out-File** per salvare le informazioni restituite nel file di testo C:\\Logs\\Tenants.txt:

    Get-Tenant | Out-File -FilePath "C:\Logs\Tenants.txt"

Il comando seguente usa il cmdlet **Select-Object** per limitare i dati restituiti e visualizzati sullo schermo. In questo esempio, il cmdlet [Get-CsOnlineUser](get-csonlineuser.md) recupera informazioni relative a tutti gli utenti di Skype for Business online, quindi viene usato il cmdlet **Select-Object** per limitare i dati visualizzati al valore Identity e ai criteri di archiviazione dell'utente:

    Get-CsOnlineUser | Select-Object Identity, ArchivingPolicy

Poiché nel computer saranno disponibili centinaia di cmdlet, può essere difficile stabilire quali appartengano a Skype for Business online e quali no. Per restituire un elenco dei cmdlet di Skype for Business online (e solo dei cmdlet di Skype for Business online), prima di tutto è necessario determinare il nome del modulo temporaneo di Windows PowerShell che contiene tutti i cmdlet di Skype for Business online. A tale scopo, eseguire il comando seguente dal prompt di Windows PowerShell:

    Get-Module

Verranno visualizzate informazioni simili a quelle riportate di seguito:

    ModuleType Name                 ExportedCommands
    ---------- ----                 ----------------
    Manifest   Microsoft.PowerS...  {Add-Computer, Add-Content, A...}
    Script     tmp_5astd3uh.m5v     {Disable-CsMeetingRoom, Enabl...}

Il modulo con ModuleType Script è quello che contiene i cmdlet di Skype for Business online. Per ottenere un elenco di questi cmdlet, eseguire il cmdlet **Get-Command**, usando il nome del modulo Script come nome di modulo:

    Get-Command -Module tmp_5astd3uh.m5v

Potrebbero essere presenti più moduli con ModuleType uguale a Script. In tal caso, per scoprire quale modulo include il cmdlet **Get-CsTenant** si può usare il comando seguente:

    Get-Command Get-CsTenant

Il modulo restituito per il cmdlet **Get-CsTenant** sarà il modulo che contiene tutti i cmdlet di Skype for Business online:

    CommandType     Name                                               ModuleName
    -----------     ----                                               ----------
    Function        Get-CsTenant                                       tmp_5astd3uh.m5v

## Vedere anche

#### Concetti

[Introduzione a Windows PowerShell e Lync Online](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

