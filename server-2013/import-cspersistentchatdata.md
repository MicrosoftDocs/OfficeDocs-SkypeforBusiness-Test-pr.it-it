---
title: Import-CsPersistentChatData
TOCTitle: Import-CsPersistentChatData
ms:assetid: 17151a25-5dea-498a-93d5-fed3da7d3fa5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204709(v=OCS.15)
ms:contentKeyID: 49299803
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsPersistentChatData

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente agli amministratori di importare dati esportati da un database di Group Chat di Microsoft Lync Server 2010 in un database di Chat persistente di Lync Server 2013. Questi dati devono essere stati precedentemente esportati dal database di Group Chat utilizzando il cmdlet **Export-CsPersistentChatData**. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Import-CsPersistentChatData -FileName <String> <COMMON PARAMETERS>

    Import-CsPersistentChatData -ByteInput <Byte[]> <COMMON PARAMETERS>

    COMMON PARAMETERS: -DBInstance <String> [-Confirm [<SwitchParameter>]] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 legge i dati esportati di Chat persistente dal file C:\\Logs\\PersistentChatExport.xml e quindi li aggiunge nel database di Chat persistente atl-sql-001.litwareinc.com\\rtc, dove "atl-sql-001.litwareinc.com" è il nome di dominio completo del computer SQL Server e "rtc" è l'istanza del database di SQL Server.

    Import-CsPersistentChatData -DBInstance "atl-sql-001.litwareinc.com\rtc" -FileName "C:\Logs\PersistentChatExport.zip"

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Se attualmente si esegue Lync Server 2010, è possibile effettuare la migrazione dell'implementazione di Group Chat corrente utilizzando il cmdlet **Export-CsPersistentChatData** per esportare le impostazioni di configurazione di Group Chat esistenti e quindi utilizzare il cmdlet **Import-CsPersistentChatData** per eseguire la migrazione delle informazioni in Lync Server 2013 e nel servizio Chat persistente. Si noti che il cmdlet **Export-CsPersistentChatData** consente di importare tutte le impostazioni e i dati di Group Chat o solo una parte di essi. È ad esempio possibile esportare e quindi importare le categorie e le chat room di Group Chat senza esportare tutto il contenuto associato a tali categorie e chat room.

Sebbene siano stati creati principalmente per la migrazione, i cmdlet **CsPersistentChatData** possono essere utilizzati anche per gestire i dati di Chat persistente in Lync Server 2013.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsPersistentChatData"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Import-CsPersistentChatData** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>ByteInput</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Byte[]</p></td>
<td><p>Se si specifica questo parametro, i dati vengono importati come matrice di byte anziché come file XML.</p></td>
</tr>
<tr class="even">
<td><p><em>DBInstance</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo e nome dell'istanza di SQL Server in cui si trova il database di Chat persistente di Lync Server 2013. La sintassi seguente ad esempio specifica il database contenuto nell'istanza del database RTC nel server atl-sql-001.litwareinc.com:</p>
<p>-DBInstance &quot;atl-sql-001.litwareinc.com\rtc&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>FileName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Percorso completo del file XML da importare, ad esempio:</p>
<p>-FileName &quot;C:\Logs\PersistentChatExport.xml&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet, ad esempio:</p>
<p>-Report &quot;C:\Logs\PersistentChatExport.html&quot;</p>
<p>Se il file esiste già, viene sovrascritto durante l'esecuzione del cmdlet.</p></td>
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

Nessuno. Il cmdlet **Import-CsPersistentChatData** non accetta input da pipeline.

## Tipi restituiti

Nessuno.

