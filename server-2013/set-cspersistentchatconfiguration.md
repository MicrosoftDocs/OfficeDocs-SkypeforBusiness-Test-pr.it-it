---
title: Set-CsPersistentChatConfiguration
TOCTitle: Set-CsPersistentChatConfiguration
ms:assetid: 97d23d2e-878c-4573-bfce-0ddddc5a190e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205122(v=OCS.15)
ms:contentKeyID: 49301399
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPersistentChatConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una raccolta esistente di impostazioni di configurazione di Chat persistente. Tali impostazioni vengono utilizzate per gestire il servizio Chat persistente e consentono ad esempio di specificare il numero massimo di utenti che possono partecipare a una chat room. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsPersistentChatConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsPersistentChatConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-DefaultChatHistory <Int16>] [-Force <SwitchParameter>] [-MaxFileSizeKB <UInt32>] [-ParticipantUpdateLimit <UInt32>] [-RoomManagementUrl <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 imposta su 100 la proprietà DefaultChatHistory delle impostazioni di configurazione globali di Chat persistente.

    Set-CsPersistentChatConfiguration -Identity "global" -DefaultChatHistory 100

## Esempio 2

Nell'esempio 2 la proprietà DefaultChatHistory viene impostata su 100 per tutte le impostazioni di configurazione di Chat persistente. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsPersistentChatConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione di Chat persistente definite nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsPersistentChatConfiguration**, che modifica la proprietà DefaultChatHistory per tutti gli elementi della raccolta.

    Get-CsPersistentChatConfiguration | Set-CsPersistentChatConfiguration -DefaultChatHistory 100

## Esempio 3

Nell'esempio 3 viene illustrato come modificare la proprietà DefaultChatHistory per tutte le impostazioni di configurazione di Chat persistente applicate nell'ambito del sito. A tale scopo, nel comando viene innanzitutto chiamato il cmdlet **Get-CsPersistentChatConfiguration** insieme al parametro Filter. Il valore di parametro "site:\*" circoscrive i dati restituiti limitandoli alle raccolte di impostazioni configurate nell'ambito del sito. Tali impostazioni vengono quindi inviate tramite pipe al cmdlet **Set-CsPersistentChatConfiguration**, che imposta su 100 la proprietà DefaultChatHistory di ogni raccolta di impostazioni.

    Get-CsPersistentChatConfiguration -Filter "site:*" | Set-CsPersistentChatConfiguration -DefaultChatHistory 100

## Esempio 4

Nell'esempio 4 viene modificata la proprietà DefaultChatHistory per qualsiasi raccolta di impostazioni di configurazione di Chat persistente in cui la cronologia chat predefinita attualmente è maggiore di 100. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsPersistentChatConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione di Chat persistente in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà DefaultChatHistory è maggiore di (-gt) 100. Tale raccolta filtrata viene a sua volta inviata tramite pipe al cmdlet **Set-CsPersistentChatConfiguration**, che seleziona ogni elemento della raccolta filtrata e imposta su 100 il valore della proprietà DefaultChatHistory.

    Get-CsPersistentChatConfiguration | Where-Object {$_.DefaultChatHistory -gt 100} | Set-CsPersistentChatConfiguration -DefaultChatHistory 100

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Il servizio Chat persistente viene gestito in parte dalle impostazioni di configurazione di Chat persistente, che definiscono elementi quali il numero dei messaggi di chat precedentemente inseriti e immediatamente disponibili quando si accede a una chat room (cronologia di chat) o le dimensioni massime di un file che è possibile caricare o scaricare dal servizio. Queste impostazioni possono essere configurate nell'ambito globale o del sito oppure nell'ambito del servizio (ovvero è possibile disporre di una raccolta personalizzata di impostazioni assegnate a un singolo pool di Chat persistente).

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPersistentChatConfiguration"}

**Pannello di controllo di Lync Server:** per modificare una raccolta esistente di impostazioni di configurazione di Chat persistente utilizzando il Pannello di controllo di Lync Server, fare clic su **Chat persistente**, su **Configurazione di Chat persistente** e quindi fare doppio clic sulla raccolta da modificare.

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DefaultChatHistory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int16</p></td>
<td><p>Numero predefinito di messaggi chat istantaneamente disponibili in una chat room. Questo valore rappresenta solo il numero di messaggi immediatamente disponibili e non il limite relativo al numero totale di messaggi che possono essere recuperati.</p>
<p>DefaultChatHistory può essere impostato su qualsiasi valore compreso tra 1 e 500 (inclusi). Il valore predefinito è 30.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco delle impostazioni di configurazione di Chat persistente da modificare. Per modificare una raccolta di impostazioni configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>Per modificare una raccolta configurata nell'ambito del servizio, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;service:PersistentChatServer:atl-gc-001.litwareinc.com&quot;</p>
<p>Per modificare la raccolta globale, utilizzare la sintassi seguente:</p>
<p>-Identity &quot;global&quot;</p>
<p>Se non si include il parametro Identity, il cmdlet <strong>Set-CsPersistentChatConfiguration</strong> modificherà automaticamente le impostazioni globali.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxFileSizeKB</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Dimensione massima, in kilobyte, di un file che può essere caricato o scaricato dal servizio Web. Il valore predefinito è 20000 KB.</p></td>
</tr>
<tr class="odd">
<td><p><em>ParticipantUpdateLimit</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Numero massimo di utenti che possono partecipare a una chat room prima che gli aggiornamenti dell'elenco dei partecipanti attivi vengano disabilitati. Il valore predefinito è 75.</p></td>
</tr>
<tr class="even">
<td><p><em>RoomManagementUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL della pagina Web che gli amministratori possono utilizzare per gestire le singole chat room.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Set-CsPersistentChatConfiguration** accetta istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatConfiguration inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsPersistentChatConfiguration** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsPersistentChatConfiguration](get-cspersistentchatconfiguration.md)  
[New-CsPersistentChatConfiguration](new-cspersistentchatconfiguration.md)  
[Remove-CsPersistentChatConfiguration](remove-cspersistentchatconfiguration.md)

