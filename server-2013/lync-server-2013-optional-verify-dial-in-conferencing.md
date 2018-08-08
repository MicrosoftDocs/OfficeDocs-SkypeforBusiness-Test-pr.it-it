---
title: "Lync Server 2013: (Facolt.) Verifica teleconferenze con accesso esterno"
TOCTitle: (Facoltativo) Verificare le conferenze telefoniche con accesso esterno
ms:assetid: 3e2b4220-8fb3-442f-98b1-78447adb321f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425905(v=OCS.15)
ms:contentKeyID: 49300297
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# (Facoltativo) Verificare le conferenze telefoniche con accesso esterno in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2011-01-21_

Per verificare che la pagina Web Impostazioni conferenza telefonica con accesso esterno e i numeri di accesso esterno funzionino correttamente, è necessario eseguire le operazioni seguenti:

  - Testare la pagina Web Impostazioni conferenza telefonica con accesso esterno eseguendo l'accesso all'URL semplice.

  - Verificare che i numeri di accesso funzionino correttamente per un pool specifico eseguendo lo script riportato più avanti in questo argomento. Questo script simula le chiamate ai numeri di accesso. Per utilizzare lo script, sono necessari l'indirizzo SIP e le credenziali di un client per comunicazioni unificate ospitato nel pool specifico.

Questo passaggio è facoltativo.

## Per testare i numeri di accesso per un pool specifico

1.  Accedere al computer come membro del gruppo RTCUniversalServerAdmins o come membro del ruolo **Cs-ServerAdministrator** o **CsAdministrator** .

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire il comando seguente al prompt:
    
        $credentials = Get-Credential
           User name:  testuser1@contoso.com
           Password:   ********
        Test-CsDialInConferencing -UserSipAddress sip:testuser1@contoso.com -UserCredential $credentials -TargetFqdn <serverName>.<domainName>.com -Verbose
    
    Nel rapporto risultante viene mostrato l'esito positivo o negativo, insieme a specifiche informazioni di diagnostica. Il flag –Verbose consente di ottenere informazioni più dettagliate su quanti numeri di accesso sono stati trovati con le relative informazioni.

