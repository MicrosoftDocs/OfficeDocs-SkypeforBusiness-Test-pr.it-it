---
title: Get-CsPersistentChatComplianceConfiguration
TOCTitle: Get-CsPersistentChatComplianceConfiguration
ms:assetid: 01fe3824-32fb-4d75-b80a-8a7dcc109911
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204625(v=OCS.15)
ms:contentKeyID: 49299490
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPersistentChatComplianceConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle impostazioni di configurazione della conformità di Chat persistente attualmente in uso nell'organizzazione. La conformità di Chat persistente consente agli amministratori di gestire un archivio di elementi e attività di Chat persistente, tra cui nuovi messaggi, nuovi eventi, ad esempio un utente che accede a una chat room o ne esce, caricamenti e download di file e ricerche nella cronologia di chat. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsPersistentChatComplianceConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsPersistentChatComplianceConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce informazioni su tutte le impostazioni di configurazione della conformità di Chat persistente attualmente in uso nell'organizzazione.

    Get-CsPersistentChatComplianceConfiguration

## Esempio 2

Nell'esempio 2 vengono restituite informazioni sulle impostazioni di configurazione della conformità di Chat persistente applicate al sito Redmond.

    Get-CsPersistentChatComplianceConfiguration -Identity "site:Redmond"

## Esempio 3

Nell'esempio 3 vengono restituite informazioni su tutte le impostazioni di configurazione della conformità di Chat persistente applicate nell'ambito del servizio. Per ottenere questo risultato, vengono inclusi il parametro Filter e il valore "service:\*".

    Get-CsPersistentChatComplianceConfiguration -Filter "service:*"

## Esempio 4

Nell'esempio 4 vengono restituite informazioni per tutte le impostazioni di configurazione della conformità di Chat persistente in cui la proprietà OneChatRoomPerOutputFile è uguale a True. A tale scopo, il comando utilizza innanzitutto **Get-CsPersistentChatComplianceConfiguration** per restituire una raccolta costituita da tutte le impostazioni di configurazione della conformità di Chat persistente. La raccolta così ottenuta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà OneChatRoomPerOutputFile è uguale a True ($True).

    Get-CsPersistentChatComplianceConfiguration | Where-Object {$_.OneChatRoomPerOutputFile -eq $True}

## Esempio 5

Nell'esempio 5 le informazioni restituite sono relative solo alle impostazioni di configurazione della conformità di Chat persistente in cui la proprietà CustomConfiguration è impostata su un valore Null. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsPersistentChatComplianceConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione della conformità di Chat persistente attualmente in uso. La raccolta così ottenuta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui CustomConfiguration è uguale a un valore Null ($Null)

    Get-CsPersistentChatComplianceConfiguration | Where-Object {$_.CustomConfiguration -ne $Null}

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Molte organizzazioni, tra cui le organizzazioni che operano nel settore sanitario o finanziario, sono tenute a conservare archivi di tutte le comunicazioni elettroniche, incluse le eventuali conversazioni effettuate utilizzando il servizio Chat persistente. Lync Server consente di creare un database di conformità separato contenente un archivio dettagliato di tutto ciò che si verifica nelle chat room di Chat persistente. La conformità di Chat persistente può essere abilitata o disabilitata nell'ambito del sito o del servizio, ovvero può essere abilitata o disabilitata per un pool di Chat persistente specifico. La conformità di Chat persistente inoltre può essere gestita solo utilizzando l'interfaccia della riga di comando Windows PowerShell. Nel Pannello di controllo di Lync Server 2013 non sono disponibili opzioni per la gestione della conformità di Chat persistente.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt di Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPersistentChatComplianceConfiguration"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsPersistentChatComplianceConfiguration** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare i caratteri jolly per specificare la raccolta o le raccolte di impostazioni di configurazione della conformità di Chat persistente da restituire. Questa sintassi ad esempio restituisce tutte le impostazioni configurate nell'ambito del servizio:</p>
<p>-Filter &quot;service:*&quot;</p>
<p>Non è possibile utilizzare i parametri Filter e Identity nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco delle impostazioni di conformità di Chat persistente da restituire. Per ottenere la raccolta globale, utilizzare la sintassi seguente:</p>
<p>-Identity &quot;global&quot;</p>
<p>Per restituire una raccolta di impostazioni configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>Per restituire una raccolta configurata nell'ambito del servizio, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;service:PersistentChatServer:atl-gc-001.litwareinc.com&quot;</p>
<p>Si noti che non è possibile utilizzare i caratteri jolly con il parametro Identity.</p>
<p>Se in un comando non sono inclusi né il parametro Identity né il parametro Filter, il cmdlet <strong>Get-CsPersistentChatComplianceConfiguration</strong> restituirà informazioni su tutte le impostazioni di conformità di Chat persistente in uso nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di conformità di Chat persistente dalla replica locale dell'archivio di gestione centrale anziché direttamente dall'archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsPersistentChatComplianceConfiguration** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsPersistentChatComplianceConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatComplianceConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsPersistentChatComplianceConfiguration](new-cspersistentchatcomplianceconfiguration.md)  
[Remove-CsPersistentChatComplianceConfiguration](remove-cspersistentchatcomplianceconfiguration.md)  
[Set-CsPersistentChatComplianceConfiguration](set-cspersistentchatcomplianceconfiguration.md)

