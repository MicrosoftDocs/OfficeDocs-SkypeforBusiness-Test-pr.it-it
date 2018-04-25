---
title: Connessione automatica a Lync Online a ogni avvio di Windows PowerShell
TOCTitle: Connessione automatica a Lync Online a ogni avvio di Windows PowerShell
ms:assetid: 68f76c36-5dd6-48ea-b19a-d65593199e4c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362799(v=OCS.15)
ms:contentKeyID: 56269917
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Connessione automatica a Lync Online a ogni avvio di Windows PowerShell

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Se non si ricordano tutti i comandi necessari per connettersi a Skype for Business online, è possibile creare una configurazione che consenta di fare semplicemente doppio clic su un collegamento, immettere la propria password di Skype for Business online e ottenere così l'accesso a Skype for Business online.

A questo scopo, aprire Blocco note o qualsiasi altro editor di testo, quindi incollare i comandi seguenti, sostituendo il proprio nome account Skype for Business online a kenmyer@litwareinc.com:

    $credential = Get-Credential "kenmyer@litwareinc.com"
    $session = New-CsOnlineSession -Credential $credential 
    Import-PSSession $session

Salvare il file con estensione di file PS1(ad esempio, C:\\Scripts\\LyncOnline.ps1).

Dopo aver salvato il file, completare la procedura seguente per creare sul desktop un collegamento che avvia Windows PowerShell ed esegue lo script all'avvio:

1.  Fare clic con il pulsante destro del mouse sul desktop, scegliere **Nuovo**, quindi **Collegamento**.

2.  Nella procedura guidata **Crea collegamento** digitare quanto segue nella casella **Immettere il percorso per il collegamento** e fare clic su **Avanti** (usare il percorso del file di script appena creato):
    
        powershell.exe -noexit C:\Scripts\LyncOnline.ps1

3.  Nella casella **Immettere il nome del collegamento** digitare un nome per il collegamento, ad esempio **Skype for Business online**, quindi fare clic su **Fine**.

4.  La prossima volta che si vuole usare Windows PowerShell per la gestione di Skype for Business online, sarà sufficiente fare doppio clic sul collegamento e immettere la propria password. Lo script si occuperà di stabilire la connessione e di impostare la nuova sessione remota.

La nuova sessione non viene in genere archiviata nella variabile $session. Al contrario, generalmente le viene assegnato l'ID sessione 1. Ciò non influisce in alcun modo sulla sessione, almeno non fino al momento in cui la sessione deve essere chiusa. Per chiuderla sarà infatti necessario fare riferimento all'ID sessione quando si chiama il cmdlet **Remove-PSSession**:

    Remove-PSSession 1

È possibile verificare l'ID assegnato alla sessione di Skype for Business online eseguendo questo comando dal prompt di Windows PowerShell:

    Get-PSSession

## Vedere anche

#### Concetti

[Configurazione del computer per la gestione di Lync Online](configuring-your-computer-for-skype-for-business-online-management.md)

