---
title: 'Lync Server 2013: Amministrazione degli utenti in una distribuzione ibrida'
TOCTitle: Amministrazione degli utenti in una distribuzione ibrida
ms:assetid: 6924ed7b-30a9-4be7-b952-90655625f2c8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204967(v=OCS.15)
ms:contentKeyID: 49300850
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Amministrazione degli utenti in una distribuzione ibrida di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-05-29_

Per gestire le impostazioni utente e i criteri per gli utenti di cui è stata eseguita la migrazione a Lync Online, è possibile utilizzare le funzionalità di gestione degli utenti disponibili nel portale online di Microsoft Office 365. Per eseguire attività amministrative, è necessario eseguire l'accesso con un account di amministratore tenant.

## Rispostamento degli utenti in locale

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Le informazioni contenute in questa sezione sono applicabili solo agli utenti creati e abilitati per Lync in locale e in seguito spostati da una distribuzione in locale a Lync Online. Se si desidera spostare gli utenti creati in Lync Online (e mai abilitati per Lync in una distribuzione in locale) vedere, <a href="lync-server-2013-moving-users-from-lync-online-to-lync-on-premises.md">Spostare gli utenti da Lync Online a Lync in locale in Lync Server 2013</a>.</td>
</tr>
</tbody>
</table>


  - Eseguire i seguenti cmdlet per rispostare un utente da Lync Online a Lync in locale:
    
        $cred=Get-Credential
    
        Move-CsUser -Identity username@contoso.com -Target localpool.contoso.com -Credential $cred -HostedMigrationOverrideUrl <URL>

Il formato dell'URL specificato per il parametro **HostedMigrationOverrideUrl** deve essere l'URL del pool in cui è in esecuzione il servizio di migrazione ospitata, nel formato seguente:

*Https://\<FQDN pool\>/HostedMigration/hostedmigrationService.svc* . È possibile determinare l'URL del servizio di migrazione ospitata visualizzando l'URL del Pannello di controllo di Lync Online per l'account del tenant Office 365.

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

