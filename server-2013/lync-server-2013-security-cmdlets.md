---
title: Cmdlet per la sicurezza
TOCTitle: Cmdlet per la sicurezza
ms:assetid: 9a6c654d-287d-434e-8d93-409f0d623f5a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398799(v=OCS.15)
ms:contentKeyID: 49301430
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlet per la sicurezza

 

_**Ultima modifica dell'argomento:** 2012-10-09_

I cmdlet relativi alla sicurezza inclusi in Microsoft Lync Server 2013 vengono utilizzati principalmente per gestire l'autenticazione, nonché le autorizzazioni e i diritti utente. È disponibile un'ampia gamma di cmdlet per la gestione dell'autenticazione, inclusi i cmdlet per l'autenticazione tramite certificato e PIN. Diversi cmdlet inoltre consentono di utilizzare la nuova funzionalità di controllo dell'accesso basato sui ruoli per delegare il controllo amministrativo di Lync Server.

## Cmdlet per la sicurezza

Molte attività di gestione relative alle impostazioni di sicurezza possono essere eseguite dal Pannello di controllo di Lync Server. I cmdlet per le autorizzazioni utente rappresentano un'eccezione. È tuttavia possibile eseguire tutte le attività di gestione della sicurezza con i cmdlet da Lync Server Management Shell o da uno script. L'utilizzo di uno script consente di automatizzare particolari attività. Di seguito è riportato un elenco di cmdlet direttamente correlati alla gestione delle impostazioni di sicurezza:

**[Cmdlet per i certificati e l'autenticazione](lync-server-2013-certificate-and-authentication-cmdlets.md)**

  -   
    [Get-CsCertificate](get-cscertificate.md)

  -   
    [Import-CsCertificate](import-cscertificate.md)

  -   
    [Remove-CsCertificate](remove-cscertificate.md)

  -   
    [Request-CsCertificate](request-cscertificate.md)

  -   
    [Set-CsCertificate](set-cscertificate.md)

  -   
    [Test-CsCertificateConfiguration](test-cscertificateconfiguration.md)

  -   
    [Get-CsClientCertificate](get-csclientcertificate.md)

  -   
    [Revoke-CsClientCertificate](revoke-csclientcertificate.md)

  -   
    [Lock-CsClientPin](lock-csclientpin.md)

  -   
    [Set-CsClientPin](set-csclientpin.md)

  -   
    [Unlock-CsClientPin](unlock-csclientpin.md)

  -   
    [Get-CsClientPinInfo](get-csclientpininfo.md)

  -   
    [New-CsKerberosAccount](new-cskerberosaccount.md)

  -   
    [Get-CsKerberosAccountAssignment](get-cskerberosaccountassignment.md)

  -   
    [New-CsKerberosAccountAssignment](new-cskerberosaccountassignment.md)

  -   
    [Remove-CsKerberosAccountAssignment](remove-cskerberosaccountassignment.md)

  -   
    [Set-CsKerberosAccountAssignment](set-cskerberosaccountassignment.md)

  -   
    [Test-CsKerberosAccountAssignment](test-cskerberosaccountassignment.md)

  -   
    [Set-CsKerberosAccountPassword](set-cskerberosaccountpassword.md)

  -   
    [Get-CsPinPolicy](get-cspinpolicy.md)

  -   
    [Grant-CsPinPolicy](grant-cspinpolicy.md)

  -   
    [New-CsPinPolicy](new-cspinpolicy.md)

  -   
    [Remove-CsPinPolicy](remove-cspinpolicy.md)

  -   
    [Set-CsPinPolicy](set-cspinpolicy.md)

  -   
    [Get-CsProxyConfiguration](get-csproxyconfiguration.md)

  -   
    [New-CsProxyConfiguration](new-csproxyconfiguration.md)

  -   
    [Remove-CsProxyConfiguration](remove-csproxyconfiguration.md)

  -   
    [Set-CsProxyConfiguration](set-csproxyconfiguration.md)

  -   
    [Get-CsSipDomain](get-cssipdomain.md)

  -   
    [New-CsSipDomain](new-cssipdomain.md)

  -   
    [Remove-CsSipDomain](remove-cssipdomain.md)

  -   
    [Set-CsSipDomain](set-cssipdomain.md)

**[Cmdlet per le autorizzazioni e i diritti utente](lync-server-2013-user-rights-and-permissions-cmdlets.md)**

  -   
    [Get-CsAdminRole](get-csadminrole.md)

  -   
    [New-CsAdminRole](new-csadminrole.md)

  -   
    [Remove-CsAdminRole](remove-csadminrole.md)

  -   
    [Set-CsAdminRole](set-csadminrole.md)

  -   
    [Update-CsAdminRole](update-csadminrole.md)

  -   
    [Get-CsAdminRoleAssignment](get-csadminroleassignment.md)

  -   
    [Grant-CsOUPermission](grant-csoupermission.md)

  -   
    [Revoke-CsOUPermission](revoke-csoupermission.md)

  -   
    [Test-CsOUPermission](test-csoupermission.md)

  -   
    [Grant-CsSetupPermission](grant-cssetuppermission.md)

  -   
    [Revoke-CsSetupPermission](revoke-cssetuppermission.md)

  -   
    [Test-CsSetupPermission](test-cssetuppermission.md)

**[Cmdlet di interoperabilità](lync-server-2013-interoperability-cmdlets.md)**

  - [Get-CsOAuthConfiguration](get-csoauthconfiguration.md)

  - [Set-CsOAuthConfiguration](set-csoauthconfiguration.md)

  - [Get-CsOAuthServer](get-csoauthserver.md)

  - [New-CsOAuthServer](new-csoauthserver.md)

  - [Remove-CsOAuthServer](remove-csoauthserver.md)

  - [Set-CsOAuthServer](set-csoauthserver.md)

  - [Get-CsPartnerApplication](get-cspartnerapplication.md)

  - [New-CsPartnerApplication](new-cspartnerapplication.md)

  - [Remove-CsPartnerApplication](remove-cspartnerapplication.md)

  - [Set-CsPartnerApplication](set-cspartnerapplication.md)

## Vedere anche

#### Ulteriori risorse

[Blog di Lync Server PowerShell](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x410)

