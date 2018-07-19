---
title: Cmdlet che usano l'ambito globale e l'ambito tag
TOCTitle: Cmdlet che usano l'ambito globale e l'ambito tag
ms:assetid: 1e2bc055-8a72-425e-967b-e253add7018c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362774(v=OCS.15)
ms:contentKeyID: 56269887
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlet che usano l'ambito globale e l'ambito tag

 

_**Ultima modifica dell'argomento:** 2015-06-22_

In Skype for Business online i criteri possono essere configurati nell'*ambito globale* o nell'*ambito tag* (o *ambito per utente*). Quando si usano i cmdlet **Get-Cs**, non è necessario specificare un ambito o un'identità. Se si chiama uno di questi cmdlet senza parametri, verranno restituiti tutti gli elementi rilevanti. Questo comando restituisce ad esempio informazioni su tutti i criteri di accesso esterno:

    Get-CsExternalAccessPolicy

È necessario includere solo il parametro Identity o Filter se si vogliono limitare i dati restituiti. Per restituire ad esempio solo i criteri globali, usare il comando:

    Get-CsExternalAccessPolicy -Identity "global"

Per restituire i criteri per utente con il parametro Identity “RedmondAccessPolicy”, usare questo comando:

    Get-CsExternalAccessPolicy -Identity "RedmondAccessPolicy"


> [!NOTE]
> Quando si fa riferimento a criteri per utente, il <STRONG>prefisso</STRONG> tag è facoltativo. È valida anche questa sintassi che include il prefisso:<BR>Get-CsExternalAccessPolicy –Identity "tag:RedmondAccessPolicy"



Per restituire tutti i criteri, eccetto quelli globali, ovvero tutti i criteri per utente, usare questo comando:

    Get-CsExternalAccessPolicy -Filter "tag:*"

I cmdlet seguenti funzionano sia nell'ambito globale che in quello per utente (tag):

  - [Get-CsClientPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsClientPolicy)

  - [Get-CsConferencingPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsConferencingPolicy)

  - [Get-CsDialPlan](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsDialPlan)

  - [Get-CsExternalAccessPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsExternalAccessPolicy)

  - [Get-CsHostedVoicemailPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsHostedVoicemailPolicy)

  - [Get-CsPresencePolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsPresencePolicy)

  - [Get-CsVoicePolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsVoicePolicy)


> [!NOTE]
> Nonostante il nome, dal punto di vista funzionale i dial plan sono criteri. Il termine <EM>dial plan</EM> viene usato ad esempio al posto di criteri di composizione per mantenere la terminologia usata nelle versioni precedenti di Lync Server.



## Vedere anche

#### Concetti

[Identità, ambiti e tenant](identities-scopes-and-tenants-in-skype-for-business-online.md)  
[Cmdlet di Lync Online](https://docs.microsoft.com/en-us/SkypeForBusiness/set-up-your-computer-for-windows-powershell/set-up-your-computer-for-windows-powershell)

