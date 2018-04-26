---
title: 'Lync Server 2013: Creare un account di autenticazione Kerberos'
TOCTitle: Creare un account di autenticazione Kerberos
ms:assetid: 63f0cef6-562a-4209-ae25-71f8dc7c7295
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398449(v=OCS.15)
ms:contentKeyID: 49300781
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare un account di autenticazione Kerberos in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-01-02_

Per eseguire correttamente questa procedura, è necessario essere connessi al server o al dominio almeno come membri del gruppo Domain Admins.

È possibile creare account di autenticazione Kerberos per ogni sito oppure creare un singolo account di autenticazione Kerberos e utilizzarlo per tutti i siti. Si utilizzano cmdlet di Windows PowerShell per creare e gestire gli account, inclusa l'identificazione degli account assegnati a ogni sito. Gli account di autenticazione Kerberos non vengono visualizzati in Generatore di topologie e nel Pannello di controllo di Lync Server 2013. Utilizzare la procedura seguente per creare uno o più account utente da utilizzare per l'autenticazione Kerberos.

## Per creare un account Kerberos

1.  Come membro del gruppo Domain Admins, accedere a un computer nel dominio che esegue Lync Server 2013 oppure a un computer in cui sono installati gli strumenti di amministrazione.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Dalla riga di comando eseguire il comando seguente:
    
        New-CsKerberosAccount -UserAccount "Domain\UserAccount" -ContainerDN "CN=Users,DC=DomainName,DC=DomainExtension"
    
    Ad esempio:
    
        New-CsKerberosAccount -UserAccount "Contoso\KerbAuth" -ContainerDN "CN=Users,DC=contoso,DC=com"

4.  Verificare che l'oggetto Computer sia stato creato. A tale scopo aprire Utenti e computer di Active Directory, espandere il contenitore **Utenti** e quindi verificare che l'oggetto Computer per l'account utente sia presente nel contenitore.

