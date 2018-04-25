---
title: Debug-CsInterPoolReplication
TOCTitle: Debug-CsInterPoolReplication
ms:assetid: 945bfd1c-1759-4869-9316-b3260fcc633d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619185(v=OCS.15)
ms:contentKeyID: 49301359
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Debug-CsInterPoolReplication

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica il corretto funzionamento della replica tra un pool di registrazione e il relativo pool di backup assegnato. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Debug-CsInterPoolReplication -PoolFqdn <Fqdn> [-BackupModule <All | CentralMgmt | PresenceFocus | DataConf>] [-Force <SwitchParameter>]

## Esempi

## Esempio 1

Il comando mostrato nell'Esempio 1 verifica lo stato della replica completa tra il pool atl-cs-001.litwareinc.com e il relativo pool di backup assegnato in precedenza.

    Debug-CsInterPoolReplication -PoolFqdn "atl-cs-001.litwareinc.com"

## Esempio 2

Nell'Esempio 2 viene verificata solo la replica dei dati delle conferenze dati tra il pool atl-cs-001.litwareinc.com e il relativo pool di backup assegnato in precedenza.

    Debug-CsInterPoolReplication -PoolFqdn "atl-cs-001.litwareinc.com" -BackupModule DataConf

## Descrizione dettagliata

In Lync Server 2013 ogni pool di registrazione può essere associato a un pool di backup. Il pool di backup mantiene una copia di tutti i dati archiviati nel pool primario. Se il pool primario risulta non disponibile, è possibile eseguire il failover automatico dei relativi utenti al pool di backup. In questo modo gli utenti potranno continuare a utilizzare Lync Server anche quando il relativo pool principale non è disponibile. Il cmdlet Debug-CsInterPoolReplication viene utilizzato per confrontare i dati archiviati in un pool primario e il relativo pool di backup e quindi verificare che la replica tra i due pool funzioni nel modo previsto.

Si noti che questo comando non funzionerà se al pool testato non è stato assegnato un pool di backup.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Debug-CsInterPoolReplication"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet Debug-CsInterPoolReplication non sono disponibili in Pannello di controllo di Lync Server.

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
<td><p>Nome di dominio completo del pool primario testato. Ad esempio:</p>
<p>-PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>BackupModule</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Hadr.BackupService.BackupModules</p></td>
<td><p>Consente agli amministratori di specificare l'archivio dati da verificare. I valori consentiti sono:</p>
<p>* All</p>
<p>* CentralMgmt</p>
<p>* PresenceFocus</p>
<p>* DataConf</p>
<p>Il valore predefinito è All.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Debug-CsInterPoolReplication non accetta dati da pipeline.

## Tipi restituiti

Valore stringa.

