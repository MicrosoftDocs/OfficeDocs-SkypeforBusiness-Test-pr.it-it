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

  - [Enable-CsMeetingRoom](enable-csmeetingroom.md)

  - [Get-CsExUmContact](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsExUmContact)

  - [Get-CsMeetingRoom](get-csmeetingroom.md)

  - [Get-CsOnlineUser](get-csonlineuser.md)

  - [Get-CsUserAcp](get-csuseracp.md)

  - [New-CsExUmContact](new-csexumcontact.md)

  - [Remove-CsExUmContact](remove-csexumcontact.md)

  - [Remove-CsUserAcp](remove-csuseracp.md)

  - [Set-CsExUmContact](set-csexumcontact.md)

  - [Set-CsMeetingRoom](set-csmeetingroom.md)

  - [Set-CsUserAcp](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsUserAcp)

Tenere presente che non è necessario specificare un'identità utente quando si chiama uno dei cmdlet **Get-Cs**. In questo caso, i cmdlet restituiscono tutte le istanze dell'elemento specificato. Ad esempio, il comando seguente restituisce informazioni su tutti gli utenti che sono stati abilitati per Skype for Business online:

    Get-CsOnlineUser

Il parametro Identity è obbligatorio solo quando si vogliono recuperare le informazioni relative a un utente specifico:

    Get-CsOnlineUser -Identity "Ken Myer"

## Vedere anche

#### Concetti

[Identità, ambiti e tenant](identities-scopes-and-tenants-in-skype-for-business-online.md)  
[Cmdlet di Lync Online](the-skype-for-business-online-cmdlets.md)

