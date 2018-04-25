---
title: Cmdlet per i server della Rubrica
TOCTitle: Cmdlet per i server della Rubrica
ms:assetid: 33da45da-3c57-4d04-9679-f0e5a0cfd37e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg415643(v=OCS.15)
ms:contentKeyID: 49300123
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlet per i server della Rubrica

 

_**Ultima modifica dell'argomento:** 2012-06-26_

I server della Rubrica operano come intermediari tra Servizi di dominio Active Directory e Microsoft Lync Server 2013. Il server della Rubrica garantisce che le informazioni degli utenti archiviate in Lync Server 2013 siano sincronizzate con le informazioni degli utenti archiviate in Active Directory. A tale scopo, i file della Rubrica vengono sincronizzati periodicamente con le informazioni archiviate nel database degli utenti. A sua volta, Lync Server offre diversi cmdlet per la gestione dei server della Rubrica.

## Cmdlet per i server della Rubrica

Non è possibile configurare le impostazioni dei server della Rubrica nel Pannello di controllo di Lync Server. Lo strumento principale per la gestione di queste impostazioni è Windows PowerShell. Viene riportato di seguito un elenco di cmdlet direttamente correlati alla gestione dei server della Rubrica:

**Server della Rubrica**

  -   
    [Get-CsAddressBookConfiguration](get-csaddressbookconfiguration.md)

  -   
    [New-CsAddressBookConfiguration](new-csaddressbookconfiguration.md)

  -   
    [Remove-CsAddressBookConfiguration](remove-csaddressbookconfiguration.md)

  -   
    [Set-CsAddressBookConfiguration](set-csaddressbookconfiguration.md)

<!-- end list -->

  -   
    [Update-CsAddressBook](update-csaddressbook.md)

  -   
    [Debug-CsAddressBookReplication](debug-csaddressbookreplication.md)

<!-- end list -->

  -   
    [Test-CsAddressBookService](test-csaddressbookservice.md)

  -   
    [Test-CsAddressBookWebQuery](test-csaddressbookwebquery.md)

## Vedere anche

#### Ulteriori risorse

[Blog su Lync Server PowerShell](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x410)

