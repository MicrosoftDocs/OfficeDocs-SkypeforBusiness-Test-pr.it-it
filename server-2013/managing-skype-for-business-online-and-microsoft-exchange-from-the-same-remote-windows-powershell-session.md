---
title: Gestione di Lync Online e Microsoft Exchange dalla stessa sessione remota di Windows PowerShell
TOCTitle: Gestione di Lync Online e Microsoft Exchange dalla stessa sessione remota di Windows PowerShell
ms:assetid: 4eb4b5f0-f407-46bd-a2ac-a7ccbc387d51
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362787(v=OCS.15)
ms:contentKeyID: 56269902
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestione di Lync Online e Microsoft Exchange dalla stessa sessione remota di Windows PowerShell

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Quando si esegue la sottoscrizione a Office 365, si ottiene l'accesso non solo a Skype for Business online, ma anche a Exchange Online. È possibile usare una sessione remota di Windows PowerShell per gestire Skype for Business online. È possibile usare una sessione remota di Windows PowerShell anche per gestire Exchange. Skype for Business online e Exchange Online, tuttavia, non condividono lo stesso URI, né usano lo stesso metodo di connessione. Ciò significa che è necessario usare sessioni separate per gestire Skype for Business online e Exchange. Esiste comunque un modo per gestire entrambi i prodotti mediante un'unica sessione remota di Windows PowerShell.

Non solo è possibile gestire entrambi i prodotti dalla stessa istanza di Windows PowerShell, ma configurare questa sessione di gestione doppia è estremamente facile. Prima di tutto, avviare Windows PowerShell e connettersi a Skype for Business online come di consueto: creare un oggetto credenziali, quindi creare una nuova sessione di connessione a Skype for Business online:

    $credential = Get-Credential "kenmyer@litwareinc.com"
    $lyncSession = New-CsOnlineSession -Credential $credential

Usare quindi un processo analogo per connettersi a Exchange Online. Tenere presente che non è necessario creare un nuovo oggetto credenziali, ma è possibile continuare a usare lo stesso oggetto ($credential) utilizzato per l'accesso a Skype for Business online:

    $exchangeSession = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri "https://outlook.office365.com/powershell-liveid/" -Credential $credential -Authentication "Basic" -AllowRedirection

Usare sempre l'URI https://outlook.office365.com/powershell-liveid/ quando ci si connette a Exchange Online, indipendentemente dall'URI di Office 365. Dopo l'autenticazione, si verrà reindirizzati automaticamente all'URI appropriato. Per questo motivo è molto importante includere il parametro AllowRedirection. Se questo parametro viene omesso, l'autenticazione verrà eseguita, ma il reindirizzamento avrà esito negativo e non sarà possibile connettersi a Exchange Online:

    New-PSSession : [ps.outlook.com] The WinRM service cannot process the request because the request needs to be sent to a different machine. Use the redirect information to send the request to a new machine.  Redirect location reported: https://pod51043psh.outlook.com/powershell-liveid?PSVersion=3.0 . To automatically connect to the redirected URI, verify  MaximumConnectionRedirectionCount" property of session preference variable "PSSessionOption" and use "AllowRedirection" parameter on the cmdlet.

A questo punto nel computer dovrebbero essere in esecuzione due sessioni remote separate. Per verificare questa condizione, digitare il comando seguente al prompt di Windows PowerShell:

    Get-PSSession

Le informazioni visualizzate dovrebbero essere analoghe alle seguenti:

    Id Name      ComputerName  State   ConfigurationName     Availability
    -- ----      ------------  -----   -----------------     ------------
     1 Session1  pod510w43...  Opened  Microsoft.PowerShell     Available
     2 Session2  up02921vd...  Opened  Microsoft.Exchange       Available

A questo punto sono presenti un paio di sessioni remote che possono essere importate nella sessione locale di Windows PowerShell. A questo scopo, eseguire questi due comandi:

    Import-PSSession $lyncSession
    Import-PSSession $exchangeSession

I cmdlet Skype for Business online e Exchange Online sono ora disponibili per l'uso. Per verificare questa condizione, eseguire il comando seguente e assicurarsi di ricevere le informazioni utente:

    Get-CsOnlineUser -ResultSize 1

Eseguire quindi il seguente comando di Exchange e verificare di ricevere le informazioni sulla cassetta postale:

    Get-Mailbox -ResultSize 1

Per chiudere la sessione di gestione, assicurarsi di chiudere entrambe le sessioni remote:

    Remove-PSSession $lyncSession
    Remove-PSSession $exchangeSession

## Vedere anche

#### Concetti

[Configurazione del computer per la gestione di Lync Online](configuring-your-computer-for-skype-for-business-online-management.md)

