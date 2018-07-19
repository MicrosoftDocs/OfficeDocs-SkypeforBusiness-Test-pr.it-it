---
title: 'Lync Server 2013: Spostare utenti in Lync Online'
TOCTitle: Spostare utenti in Lync Online
ms:assetid: 6a523c86-2eac-4fa4-973a-4406872c9a7d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204969(v=OCS.15)
ms:contentKeyID: 49300870
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Spostare utenti in Lync Online in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-05-29_

Prima di avviare la migrazione degli utenti a Lync Online, è consigliabile eseguire il backup dei dati utente associati all'account da spostare. Non tutti i dati utente vengono spostati insieme all'account utente. Per ulteriori informazioni, vedere [Requisiti di backup e ripristino: dati](lync-server-2013-backup-and-restoration-requirements-data.md).

## Eseguire la migrazione delle impostazioni utente a Lync Online

Le impostazioni utente vengono spostate insieme all'account utente, ma alcune impostazioni locali non vengono spostate insieme all'account.

## Spostamento degli utenti pilota in Lync Online

Prima di iniziare a spostare gli utenti in Lync Online, può essere utile spostare solo alcuni utenti pilota per verificare la corretta configurazione dell'ambiente. Sarà così possibile controllare che le funzionalità e i servizi di Lync funzionino come previsto prima di tentare lo spostamento di ulteriori utenti.

Per spostare un utente locale nel tenant di Skype for Business online, eseguire i cmdlet seguenti in Lync Server Management Shell utilizzando le credenziali di amministratore per il tenant di Microsoft Office 365. Sostituire "username@contoso.com" con le informazioni dell'utente da spostare.

    $creds=Get-Credential

    Move-CsUser -Identity username@contoso.com -Target sipfed.online.lync.com -Credential $creds -HostedMigrationOverrideUrl <URL>

Il formato dell'URL specificato per il parametro **HostedMigrationOverrideUrl** deve essere l'URL del pool in cui è in esecuzione il servizio di migrazione ospitata, nel formato seguente: *Https://\<FQDN pool\>/HostedMigration/hostedmigrationService.svc* .

È possibile determinare l'URL del servizio di migrazione ospitata visualizzando l'URL del Pannello di controllo di Lync Online per l'account del tenant Office 365.

**Per determinare l'URL del servizio di migrazione ospitata per il tenant Office 365**

1.  Accedere al tenant Office 365 come amministratore.

2.  Aprire l' **Interfaccia di amministrazione di Lync** .

3.  Con l' **Interfaccia di amministrazione di Lync** visualizzata, selezionare e copiare l'URL nella barra degli indirizzi fino a **lync.com**. L'URL è simile a quello seguente:
    
    `https://webdir0a.online.lync.com/lscp/?language=en-US&tenantID=`

4.  Sostituire **webdir** nell'URL con **admin**. Si otterrà quanto segue:
    
    `https://admin0a.online.lync.com`

5.  Aggiungere la stringa seguente all'URL: **/HostedMigration/hostedmigrationservice.svc**.
    
    L'URL risultante, che corrisponde al valore di **HostedMigrationOverrideUrl**, è simile al seguente:
    
    `https://admin0a.online.lync.com/HostedMigration/hostedmigrationservice.svc`

## Spostamento degli utenti in Lync Online

È possibile spostare più utenti tramite il cmdlet [Get-CsUser](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsUser) con il parametro –Filter per selezionare gli utenti con una proprietà specifica assegnata agli account utente, come ad esempio RegistrarPool. È quindi possibili inviare gli utenti restituiti al cmdlet [Move-CsUser](move-csuser.md), come indicato nell'esempio seguente.

    Get-CsUser -Filter {UserProperty -eq "UserPropertyValue"} | Move-CsUser -Target sipfed.online.lync.com -Credential $creds -HostedMigrationOverrideUrl <URL>

È inoltre possibile utilizzare il parametro -OU per recuperare tutti gli utenti nell'unità organizzativa specificata, come indicato nell'esempio seguente.

    Get-CsUser -OU "cn=hybridusers,cn=contoso.." | Move-CsUser -Target sipfed.online.lync.com -Credentials $creds -HostedMigrationOverrideUrl <URL>

## Verificare le impostazioni utente e le funzionalità di Lync Online

È possibile verificare il corretto spostamento degli utenti nei modi seguenti:

  - Visualizzare lo stato dell'utente nel pannello di controllo di Lync Online. L'indicatore visivo per gli utenti locali e quelli online è diverso.

  - Eseguire il cmdlet seguente:
    
        Get-CsUser -Identity

