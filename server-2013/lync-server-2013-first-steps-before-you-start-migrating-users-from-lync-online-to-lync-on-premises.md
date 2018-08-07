---
title: Passaggi preliminari per la migrazione di utenti da Lync Online a Lync in locale
TOCTitle: Passaggi preliminari per la migrazione di utenti da Lync Online a Lync in locale
ms:assetid: 98245b04-ded4-4186-8da3-ba1c554b5c39
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn689118(v=OCS.15)
ms:contentKeyID: 62247333
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Passaggi preliminari per la migrazione di utenti da Lync Online a Lync in locale

 

_**Ultima modifica dell'argomento:** 2014-05-08_

Prima di iniziare a spostare gli utenti di Lync Online nell'ambiente locale, verificare che le seguenti condizioni siano vere:

  - È necessario che l'ambiente locale di Lync Server sia completamente distribuito e convalidato. Per ulteriori informazioni, vedere [Distribuzione di Lync Server 2013](lync-server-2013-deploying-lync-server.md).

  - È necessario che il tenant di Lync Online sia configurato per l'accesso remoto PowerShell.
    
    A tale scopo, installare il modulo di Skype for Business online per Windows PowerShell, disponibile qui: [http://go.microsoft.com/fwlink/p/?LinkId=391911](http://go.microsoft.com/fwlink/p/?linkid=391911).
    
    Dopo aver installato il modulo, sarà possibile stabilire una sessione remota digitando i seguenti cmdlet in Lync Server Management Shell:
    
    ```
    Import-Module LyncOnlineConnector
    ```
    ```
    $cred = Get-Credential
    ```
    ```
    $CSSession = New-CsOnlineSession -Credential $cred
    ```
    ```
    Import-PSSession $CSSession -AllowClobber
    ```
    
  Per ulteriori informazioni su come stabilire una sessione remota di PowerShell con Skype for Business online, vedere [Connessione a Lync Online tramite Windows PowerShell](https://docs.microsoft.com/en-us/SkypeForBusiness/set-up-your-computer-for-windows-powershell/set-up-your-computer-for-windows-powershell).
  
  Per ulteriori informazioni su come usare il modulo PowerShell di Skype for Business online, vedere [Uso di Windows PowerShell per gestire Lync Online](https://docs.microsoft.com/en-us/SkypeForBusiness/set-up-your-computer-for-windows-powershell/set-up-your-computer-for-windows-powershell).

  - È necessario configurare Lync Online per lo spazio indirizzi SIP condiviso. A tale scopo, avviare una sessione remota di PowerShell con Lync Online. Quindi eseguire il seguente cmdlet:
    
        Set-CsTenantFederationConfiguration -SharedSipAddressSpace $True

Dopo aver completato questi passaggi, è possibile passare all'argomento [Eseguire la migrazione degli utenti di Lync Online a Lync in locale](lync-server-2013-migrating-lync-online-users-to-lync-on-premises.md).

