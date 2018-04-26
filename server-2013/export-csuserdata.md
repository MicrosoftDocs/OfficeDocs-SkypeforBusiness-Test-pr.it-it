---
title: Export-CsUserData
TOCTitle: Export-CsUserData
ms:assetid: 52c411e1-76da-48b8-b1e3-ddc7c7f86e3d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204897(v=OCS.15)
ms:contentKeyID: 49300581
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Export-CsUserData

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Esporta i dati degli utenti in un formato che può essere importato in Lync Server. I dati verranno esportati come file ZIP contenente una coppia di documenti XML. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Export-CsUserData -PoolFqdn <Fqdn> <COMMON PARAMETERS>

    Export-CsUserData -Identity <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: -FileName <String> [-ConfDirectoryFilter <String>] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-LegacyFormat <SwitchParameter>] [-UserFilter <String>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 esporta i dati degli utenti dal pool atl-cs-001.litwareinc.com in un file denominato C:\\Logs\\ExportedUserData.zip.

    Export-CsUserData -PoolFqdn "atl-cs-001.litwareinc.com" -FileName "C:\Logs\ExportedUserData.zip"

## Descrizione dettagliata

Il cmdlet **Export-CsUserData** consente agli amministratori di esportare i dati degli utenti e/o la directory conferenze di un pool di Lync Server. Questi dati, che possono essere salvati nel formato dei dati utente utilizzato da Lync Server 2013 o Microsoft Lync Server 2010, possono quindi essere importati utilizzando il cmdlet [Import-CsUserData](import-csuserdata.md).

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Export-CsUserData"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Export-CsUserData** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>FileName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Percorso completo del file ZIP che verrà creato dal cmdlet <strong>Export-CsUserData</strong>. In questo file saranno contenuti i dati utente esportati. Ad esempio:</p>
<p>-FileName &quot;C:\Logs\ExportedData.zip&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo del pool in cui è installato il database utenti contenente i dati degli utenti da esportare, ad esempio:</p>
<p>-Identity &quot;atl-sql-001.litwareinc.com&quot;</p>
<p>Si noti che è possibile recuperare i nomi di dominio completi dei pool di database utenti utilizzando il comando seguente:</p>
<p>Get-CsService –UserDatabase</p></td>
</tr>
<tr class="odd">
<td><p><em>PoolFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del pool di registrazione contenente i dati degli utenti da esportare, ad esempio:</p>
<p>-PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>ConfDirectoryFilter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Se specificato, questo parametro consente di esportare informazioni sulla directory conferenze specificata. Per esportare ad esempio i dati dalla directory conferenze con ID 13, utilizzare la sintassi seguente:</p>
<p>-ConfDirectoryFilter 13</p>
<p>Per ottenere gli ID delle directory conferenze, utilizzare il comando seguente:</p>
<p>Get-CsConferenceDirectory</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente agli amministratori di specificare il nome FQDN del controller di dominio da utilizzare quando si esegue il cmdlet <strong>Export-CsUserData</strong>. Se non viene specificato, il cmdlet utilizzerà il primo controller di dominio disponibile.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>LegacyFormat</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se si specifica questo parametro, i dati verranno salvati nel formato utilizzato da Microsoft Lync Server 2010.</p></td>
</tr>
<tr class="even">
<td><p><em>UserFilter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di esportare dati di un singolo utente. L'utente viene indicato specificando il relativo indirizzo SIP, escluso il prefisso sip:, ad esempio:</p>
<p>-UserFilter &quot;kenmyer@litwareinc.com&quot;</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Export-CsUserData** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Export-CsUserData** crea nuovi file ZIP.

## Vedere anche

#### Ulteriori risorse

[Convert-CsUserData](convert-csuserdata.md)  
[Import-CsUserData](import-csuserdata.md)  
[Sync-CsUserData](sync-csuserdata.md)  
[Update-CsUserData](update-csuserdata.md)

