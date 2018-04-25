---
title: Abilitare o disabilitare un provider di servizi di messaggistica istantanea pubblici specifico
TOCTitle: Abilitare o disabilitare un provider di servizi di messaggistica istantanea pubblici specifico
ms:assetid: 9d3e2607-01c0-4ae9-accc-39f03ce253bb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362825(v=OCS.15)
ms:contentKeyID: 56269961
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare o disabilitare un provider di servizi di messaggistica istantanea pubblici specifico

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Skype for Business online consente di stabilire una federazione con gli utenti di uno o più dei provider di servizi di messaggistica istantanea pubblici seguenti:

  - Rete Windows Live di servizi Internet

  - Yahoo\!

  - AOL

Per consentire la federazione con uno o più di questi provider, usare il cmdlet [Set-CsTenantPublicProvider](set-cstenantpublicprovider.md) e impostare la proprietà Provider su uno o più dei valori seguenti:

  - Windows Live

  - Yahoo\!

  - AOL

Ad esempio, il comando seguente stabilisce la federazione con Windows Live e AOL:

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "AOL","WindowsLive"

Ogni volta che si vuole aggiungere o rimuovere un provider, è necessario includere tutti i provider federati pertinenti nel comando. Ad esempio, per aggiungere Yahoo\! occorre aggiungere il comando seguente:

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "Yahoo"

Con l'esecuzione di questo comando Yahoo\! rimane l'unico provider federato, poiché è il provider chiamato nel comando. Per stabilire la federazione con tutti e tre i provider di servizi di messaggistica istantanea pubblici, è necessario includerli tutti e tre:

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "Yahoo", "AOL","WindowsLive"

Tenere presente che quando si chiama il cmdlet Set-CsTenantPublicProvider è necessario includere il parametro Tenant. Se non lo si include, viene chiesto di inserire l'ID tenant. Per recuperare l'ID del tenant di Skype for Business online è possibile usare il comando seguente:

    Get-CsTenant | Select-Object TenantID

In alternativa, è possibile usare il comando seguente per memorizzare l'ID tenant in una variabile:

    $tenantID = (Get-CsTenant | Select-Object TenantID)

Questa variabile ($tenantID in questo esempio) può quindi essere usata per chiamare Set-CsTenantPublicProvider:

    Set-CsTenantPublicProvider -Tenant $tenantID -Provider "Yahoo", "AOL","WindowsLive"

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

