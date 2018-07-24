---
title: "Lync Server 2013: Rimuovere l'autenticazione Kerberos da un sito"
TOCTitle: Rimuovere l'autenticazione Kerberos da un sito
ms:assetid: 93171b02-bb36-42dc-943d-86d9dde45b59
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398749(v=OCS.15)
ms:contentKeyID: 49301342
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rimuovere l'autenticazione Kerberos da un sito in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-01-16_

Per eseguire correttamente questa procedura, è necessario essere connessi come utente membro del gruppo RTCUniversalServerAdmins.

Per rimuovere l'autenticazione Kerberos da un sito o ritirare un sito, è necessario rimuovere l'assegnazione dell'account di autenticazione Kerberos dal sito utilizzando il cmdlet **Remove-CsKerberosAccountAssignment**. Utilizzare la procedura seguente per rimuovere l'assegnazione dell'account di autenticazione Kerberos, rimuovendo così l'assegnazione da tutti i computer del sito.


> [!WARNING]
> Se si intende ritirare in modo permanente l'account abilitato per Kerberos, dopo aver rimosso l'assegnazione è necessario utilizzare Utenti e computer di Active Directory per eliminarlo da Servizi di dominio Active Directory. Se al contrario si prevede di utilizzare l'oggetto in futuro, è possibile conservare l'oggetto Active Directory.



## Rimuovere l'autenticazione Kerberos da un sito

1.  Come membro del gruppo RTCUniversalServerAdmins, accedere a un computer nel dominio che esegue Lync Server 2013 oppure a un computer in cui sono installati gli strumenti di amministrazione.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire i due comandi seguenti dalla riga di comando:
    
    ```
    Remove-CsKerberosAccountAssignment -Identity "site:SiteName"
    ```
    ```
    Enable-CsTopology
    ```

    Ad esempio:
    
    ```
    Remove-CsKerberosAccountAssignment -Identity "site:Redmond"
    ```
    ```
    Enable-CsTopology
    ```
    
    > [!important]  
    > Dopo aver apportato le necessarie modifiche all'autenticazione Kerberos, ad esempio l'aggiunta o la rimozione di un account, è necessario eseguire <strong>Enable-CsTopology</strong> dal prompt dei comandi di Lync Server Management Shell.
