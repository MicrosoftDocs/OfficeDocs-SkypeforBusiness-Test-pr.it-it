---
title: Export-CsPersistentChatData
TOCTitle: Export-CsPersistentChatData
ms:assetid: f4855109-26e0-41b8-8a9f-890f8d892645
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205378(v=OCS.15)
ms:contentKeyID: 49302478
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Export-CsPersistentChatData

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Esporta dati da un database di Chat persistente. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Export-CsPersistentChatData [-FileName <String>] <COMMON PARAMETERS>

    Export-CsPersistentChatData [-AsBytes <SwitchParameter>] <COMMON PARAMETERS>

    COMMON PARAMETERS: -DBInstance <String> [-DBName <String>] [-DisableExportedNodes <SwitchParameter>] [-Level <User | Category | RoomDirectory | Content | All>] [-Report <String>] [-Scope <List>] [-StartDate <DateTime>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 esporta dati di Chat persistente dal database di Chat persistente posizionato nel server atl-sql-001.litwareinc.com. I dati esportati verranno archiviati nel file C:\\Logs\\PersistentChatData.zip. Poiché il parametro Level non è stato specificato, il cmdlet **Export-CsPersistentChatData** eseguirà un'esportazione completa delle informazioni di Chat persistente.

    Export-CsPersistentChatData -DBInstance "atl-sql-001.litwareinc.com\rtc" -FileName "C:\Logs\PersistentChatData.zip"

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Se attualmente si utilizza Lync Server 2010, è possibile eseguire la migrazione dell'implementazione di Group Chat corrente utilizzando il cmdlet **Export-CsPersistentChatData** per esportare le impostazioni di configurazione di Group Chat esistenti e quindi utilizzare il cmdlet **Import-CsPersistentChatData** per eseguire la migrazione delle informazioni in Lync Server 2013 e nel servizio Chat persistente. Si noti che il cmdlet **Export-CsPersistentChatData** consente di importare tutte le impostazioni e i dati di Group Chat o solo una parte di essi. È ad esempio possibile esportare e quindi importare le categorie e le chat room di Group Chat senza esportare tutto il contenuto associato a tali categorie e chat room.

Sebbene siano stati creati principalmente per la migrazione, i cmdlet **CsPersistentChatData** possono essere utilizzati anche per gestire i dati di Chat persistente in Lync Server 2013.

Per restituire un elenco di tutti i ruoli Controllo degli accessi in base al ruolo a cui è stato assegnato questo cmdlet, inclusi eventuali ruoli Controllo degli accessi in base al ruolo personalizzati creati dall'utente stesso, eseguire il comando seguente dal prompt dell'interfaccia della riga di comando Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Export-CsPersistentChatData"}

Pannello di controllo di Lync Server: le funzioni eseguite dal cmdlet **Export-CsPersistentChatData** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>DBInstance</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo dell'istanza di SQL Server in cui è posizionato il database di Chat persistente di Lync Server 2013. Ad esempio, la sintassi seguente specifica il database trovato nell'istanza del database RTC nel server atl-sql-001.litwareinc.com:</p>
<p>-DBInstance &quot;atl-sql-001.litwareinc.com\rtc&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>AsBytes</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce le informazioni di Chat persistente come matrice di byte. I dati restituiti devono quindi essere archiviati in una variabile per essere utilizzati dal cmdlet <strong>Import-CsPersistentChatData</strong>. Non è possibile utilizzare sia AsBytes che FileName nello stesso comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>DBName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome dell'istanza SQL del database di Chat persistente.</p></td>
</tr>
<tr class="even">
<td><p><em>DisableExportedNodes</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Quando è presente, tutte le chat room e le categorie esportate vengono disabilitate al completamento dell'esportazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>FileName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Percorso completo del file ZIP che il cmdlet <strong>Export-CsPersistentChatData</strong> creerà. Questo file conterrà i dati utente esportati. Ad esempio:</p>
<p>-FileName &quot;C:\Logs\PersistentChatData.zip&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Level</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Chat.Cmdlets.ExportLevel</p></td>
<td><p>Consente di specificare quali informazioni di Chat persistente verranno esportate. I valori consentiti sono:</p>
<p>* All</p>
<p>* User</p>
<p>* Category</p>
<p>* RoomDirectory</p>
<p>* Content</p>
<p>Il valore predefinito è All che indica che verranno esportate tutte le informazioni di Chat persistente.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Percorso completo del file di log creato quando viene eseguito il cmdlet. Ad esempio:</p>
<p>-Report &quot;C:\Logs\ExportPersistentChat.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Scope</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Collections.Generic.List</p></td>
<td><p>Consente di esportare dati per un set di categorie specificato (e le loro chat room corrispondenti). Per impostazione predefinita, vengono esportate tutte le categorie.</p></td>
</tr>
<tr class="odd">
<td><p><em>StartDate</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.DateTime</p></td>
<td><p>Data iniziale per il periodo di tempo per il quale si intende esportare il contenuto della chat room di Chat persistente. Ad esempio:</p>
<p>-StartDate &quot;1/1/2012&quot;</p>
<p>Questo parametro è valido solo quando Level è impostato su RoomDirectory.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Export-CsPersistentChatData** non accetta l'input da pipeline.

## Tipi restituiti

Il cmdlet **Export-CsPersistentChatData** crea file ZIP.

