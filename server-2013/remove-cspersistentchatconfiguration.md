---
title: Remove-CsPersistentChatConfiguration
TOCTitle: Remove-CsPersistentChatConfiguration
ms:assetid: 5b71b66b-9b9b-4833-94b8-528260cd7589
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204927(v=OCS.15)
ms:contentKeyID: 49300657
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsPersistentChatConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una raccolta esistente di impostazioni di configurazione di Chat persistente. Tali impostazioni vengono utilizzate per gestire il servizio Chat persistente e consentono ad esempio di specificare il numero massimo di utenti che possono partecipare a una chat room. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Remove-CsPersistentChatConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 elimina le impostazioni di configurazione di Chat persistente per il sito Redmond.

    Remove-CsPersistentChatConfiguration -Identity "site:Redmond"

## Esempio 2

Nell'esempio 2 vengono rimosse tutte le impostazioni di configurazione di Chat persistente applicate nell'ambito del sito. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsPersistentChatConfiguration** e il parametro -Filter. Il valore di filtro "site:\*" restituisce solo i dati relativi alle impostazioni applicate nell'ambito del sito. Queste impostazioni vengono quindi inviate tramite pipe al cmdlet **Remove-CsPersistentChatConfiguration**, che elimina tutte le impostazioni applicate nell'ambito del sito.

    Get-CsPersistentChatConfiguration -Filter "site:*" | Remove-CsPersistentChatConfiguration

## Esempio 3

Nell'esempio 3 vengono eliminate tutte le impostazioni di configurazione di Chat persistente in cui la cronologia delle chat predefinita è impostata su un valore maggiore di 30. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsPersistentChatConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione di Chat persistente. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà DefaultChatHistory è impostata su un valore maggiore di (-gt) 30. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsPersistentChatConfiguration**, che elimina ogni elemento della raccolta filtrata.

    Get-CsPersistentChatConfiguration | Where-Object {$_.DefaultChatHistory -gt 30} | Remove-CsPersistentChatConfiguration

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Il servizio Chat persistente viene gestito in parte dalle impostazioni di configurazione di Chat persistente, che definiscono elementi quali il numero dei messaggi di chat precedentemente inseriti e immediatamente disponibili quando si accede a una chat room (cronologia di chat) o le dimensioni massime di un file che è possibile caricare o scaricare dal servizio. Queste impostazioni possono essere configurate nell'ambito globale o del sito oppure nell'ambito del servizio (ovvero è possibile disporre di una raccolta personalizzata di impostazioni assegnate a un singolo pool di Chat persistente).

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli del controllo di accesso basato sui ruoli creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPersistentChatConfiguration"}

**Pannello di controllo di Lync Server:** per rimuovere una raccolta di impostazioni di configurazione di Chat persistente utilizzando il Pannello di controllo di Lync Server, fare clic su **Chat persistente** e quindi su **Configurazione di Chat persistente**. Selezionare la raccolta da rimuovere, fare clic su **Modifica** e quindi su **Elimina**.

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
<td><p>Identificatore univoco delle impostazioni di configurazione di Chat persistente da rimuovere. Per rimuovere una raccolta di impostazioni configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>Per rimuovere una raccolta configurata nell'ambito del servizio, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;service:PersistentChatServer:atl-gc-001.litwareinc.com&quot;</p>
<p>Si noti che non è possibile utilizzare i caratteri jolly con il parametro Identity.</p>
<p>È inoltre possibile eseguire il cmdlet <strong>Remove-CsPersistentChatConfiguration</strong> per la raccolta di impostazioni globali. In questo caso tuttavia la raccolta globale non verrà rimossa. Verranno invece reimpostate sui valori predefiniti tutte le proprietà incluse nella raccolta.</p></td>
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

Il cmdlet **Remove-CsPersistentChatConfiguration** accetta istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatConfiguration inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsPersistentChatConfiguration** invece elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsPersistentChatConfiguration](get-cspersistentchatconfiguration.md)  
[New-CsPersistentChatConfiguration](new-cspersistentchatconfiguration.md)  
[Set-CsPersistentChatConfiguration](set-cspersistentchatconfiguration.md)

