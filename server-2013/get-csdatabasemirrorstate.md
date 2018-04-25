---
title: Get-CsDatabaseMirrorState
TOCTitle: Get-CsDatabaseMirrorState
ms:assetid: 458f5367-ee04-4281-971f-08f79a625509
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204845(v=OCS.15)
ms:contentKeyID: 49300384
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsDatabaseMirrorState

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni che indicano se è stato implementato il mirroring del database per un database specifico in un pool specifico. Il mirroring del database consente di disporre contemporaneamente di due copie di uno stesso database che risiedono ognuna in un server diverso. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsDatabaseMirrorState -PoolFqdn <Fqdn> [-DatabaseType <Application | Archiving | Monitoring | User | Provision | CentralAdmin | Lyss | Registrar | Edge | PersistentChat | PersistentChatCompliance | CentralMgmt>] [-LocalStore <SwitchParameter>] [-Report <String>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce lo stato del mirror del database assegnato al database di monitoraggio per il pool atl-cs-001.litwareinc.com.

    Get-CsDatabaseMirrorState -PoolFqdn "atl-cs-001.litwareinc.com" -DatabaseType Monitoring

## Descrizione dettagliata

Il cmdlet **Get-CsDatabaseMirrorState** restituisce informazioni sui database mirror configurati per un pool, ad esempio informazioni sui database mirror eventualmente configurati per il database Front End Server, il database del servizio Informazioni percorso, i database di registrazione dettagli chiamata e della qualità percepita dagli utenti e così via. Per ogni database il cmdlet segnalerà lo stato di sincronizzazione del database primario e del database mirror. In alcuni casi verrà visualizzato un output simile al seguente, incluso il valore di proprietà DatabaseInaccessibleOrMirroringNotEnabled:

DatabaseName : lcscdr

StateOnPrimary : DatabaseInaccessibleOrMirroringNotEnabled

StateOnMirror : DatabaseInaccessibleOrMirroringNotEnabled

MirroringStatusOnPrimary :

MirroringStatusOnSecondary :

Questo significa che non è stato assegnato alcun database mirror al database primario utilizzato per la gestione dei dati dei dettagli chiamata, in questo caso il database lcscdr.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsDatabaseMirrorState"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsDatabaseMirrorState** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>PoolFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del pool di cui viene controllato lo stato del mirroring del database, ad esempio:</p>
<p>-PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>DatabaseType</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.DatabaseNameType</p></td>
<td><p>Tipo di database di cui viene controllato lo stato del mirror. I valori consentiti sono:</p>
<p>Application</p>
<p>Archiving</p>
<p>CentralAdmin</p>
<p>CentralMgmt</p>
<p>Edge</p>
<p>Lyss</p>
<p>Monitoring</p>
<p>PersistentChat</p>
<p>PersistentChatCompliance</p>
<p>Provision</p>
<p>Registrar</p>
<p>User</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera lo stato del mirror di backup dalla replica locale dell'archivio di gestione centrale anziché direttamente dall'archivio di gestione centrale.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet, ad esempio:</p>
<p>-Report &quot;C:\Logs\DatabaseMirrorState.html&quot;</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsDatabaseMirrorState** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Get-CsDatabaseMirrorState** restituisce istanze della classe Microsoft.Rtc.Management.Deployment.DatabaseMirrorState.

## Vedere anche

#### Ulteriori risorse

[Install-CsMirrorDatabase](install-csmirrordatabase.md)  
[Uninstall-CsMirrorDatabase](uninstall-csmirrordatabase.md)

