---
title: New-CsPersistentChatConfiguration
TOCTitle: New-CsPersistentChatConfiguration
ms:assetid: df83eebe-c20c-4e22-a5d4-1546a7f06e25
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205330(v=OCS.15)
ms:contentKeyID: 49302220
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPersistentChatConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta di impostazioni di configurazione di Chat persistente nell'ambito del sito o per utente. Tali impostazioni vengono utilizzate per gestire il servizio Chat persistente e consentono ad esempio di specificare il numero massimo di utenti che possono partecipare a una chat room. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    New-CsPersistentChatConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-DefaultChatHistory <Int16>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-MaxFileSizeKB <UInt32>] [-ParticipantUpdateLimit <UInt32>] [-RoomManagementUrl <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 crea un nuovo set di impostazioni di configurazione di Chat persistente applicate al sito Redmond. In questo esempio la proprietà ParticipantUpdateLimit è impostata su 100.

    New-CsPersistentChatConfiguration -Identity "site:Redmond" -ParticipantUpdateLimit 100

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Il servizio Chat persistente viene gestito in parte dalle impostazioni di configurazione di Chat persistente, che definiscono elementi quali il numero dei messaggi di chat precedentemente inseriti e immediatamente disponibili quando si accede a una chat room (cronologia di chat) o le dimensioni massime di un file che è possibile caricare o scaricare dal servizio. Queste impostazioni possono essere configurate nell'ambito globale o del sito oppure nell'ambito del servizio (ovvero è possibile disporre di una raccolta personalizzata di impostazioni assegnate a un singolo pool di Chat persistente).

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPersistentChatConfiguration"}

**Pannello di controllo di Lync Server:** Per creare una nuova raccolta di impostazioni di configurazione di Chat persistente utilizzando Pannello di controllo di Lync Server, fare clic su **Chat persistente**, **Configurazione di Chat persistente**, **Nuovo** e quindi su **Configurazione sito** o su **Configurazione pool**.

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
<td><p>Identificatore univoco per le nuove impostazioni di configurazione di Chat persistente create. Le nuove impostazioni di configurazione possono essere create con ambito di sito o di servizio (solo per il servizio Chat persistente Server). Per creare nuove impostazioni nell'ambito del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>Per creare nuove impostazioni nell'ambito del servizio, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;service:PersistentChatServer:atl-gc-001.litwarein.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di visualizzare una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultChatHistory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int16</p></td>
<td><p>Numero predefinito di messaggi di chat immediatamente disponibili in una chat room. Notare che questo valore rappresenta solo il numero di messaggi immediatamente disponibili, non pone un limite sulla quantità totale di messaggi che si possono recuperare.</p>
<p>DefaultChatHistory può essere impostato su qualsiasi valore da 1 a 500 (compresi). Il valore predefinito è 30.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxFileSizeKB</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Dimensione massima di un file (in kilobyte) che può essere caricato o scaricato dal servizio Web. Il valore predefinito è 20000 KB.</p></td>
</tr>
<tr class="odd">
<td><p><em>ParticipantUpdateLimit</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Numero massimo di utenti che possono partecipare a una chat room prima che vengano disabilitati gli aggiornamenti dell'elenco di partecipanti. Il valore predefinito è 75.</p></td>
</tr>
<tr class="even">
<td><p><em>RoomManagementUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL per la pagina Web che gli amministratori possono utilizzare per gestire singole chat room.</p></td>
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

Nessuno. Il cmdlet **New-CsPersistentChatConfiguration** non accetta l'input da pipeline.

## Tipi restituiti

Il cmdlet **New-CsPersistentChatConfiguration** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsPersistentChatConfiguration](get-cspersistentchatconfiguration.md)  
[Remove-CsPersistentChatConfiguration](remove-cspersistentchatconfiguration.md)  
[Set-CsPersistentChatConfiguration](set-cspersistentchatconfiguration.md)

