---
title: Update-CsAddressBook per la gestione della rubrica
TOCTitle: Update-CsAddressBook per la gestione della rubrica
ms:assetid: 0ffd2ef8-201c-44aa-8c64-1c7b0eaa7d48
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg429695(v=OCS.15)
ms:contentKeyID: 49299708
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Update-CsAddressBook per la gestione della rubrica

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Chi può eseguire questo cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet Update-CsAddressBook i membri dei gruppi seguenti: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli di Controllo dell'accesso basato sui ruoli (RBAC) a cui tale cmdlet è stato assegnato, inclusi i ruoli RBAC personalizzati creati personalmente, al prompt di Windows PowerShell eseguire il comando seguente:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Update-CsAddressBook"}

Il cmdlet Update-CsAddressBook sostituisce il comando **abserver.exe –syncNow** di Office Communications Server. Lo scopo del cmdlet è quello di avviare immediatamente una sincronizzazione anziché attendere l'intervallo di tempo pianificato. Il primo comando di esempio aggiorna tutte le rubriche dell'organizzazione. Il secondo aggiorna solo la rubrica associata al server definito.


> [!NOTE]
> In Lync Server 2013, User Replicator di Lync Server acquisirà le modifiche da Active Directory e aggiornerà il database degli utenti di Lync Server in base a un intervallo configurato. User Replicator di Lync Server, inoltre, propagherà rapidamente le modifiche al database RTCab senza che l'amministratore esegua Update-CSAddressBook. Gli amministratori devono solo eseguire Update-CSAddressBook se è abilitato il download del file della Rubrica.



Ad esempio:

    Update-CsAddressBook

    Update-CsAddressBook -Fqdn atl-abs-001.contoso.com

Per una descrizione dettagliata del comando completo, vedere l'argomento seguente nella guida di riferimento principale ai cmdlet RTC di Windows PowerShell di Lync Server.

## Vedere anche

#### Ulteriori risorse

[Update-CsAddressBook](https://docs.microsoft.com/en-us/powershell/module/skype/Update-CsAddressBook)

