---
title: Cmdlet che non usano un ambito o un'identità
TOCTitle: Cmdlet che non usano un ambito o un'identità
ms:assetid: 9c50c732-3c64-4b6a-96fd-8f528eb739ce
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362824(v=OCS.15)
ms:contentKeyID: 56269964
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlet che non usano un ambito o un'identità

 

_**Ultima modifica dell'argomento:** 2015-06-22_

I cmdlet usati per modificare gli elenchi di domini autorizzati e bloccati (elenchi che determinano con quali organizzazioni esterne possono comunicare gli utenti) non usano né un ambito né un'identità. Il cmdlet **New-CsEdgeAllowAllKnownDomains** non ha di fatto parametri di alcun tipo. I cmdlet che non usano né un ambito né un'identità sono:

  - [New-CsEdgeAllowAllKnownDomains](https://docs.microsoft.com/powershell/module/skype/New-CsEdgeAllowAllKnownDomains)

  - [New-CsEdgeAllowList](https://docs.microsoft.com/powershell/module/skype/New-CsEdgeAllowList)

  - [New-CsEdgeDomainPattern](https://docs.microsoft.com/powershell/module/skype/New-CsEdgeDomainPattern)

Tenere presente che sia con il cmdlet **New-CsEdgeAllowList** che con il cmdlet **New-CsEdgeDomainPattern** è necessario includere il parametro Domain. Ad esempio:

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"

## Vedere anche

#### Concetti

[Identità, ambiti e tenant](identities-scopes-and-tenants-in-skype-for-business-online.md)  
[Cmdlet di Lync Online](the-skype-for-business-online-cmdlets.md)

