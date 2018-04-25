---
title: Cmdlet che usano l'identità di un provider di servizi di conferenza
TOCTitle: Cmdlet che usano l'identità di un provider di servizi di conferenza
ms:assetid: be5621b6-ec11-4b12-83ec-075af269ca6a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362841(v=OCS.15)
ms:contentKeyID: 56269970
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlet che usano l'identità di un provider di servizi di conferenza

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Per ottenere informazioni sui provider di servizi di audioconferenza con cui l'organizzazione ha stipulato un contratto, è possibile chiamare semplicemente il cmdlet [Get-CsAudioConferencingProvider](get-csaudioconferencingprovider.md) senza parametri:

    Get-CsAudioConferencingProvider

Se si desidera limitare i dati restituiti a un solo provider (in questo esempio, il provider Contoso Audio Services), usare il parametro Identity:

    Get-CsAudioConferencingProvider -Identity "Contoso Audio Services"

Esiste un solo cmdlet di Skype for Business online che accetta l'ID di un provider di servizi di audioconferenza:

  - [Get-CsAudioConferencingProvider](get-csaudioconferencingprovider.md)

## Vedere anche

#### Concetti

[Identità, ambiti e tenant](identities-scopes-and-tenants-in-skype-for-business-online.md)  
[Cmdlet di Lync Online](the-skype-for-business-online-cmdlets.md)

