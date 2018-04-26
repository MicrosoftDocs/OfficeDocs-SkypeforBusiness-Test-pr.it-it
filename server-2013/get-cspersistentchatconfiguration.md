---
title: Get-CsPersistentChatConfiguration
TOCTitle: Get-CsPersistentChatConfiguration
ms:assetid: a15ce45f-00cc-49af-9ef4-3991d891d37e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205140(v=OCS.15)
ms:contentKeyID: 49301510
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsPersistentChatConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce le informazioni sulle impostazioni di configurazione di Chat persistente attualmente in uso nell'organizzazione. Tali impostazioni vengono utilizzate per gestire il servizio Chat persistente e consentono ad esempio di specificare il numero massimo di utenti che possono partecipare a una chat room. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsPersistentChatConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsPersistentChatConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce le informazioni su tutte le impostazioni di configurazione di Chat persistente in uso nell'organizzazione.

    Get-CsPersistentChatConfiguration

## Esempio 2

Nell'esempio 2 vengono restituite le informazioni su un insieme specifico di impostazioni di configurazione di Chat persistente, ovvero le impostazioni applicate al sito Redmond.

    Get-CsPersistentChatConfiguration -Identity "site:Redmond"

## Esempio 3

Nell'esempio 3 vengono restituite le informazioni su tutte le impostazioni di configurazione di Chat persistente nell'ambito del sito. A tale scopo, vengono inclusi il parametro Filter e il valore di filtro "service:\*".

    Get-CsPersistentChatConfiguration -Filter "service:*"

## Esempio 4

Nell'esempio 4 vengono restituite informazioni su tutte le impostazioni di configurazione di Chat persistente in cui la cronologia chat predefinita è impostata su un valore maggiore di 30. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsPersistentChatConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione di Chat persistente. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà DefaultChatHistory è maggiore di (-gt) 30.

    Get-CsPersistentChatConfiguration | Where-Object {$_.DefaultChatHistory -gt 30}

## Esempio 5

Nell'esempio 5 viene illustrato come restituire le informazioni su tutte le impostazioni di configurazione di Chat persistente in cui non è stato definito l'URL di gestione delle chat room. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsPersistentChatConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione di Chat persistente. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona tutte le impostazioni in cui la proprietà RoomManagementUrl è uguale a un valore Null ($Null).

    Get-CsPersistentChatConfiguration | Where-Object {$_.RoomManagementUrl -eq $Null}

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Il servizio Chat persistente viene gestito in parte dalle impostazioni di configurazione di Chat persistente, che definiscono elementi quali il numero dei messaggi di chat precedentemente inseriti e immediatamente disponibili quando si accede a una chat room (cronologia di chat) o le dimensioni massime di un file che è possibile caricare o scaricare dal servizio. Queste impostazioni possono essere configurate nell'ambito globale o del sito oppure nell'ambito del servizio (ovvero è possibile disporre di una raccolta personalizzata di impostazioni assegnate a un singolo pool di Chat persistente).

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsPersistentChatConfiguration"}

**Pannello di controllo di Lync Server:** per visualizzare le informazioni di configurazione di Chat persistente nel Pannello di controllo di Lync Server, fare clic su **Chat persistente** e quindi su **Configurazione di Chat persistente**.

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
<td><p>Consente di utilizzare caratteri jolly per specificare la raccolta (o le raccolte) di impostazioni di configurazione di Chat persistente da restituire. Ad esempio, la sintassi seguente restituisce tutte le impostazioni configurate nell'ambito del servizio:</p>
<p>-Filter &quot;service:*&quot;</p>
<p>Non è possibile utilizzare i parametri Filter e Identity nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco delle impostazioni di configurazione di Chat persistente da restituire. Per restituire la raccolta globale, utilizzare la sintassi seguente:</p>
<p>-Identity &quot;global&quot;</p>
<p>Per restituire una raccolta di impostazioni configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>Per restituire una raccolta configurata nell'ambito del servizio, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;service:PersistentChatServer:atl-gc-001.litwareinc.com&quot;</p>
<p>Non è possibile utilizzare i caratteri jolly con il parametro Identity.</p>
<p>Se in un comando non viene incluso né il parametro Identity né il parametro Filter, il cmdlet <strong>Get-CsPersistentChatConfiguration</strong> restituirà informazioni su tutte le impostazioni di configurazione di Chat persistente in uso nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione di Chat persistente dalla replica locale dell'archivio di gestione centrale anziché direttamente da tale archivio.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsPersistentChatConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsPersistentChatConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsPersistentChatConfiguration](new-cspersistentchatconfiguration.md)  
[Remove-CsPersistentChatConfiguration](remove-cspersistentchatconfiguration.md)  
[Set-CsPersistentChatConfiguration](set-cspersistentchatconfiguration.md)

