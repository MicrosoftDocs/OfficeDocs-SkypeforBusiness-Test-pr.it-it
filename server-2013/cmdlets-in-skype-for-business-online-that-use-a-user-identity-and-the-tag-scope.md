---
title: Cmdlet che usano un'identità utente e l'ambito tag
TOCTitle: Cmdlet che usano un'identità utente e l'ambito tag
ms:assetid: 344a21b0-5301-4e77-853a-970bb1c11e1d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362781(v=OCS.15)
ms:contentKeyID: 56269895
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlet che usano un'identità utente e l'ambito tag

 

_**Ultima modifica dell'argomento:** 2015-06-22_

I cmdlet **Grant-Cs**, usati per l'assegnazione di criteri agli utenti, richiedono due identificatori: un'identità utente (parametro Identity) e l'identità di un criterio per utente (parametro PolicyName). Per assegnare ad esempio il criterio vocale, RedmondVoicePolicy, all'utente Ken Myer, usare il comando seguente:

    Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName "RedmondVoicePolicy"

È necessario tenere presenti due aspetti quando si assegnano criteri agli utenti. Prima di tutto, possono essere assegnati solo criteri per utente, non è infatti possibile assegnare criteri globali a un utente. Questo comando avrà ad esempio esito negativo:

    Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName "global"

Il comando non riesce perché non è necessario assegnare il criterio globale. Per gestire un utente usando il criterio globale, evitare di assegnare a tale utente un criterio per utente. Se non si assegna un criterio per utente, l'utente verrà gestito automaticamente tramite il criterio globale.


> [!NOTE]
> Se è già stato assegnato in criterio per utente in precedenza e si desidera rimuovere tale assegnazione per gestire l'utente mediante criteri globali, usare prima di tutto la seguente sintassi che rimuove l'assegnazione di un criterio per utente concedendo a tale utente un criterio Null:<BR>Grant-CsVoicePolicy –Identity "Ken Myer" –PolicyName $Null



Tenere quindi presente che i criteri per utente vengono creati nell'ambito tag. Non è tuttavia possibile omettere il **prefisso** tag quando si specifica un nome di criterio. Questi due comandi sono identici:

    Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName "tag:RedmondVoicePolicy"
    Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName "RedmondVoicePolicy"

Per ottenere le identità di tutti i criteri per utente, o almeno tutti i criteri per utente di un tipo specificato, ad esempio i criteri vocali, usare un comando simile al seguente:

    Get-CsVoicePolicy -Filter "tag:*"

I cmdlet seguenti usano sia l'identità utente che l'ambito tag:

  - [Grant-CsClientPolicy](grant-csclientpolicy.md)

  - [Grant-CsConferencingPolicy](grant-csconferencingpolicy.md)

  - [Grant-CsDialPlan](grant-csdialplan.md)

  - [Grant-CsExternalAccessPolicy](grant-csexternalaccesspolicy.md)

  - [Grant-CsHostedVoicemailPolicy](grant-cshostedvoicemailpolicy.md)

  - [Grant-CsVoicePolicy](grant-csvoicepolicy.md)

## Vedere anche

#### Concetti

[Identità, ambiti e tenant](identities-scopes-and-tenants-in-skype-for-business-online.md)  
[Cmdlet di Lync Online](the-skype-for-business-online-cmdlets.md)

