---
title: Update-CsUserDatabase
TOCTitle: Update-CsUserDatabase
ms:assetid: 86ed4291-70cc-4c41-ab2a-e5f7546a0f1f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398682(v=OCS.15)
ms:contentKeyID: 49301224
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Update-CsUserDatabase

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Forza il database utenti di back-end a cancellare il relativo stato di replica con Active Directory. Il database deve quindi leggere di nuovo tutte le informazioni relative agli utenti archiviate in Servizi di dominio Active Directory. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Update-CsUserDatabase [-Force <SwitchParameter>] [-Fqdn <Fqdn>]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 viene individuato il database utenti per il pool in cui è situato il computer locale, quindi vengono forzate la connessione del database e la restituzione delle informazioni utente complete da Active Directory.

    Update-CsUserDatabase

## ESEMPIO 2

Con l'esempio 2 viene mostrato come forzare una nuova lettura dei dati da Active Directory per un database utenti specifico. In questo caso, si tratta del database utenti per il pool atl-cs-001.litwareinc.com.

    Update-CsUserDatabase -Fqdn atl-cs-001.litwareinc.com

## Descrizione dettagliata

Il database utenti di Lync Server include informazioni dettagliate su contatti, gruppi e autorizzazioni di accesso. In quanto tale, il database deve sincronizzare periodicamente il proprio contenuto con le informazioni archiviate in Active Directory.

Nella maggior parte dei casi la sincronizzazione automatica tra il database utenti e Active Directory consente di mantenere aggiornate le informazioni nel database utenti. È tuttavia possibile che si verifichi un problema che impedisca tale sincronizzazione automatica. In tal caso, è possibile utilizzare il cmdlet **Update-CsUserDatabase** per forzare l'aggiornamento del contenuto del database utenti con una nuova lettura di tutte le informazioni utente archiviate in Active Directory. Questo cmdlet potrebbe rivelarsi necessario anche quando un aggiornamento del prodotto include una modifica al servizio User Replicator.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Update-CsUserDatabase** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Update-CsUserDatabase"}

## Parametri


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Obbligatorio</th>
<th>Tipo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di ignorare la visualizzazione di messaggi di errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Fqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo (FQDN) del computer che ospita il database utenti. Se questo parametro non viene specificato, il cmdlet <strong>Update-CsUserDatabase</strong> aggiorna il database utenti per il pool a cui appartiene il computer locale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Update-CsUserDatabase** non accetta input tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Update-CsUserDatabase** invece aggiorna le istanze dell'oggetto Microsoft.Rtc.Management.Xds.DisplayuserDatabase.

## Vedere anche

#### Ulteriori risorse

[Get-CsUserDatabaseState](get-csuserdatabasestate.md)  
[Set-CsUserDatabaseState](set-csuserdatabasestate.md)

