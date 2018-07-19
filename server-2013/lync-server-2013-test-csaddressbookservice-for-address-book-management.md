---
title: Test-CsAddressBookService per la gestione della rubrica
TOCTitle: Test-CsAddressBookService per la gestione della rubrica
ms:assetid: b88cea74-41fd-4c0e-9284-7135bff27a27
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg429720(v=OCS.15)
ms:contentKeyID: 49301773
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsAddressBookService per la gestione della rubrica

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Utenti autorizzati a eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire localmente il cmdlet Test-CsAddressBookService: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli del controllo di accesso basato sui ruoli creati personalmente), al prompt di Windows PowerShell eseguire il comando seguente:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Test-CsAddressBookService"}

In Lync Server 2013 sono disponibili diversi cmdlet che avviano comandi sintetici per verificare il corretto funzionamento di una specifica funzione o caratteristica. Il cmdlet Test-CsAddressBookService verifica che l'utente specificato possa connettersi e richiedere i file locali al servizio Web Rubrica.

Ad esempio:

    Test-CsAddressBookService -TargetFqdn atl-cs-001.contoso.com -UserCredential contoso\bob -UserSipAddress "sip:bob@contoso.com"

## Vedere anche

#### Ulteriori risorse

[Test-CsAddressBookService](https://docs.microsoft.com/en-us/powershell/module/skype/Test-CsAddressBookService)

