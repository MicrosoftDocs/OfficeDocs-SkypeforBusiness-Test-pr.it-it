---
title: Remove-CsPersistentChatComplianceConfiguration
TOCTitle: Remove-CsPersistentChatComplianceConfiguration
ms:assetid: 2d54eabf-fbb5-435b-9a71-d6b03beb09a5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204767(v=OCS.15)
ms:contentKeyID: 49300052
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPersistentChatComplianceConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una raccolta esistente di impostazioni di configurazione della conformità di Chat persistente. La conformità di Chat persistente consente agli amministratori di gestire un archivio di elementi e attività di Chat persistente, tra cui nuovi messaggi, nuovi eventi, ad esempio un utente che accede a una chat o ne esce, caricamenti e download di file e ricerche nella cronologia di chat. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Remove-CsPersistentChatComplianceConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Nell'esempio 1 vengono rimosse le impostazioni di configurazione della conformità di Chat persistente applicate al sito Redmond.

    Remove-CsPersistentChatComplianceConfiguration -Identity "site:Redmond"

## Esempio 2

Nell'esempio 2 vengono rimosse tutte le impostazioni di configurazione della conformità di Chat persistente applicate nell'ambito del sito. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsPersistentChatComplianceConfiguration** e il parametro Filter per recuperare tutte le impostazioni assegnate nell'ambito del sito. Per eseguire questa attività, viene utilizzato il valore di filtro "site:\*". Le impostazioni dell'ambito del sito recuperate vengono quindi inviate tramite pipe al cmdlet **Remove-CsPersistentChatComplianceConfiguration**, che le rimuove.

    Get-CsPersistentChatComplianceConfiguration -Filter "site:*" | Remove-CsPersistentChatComplianceConfiguration

## Esempio 3

Nell'esempio 3 viene illustrato come rimuovere tutte le impostazioni di configurazione della conformità di Chat persistente in cui le proprietà AddUserDetails e AddChatRoomDetails sono entrambe impostate su True. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsPersistentChatComplianceConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione della conformità di Chat persistente. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui le proprietà AddUserDetails e AddChatRoomDetails sono uguali a True ($True). La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsPersistentChatComplianceConfiguration**, che elimina ogni elemento in essa contenuto.

    Get-CsPersistentChatComplianceConfiguration | Where-Object {$_.AddUserDetals -eq $True -and $_.AddChatRoomDetails -eq $True} | Remove-CsPersistentChatComplianceConfiguration

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Molte organizzazioni, ad esempio organizzazioni che operano nel settore sanitario o finanziario, sono tenute a conservare archivi di tutte le comunicazioni elettroniche, incluse le eventuali conversazioni effettuate utilizzando il servizio Chat persistente. Lync Server 2013 consente di creare un database di conformità separato contenente un archivio dettagliato di tutto ciò che si verifica nelle chat room di Chat persistente. La conformità di Chat persistente può essere abilitata o disabilitata nell'ambito del sito o del servizio, ovvero può essere abilitata o disabilitata per un pool di Chat persistente specifico. La conformità di Chat persistente inoltre può essere gestita solo utilizzando l'interfaccia della riga di comando Windows PowerShell. Nel Pannello di controllo di Lync Server 2013 non sono disponibili opzioni per la gestione della conformità di Chat persistente.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPersistentChatComplianceConfiguration"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Remove-CsPersistentChatComplianceConfiguration** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco delle impostazioni di conformità di Chat persistente da rimuovere. Per rimuovere una raccolta di impostazioni configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>Per rimuovere una raccolta configurata nell'ambito del servizio, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;service:PersistentChatServer:atl-gc-001.litwareinc.com&quot;</p>
<p>Si noti che non è possibile utilizzare i caratteri jolly con il parametro Identity.</p>
<p>È inoltre possibile eseguire il cmdlet <strong>Remove-CsPersistentChatComplianceConfiguration</strong> per la raccolta di impostazioni globali. In questo caso, la raccolta globale però non verrà rimossa. Verranno invece reimpostate sui valori predefiniti tutte le proprietà incluse nella raccolta.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Remove-CsPersistentChatComplianceConfiguration** accetta le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatComplianceConfiguration inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsPersistentChatComplianceConfiguration** invece elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatComplianceConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsPersistentChatComplianceConfiguration](get-cspersistentchatcomplianceconfiguration.md)  
[New-CsPersistentChatComplianceConfiguration](new-cspersistentchatcomplianceconfiguration.md)  
[Set-CsPersistentChatComplianceConfiguration](set-cspersistentchatcomplianceconfiguration.md)

