---
title: Cmdlet che usano il parametro Tenant
TOCTitle: Cmdlet che usano il parametro Tenant
ms:assetid: e7fe7c12-fbe0-49c1-9e8c-eef6958f27d0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362850(v=OCS.15)
ms:contentKeyID: 56269992
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlet che usano il parametro Tenant

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Quando si modificano le impostazioni del provider pubblico, è sempre necessario fornire un'identità Tenant anche se si usa un singolo tenant. Questo comando consente ad esempio di impostare Windows Live come unico provider pubblico con cui gli utenti possono comunicare:

    Set-CsTenantPublicProvider -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" -Provider "WindowsLive"

Per fortuna, non è necessario digitare l'ID del tenant (ad esempio, bf19b7db-6960-41e5-a139-2aa373474354) ogni volta che si esegue uno di questi cmdlet. È infatti possibile recuperare l'ID eseguendo il cmdlet [Get-CsTenant](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsTenant), archiviare l'ID in una variabile e quindi usare tale variabile quando si chiama uno degli altri cmdlet. Ad esempio:

    $x = (Get-CsTenant).TenantId
    Set-CsTenantPublicProvider -Tenant $x -Provider "WindowsLive"

In alternativa, è possibile eseguire questa operazione in un comando singolo recuperando l'ID del tenant e quindi inoltrare tale valore mediante pipe al cmdlet Set-CsTenantPublicProvider:

    Get-CsTenant | Select-Object TenantId | ForEach-Object {Set-CsTenantPublicProvider -Tenant $_.TenantId -Provider "WindowsLive"}

Non è necessario specificare l'ID del tenant quando si chiama il cmdlet **Get-CsTenant**. Questo comando restituisce informazioni sul tenant:

    Get-CsTenant

I cmdlet seguenti accettano un'identità del tenant ma in questi casi il parametro è facoltativo e non deve necessariamente essere immesso quando si chiama il cmdlet. Windows PowerShell immetterà infatti automaticamente l'identità del tenant in base al tenant di Skype for Business online a cui si è attualmente connessi:

  - [Get-CsTenant](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsTenant)

  - [Set-CsTenantFederationConfiguration](https://docs.microsoft.com/powershell/module/skype/Set-CsTenantFederationConfiguration)

  - [Set-CsTenantHybridConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsTenantHybridConfiguration)

  - [Get-CsTenantFederationConfiguration](https://docs.microsoft.com/powershell/module/skype/Get-CsTenantFederationConfiguration)

  - [Get-CsTenantHybridConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsTenantHybridConfiguration)

  - [Get-CsTenantLicensingConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsTenantLicensingConfiguration)

Il cmdlet **Get-CsTenantFederationConfiguration** può ad esempio essere chiamato mediante questo comando:

    Get-CsTenantFederationConfiguration

Anche se non è necessario, è possibile includere il parametro Tenant quando si chiama Get-CsTenantFederationConfiguration:

    Get-CsTenantFederationConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354"

## Vedere anche

#### Concetti

[Identità, ambiti e tenant](identities-scopes-and-tenants-in-skype-for-business-online.md)  
[Cmdlet di Lync Online](the-skype-for-business-online-cmdlets.md)

