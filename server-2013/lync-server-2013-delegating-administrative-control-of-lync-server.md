---
title: 'Lync Server 2013: Delega del controllo amministrativo di Lync Server'
TOCTitle: Delega del controllo amministrativo di Lync Server 2013
ms:assetid: 0f378eff-8ef4-4c60-9fd2-67d7ee259ef8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520951(v=OCS.15)
ms:contentKeyID: 49299690
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Delega del controllo amministrativo di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-22_

In Lync Server 2013 le attività amministrative vengono delegate agli utenti mediante la nuova funzionalità di controllo dell'accesso basato sui ruoli (RBAC). Quando si installa Lync Server, vengono creati automaticamente alcuni ruoli RBAC che corrispondono ai gruppi di sicurezza universali di Servizi di dominio Active Directory. Il ruolo RBAC CsHelpDesk, ad esempio, corrisponde al gruppo CsHelpDesk disponibile nel contenitore degli utenti di Servizi di dominio Active Directory. Ogni ruolo RBAC è inoltre associato a un insieme di cmdlet di Lync ServerWindows PowerShell che rappresentano le attività che possono essere eseguite dagli utenti a cui è stato assegnato il ruolo RBAC in questione. Al ruolo CsHelpDesk, ad esempio, sono stati assegnati i cmdlet Lock-CsClientPin e UnlockCsClientPin, pertanto gli utenti a cui viene assegnato tale ruolo possono bloccare e sbloccare i PIN utente. Al ruolo CsHelpDesk, tuttavia, non è stato assegnato il cmdlet New-CsVoicePolicy, quindi gli utenti con tale ruolo non possono creare nuovi criteri vocali.

## Visualizzazione di informazioni sui ruoli RBAC

È possibile recuperare le informazioni di base sui ruoli RBAC eseguendo il comando seguente da Lync Server Management Shell:

    Get-CsAdminRole

Tenere presente che per l'identità del ruolo RBAC, ad esempio CsVoiceAdministrator, esiste un mapping diretto con un gruppo di sicurezza presente nel contenitore degli utenti in Servizi di dominio Active Directory.

Per visualizzare un elenco dei cmdlet assegnati a un ruolo, utilizzare un comando simile al seguente:

    Get-CsAdminRole -Identity "CsHelpDesk" | Select-Object -ExpandProperty Cmdlets

## Assegnazione di un ruolo RBAC a un utente

Per assegnare un ruolo RBAC a un utente, è necessario aggiungere l'utente al gruppo di sicurezza appropriato di Active Directory. Ad esempio, per assegnare il ruolo CsLocationAdministrator a un utente, è necessario aggiungere tale utente al gruppo CsLocationAdministrator. A tale scopo, è possibile eseguire la procedura seguente:

**Per assegnare un utente a un gruppo di sicurezza**

1.  Utilizzando un account che dispone dell'autorizzazione per modificare i membri di un gruppo di Active Directory, eseguire l'accesso a un computer in cui è stato installato Utenti e computer di Active Directory.

2.  Fare clic sul pulsante **Start** , scegliere **Tutti i programmi** , **Strumenti di amministrazione** e quindi **Utenti e computer di Active Directory** .

3.  In Utenti e computer di Active Directory espandere il nome del dominio e fare clic sul contenitore degli   utenti.

4.  Fare clic con il pulsante destro del mouse sul gruppo di sicurezza **CsLocationAdministrator** e scegliere **Proprietà** .

5.  Nella finestra di dialogo **Proprietà** fare clic su **Aggiungi** nella scheda **Membri** .

6.  Nella finestra di dialogo **Seleziona utenti, computer o gruppi** digitare il nome utente o il nome visualizzato dell'utente da aggiungere al gruppo, ad esempio **Ken Myer** , nella casella **Immettere i nomi degli oggetti da selezionare** e quindi fare clic su **OK** .

7.  Nella finestra di dialogo **Proprietà** fare clic su **OK** .

Per verificare che il ruolo RBAC sia stato assegnato, utilizzare il cmdlet [Get-CsAdminRoleAssignment](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsAdminRoleAssignment) passandogli il nome di account SAM (SamAccountName), ovvero il nome di accesso di Active Directory, dell'utente. Ad esempio, eseguire questo comando da Lync Server Management Shell:

    Get-CsAdminRoleAssignment  -Identity "kenmyer"

