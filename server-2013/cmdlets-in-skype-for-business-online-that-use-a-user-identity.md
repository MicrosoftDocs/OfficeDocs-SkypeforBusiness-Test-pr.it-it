---
title: Cmdlet che usano l'identità di un utente
TOCTitle: Cmdlet che usano l'identità di un utente
ms:assetid: be87409f-6372-4c70-91ac-6ef13dfbe65a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362842(v=OCS.15)
ms:contentKeyID: 56269978
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlet che usano l'identità di un utente

 

_**Ultima modifica dell'argomento:** 2015-06-22_

In Skype for Business online è possibile fare riferimento a un'identità utente in diversi modi:

  - Usare il nome visualizzato di Servizi di dominio Active Directory dell'utente. Ad esempio:
    
        -Identity "Ken Myer"

  - Usare l'indirizzo SIP dell'utente. Ad esempio:
    
        -Identity "sip:kenmyer@litwareinc.com"

  - Usare l'UPN dell'utente. Ad esempio:
    
        -Identity " kenmyer@litwareinc.com"

  - Usare il nome distinto di Servizi di dominio Active Directory dell'utente. Ad esempio:
    
        -Identity "CN=48ebd1ba-95d4-460c-b751-811ebf0c4611,OU=fa8226f5-14fa-46da-8 236-039b25bc7a27,OU=Lync Online Tenants,DC=litwareinc,DC=com"

I cmdlet seguenti accettano un'identità utente:

  - [Disable-CsMeetingRoom](https://docs.microsoft.com/en-us/powershell/module/skype/Disable-CsMeetingRoom)

  - [Enable-CsMeetingRoom](https://docs.microsoft.com/en-us/powershell/module/skype/Enable-CsMeetingRoom)

  - [Get-CsExUmContact](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsExUmContact)

  - [Get-CsMeetingRoom](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsMeetingRoom)

  - [Get-CsOnlineUser](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsOnlineUser?view=skype-ps)

  - [Get-CsUserAcp](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsUserAcp)

  - [New-CsExUmContact](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsExUmContact)

  - [Remove-CsExUmContact](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsExUmContact)

  - [Remove-CsUserAcp](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsUserAcp)

  - [Set-CsExUmContact](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsExUmContact)

  - [Set-CsMeetingRoom](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsMeetingRoom)

  - [Set-CsUserAcp](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsUserAcp)

Tenere presente che non è necessario specificare un'identità utente quando si chiama uno dei cmdlet **Get-Cs**. In questo caso, i cmdlet restituiscono tutte le istanze dell'elemento specificato. Ad esempio, il comando seguente restituisce informazioni su tutti gli utenti che sono stati abilitati per Skype for Business online:

    Get-CsOnlineUser

Il parametro Identity è obbligatorio solo quando si vogliono recuperare le informazioni relative a un utente specifico:

    Get-CsOnlineUser -Identity "Ken Myer"

## Vedere anche

#### Concetti

[Identità, ambiti e tenant](identities-scopes-and-tenants-in-skype-for-business-online.md)  
[Cmdlet di Lync Online](https://docs.microsoft.com/en-us/SkypeForBusiness/set-up-your-computer-for-windows-powershell/set-up-your-computer-for-windows-powershell)

