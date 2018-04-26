---
title: Update-CsUserData
TOCTitle: Update-CsUserData
ms:assetid: e3cb48e9-9b5e-4c73-ab54-4aea16533ed8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205358(v=OCS.15)
ms:contentKeyID: 49302281
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Update-CsUserData

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Utilizza informazioni sugli utenti precedentemente esportate per aggiornare i dati degli utenti di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Update-CsUserData -FileName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Force <SwitchParameter>] [-RoutingGroupFilter <String>] [-UserFilter <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 aggiorna i dati utente di Lync Server in base alle informazioni archiviate nel file C:\\Logs\\ExportedUserData.zip.

    Update-CsUserData -Filename "C:\Logs\ExportedUserData.zip"

## Esempio 2

Nell'esempio 2 i dati utente vengono aggiornati per un solo utente, ovvero l'utente con l'indirizzo SIP kenmyer@litwareinc.com. A tale scopo, viene incluso il parametro UserFilter seguito dall'indirizzo SIP dell'utente (senza il prefisso sip:).

    Update-CsUserData -Filename "C:\Logs\ExportedUserData.zip" -UserFilter "kenmyer@litwareinc.com"

## Descrizione dettagliata

Il cmdlet **Update-CsUserData** consente agli amministratori di aggiornare i dati utente per un utente o un set di utenti specificato. Si noti che questi dati devono essere stati precedentemente esportati utilizzando il cmdlet [Export-CsUserData](export-csuserdata.md). L'aggiornamento viene in genere eseguito per ripristinare i dati persi per un utente connesso.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Update-CsUserData"}

**Pannello di controllo di Lync Server:** The functions carried out by the **Update-CsUserData** cmdlet are not available in the Pannello di controllo di Lync Server.

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
<td><p>Percorso completo del file .ZIP o .XML contenente i dati utente da aggiornare. Ad esempio:</p>
<p>-FileName \ldblquote C:\Data\Lync2010.zip&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente agli amministratori di specificare il nome FQDN del controller di dominio da utilizzare quando si esegue il cmdlet <strong>Update-CsUserData</strong>. Se non viene specificato, il cmdlet utilizzerà il primo controller di dominio disponibile.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>RoutingGroupFilter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di aggiornare i dati solo per i gruppi di routing specificati. I gruppi di routing vengono utilizzati per indicare il server front-end utilizzato dagli utenti per la registrazione.</p></td>
</tr>
<tr class="even">
<td><p><em>UserFilter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di aggiornare i dati per un solo utente. Tale utente viene specificato mediante il relativo indirizzo SIP, senza prefisso sip:. Ad esempio:</p>
<p>-UserFilter &quot;kenmyer@litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Update-CsUserData** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Update-CsUserData** cmdlet aggiorna le informazioni sull'utente di Lync Server.

## Vedere anche

#### Ulteriori risorse

[Convert-CsUserData](convert-csuserdata.md)  
[Export-CsUserData](export-csuserdata.md)  
[Import-CsUserData](import-csuserdata.md)  
[Sync-CsUserData](sync-csuserdata.md)

