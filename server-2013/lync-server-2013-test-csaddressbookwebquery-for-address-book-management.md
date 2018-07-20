---
title: Test-CsAddressBookWebQuery per la gestione della rubrica
TOCTitle: Test-CsAddressBookWebQuery per la gestione della rubrica
ms:assetid: 977a9c1f-5f4e-4539-9a26-8748b61a57d8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg429716(v=OCS.15)
ms:contentKeyID: 49301418
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsAddressBookWebQuery per la gestione della rubrica

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Utenti autorizzati a eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire localmente il cmdlet Test-CsAddressBookWebQuery: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt di Windows PowerShell eseguire il comando seguente:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Test-CsAddressBookService"}

Analogamente alla transazione sintetica Test-CsAddressBookService, Test-CsAddressBookWebQuery invia una query al servizio Address Book Web Query per verificare che stia funzionando in modo corretto. Il cmdlet si connette al servizio di autenticazione Web Ticket e presenta le credenziali specificate in –UserCredential. Se l'autenticazione ha esito positivo, il cmdlet presenta quindi le informazioni –TargetSipAddress. Il cmdlet comunica l'esito positivo se è stato in grado di recuperare le informazioni sul contatto.

Ad esempio:

    Test-CsAddressBookWebQuery -TargetFqdn atl-cs-001.contoso.com -UserCredential contoso\bob -UserSipAddress "sip:bob@contoso.com" -TargetSipAddress "sip:bob@contoso.com"

Per una descrizione dettagliata del comando completo, fare riferimento all'argomento seguente nella documentazione di riferimento principale per i cmdlet RTC di Windows PowerShell per Lync Server.

## Vedere anche

#### Ulteriori risorse

[Test-CsAddressBookWebQuery](https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsAddressBookWebQuery)

