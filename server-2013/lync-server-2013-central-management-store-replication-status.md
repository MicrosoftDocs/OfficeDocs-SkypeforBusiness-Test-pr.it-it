---
title: "Lync Server 2013: stato della replica dell'archivio di gestione centrale"
TOCTitle: Stato della replica dell'archivio di gestione centrale
ms:assetid: f514f88d-986b-4e45-b79b-e04a7616c1fe
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn720926(v=OCS.15)
ms:contentKeyID: 62240090
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Stato della replica dell'archivio di gestione centrale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-01-26_

Quando un amministratore apporta qualsiasi tipo di modifica a Lync Server, ad esempio crea un nuovo criterio vocale o modifica le impostazioni di configurazione del server della rubrica, tale modifica viene registrata nell'archivio di gestione centrale e deve quindi essere replicata in tutti i computer che eseguono i servizi o i ruoli del server di Lync Server.

Per replicare i dati, Master Replicator (in esecuzione nel server di gestione centrale) crea uno snapshot dei dati di configurazione modificati e una copia di questo snapshot viene quindi inviata a ogni computer che esegue i servizi o i ruoli del server di Lync Server. In tali computer un agente di replica riceve lo snapshot e carica i dati modificati, quindi invia al Master Replicator un messaggio in cui è indicato lo stato aggiornato della replica.

Il cmdlet Get-CsManagementStoreReplicationStatus consente di verificare lo stato della replica per alcuni o tutti i computer Lync Server dell'organizzazione.

Chi può eseguire questo cmdlet? Per impostazione predefinita, i membri dei seguenti gruppi sono autorizzati a eseguire in locale il cmdlet Get-CsManagementStoreReplicationStatus: RTCUniversalUserAdmins, RTCUniversalServerAdmins.

Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Get-CsManagementStoreReplicationStatus"}

## Vedere anche

#### Ulteriori risorse

[Get-CsManagementStoreReplicationStatus](get-csmanagementstorereplicationstatus.md)

