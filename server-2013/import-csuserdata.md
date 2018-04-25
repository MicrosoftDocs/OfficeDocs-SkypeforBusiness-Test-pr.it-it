---
title: Import-CsUserData
TOCTitle: Import-CsUserData
ms:assetid: f39ef951-ee5b-4200-b6fb-68a4d4d6e86f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205373(v=OCS.15)
ms:contentKeyID: 49302451
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsUserData

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Importa dati di utenti precedentemente esportati utilizzando il cmdlet Export-CsUserData. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Import-CsUserData -PoolFqdn <Fqdn> <COMMON PARAMETERS>

    Import-CsUserData -Identity <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: -FileName <String> [-ConfDirectoryFilter <String>] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-LegacyFormat <SwitchParameter>] [-RoutingGroupFilter <String>] [-UserFilter <String>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 importa dati utente da un file denominato C:\\Logs\\ExportedUserData.zip al pool atl-cs-001.litwareinc.com.

    Import-CsUserData -PoolFqdn "atl-cs-001.litwareinc.com" -FileName "C:\Logs\ExportedUserData.zip"

## Descrizione dettagliata

Il cmdlet Import-CsUserData viene utilizzato per importare in Lync Server dati di utenti e/o dati di directory conferenze precedentemente salvati. Si noti che questi dati devono essere stati esportati utilizzando il cmdlet [Export-CsUserData](export-csuserdata.md).

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi eventuali ruoli RBAC personalizzati creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsUserData"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Import-CsUserData** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Percorso completo del file di input contenente il dati utente esportati. Ad esempio:</p>
<p>-InputFile &quot;C:\Data\ExportedUsers.xml&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Identità del servizio del database utenti in cui devono essere importati i dati, ad esempio:</p>
<p>-Identity &quot;UserDatabase:atl-sql-001.litwareinc.com&quot;</p>
<p>Non è possibile utilizzare i parametri Identity e PoolFqdn nello stesso comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>PoolFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del pool di registrazione per i dati utente da importare. Ad esempio:</p>
<p>–PoolFqdn &quot;atl-cs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>ConfDirectoryFilter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Quando specificato, consente di importare informazioni sulla directory conferenze specificata. Ad esempio, per importare dati dalla directory conferenze con ID 13, utilizzare la sintassi seguente:</p>
<p>-ConfDirectoryFilter 13</p>
<p>È possibile restituire gli ID della directory conferenze utilizzando il comando seguente:</p>
<p>Get-CsConferenceDirectory</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente agli amministratori di specificare il nome FQDN del controller di dominio da utilizzare quando si esegue il cmdlet <strong>Import-CsUserData</strong>. Se non viene specificato, il cmdlet utilizzerà il primo controller di dominio disponibile.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Impedisce la visualizzazione di eventuali messaggi di errore non irreversibili che potrebbero verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>LegacyFormat</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Indica che i dati da importare sono stati esportati da una versione precedente di Lync Server o Office Communications Server.</p></td>
</tr>
<tr class="even">
<td><p><em>RoutingGroupFilter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di importare solo i dati relativi agli utenti appartenenti allo stesso gruppo di routing. I gruppi di routing vengono utilizzati da Lync Server per determinare il Front End Server utilizzato dagli utenti per la registrazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserFilter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di importare i dati utente per un solo utente. Per convertire i dati per un utente specificato (e solo per tale utente), impostare il parametro UserFilter sull'indirizzo SIP di tale utente, assicurandosi di omettere il prefisso sip:. Ad esempio:</p>
<p>-UserFilter &quot;kenmyer@litwareinc.com&quot;</p>
<p>Questo parametro consente di importare i dati di un utente alla volta.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Import-CsUserData** non accetta input inviato tramite pipeline.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Convert-CsUserData](convert-csuserdata.md)  
[Export-CsUserData](export-csuserdata.md)  
[Sync-CsUserData](sync-csuserdata.md)  
[Update-CsUserData](update-csuserdata.md)

