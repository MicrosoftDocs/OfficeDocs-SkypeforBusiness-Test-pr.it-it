---
title: Set-CsArchivingServer
TOCTitle: Set-CsArchivingServer
ms:assetid: d4e51c14-34a6-4134-bb71-87bc2f11092d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398923(v=OCS.15)
ms:contentKeyID: 49302081
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsArchivingServer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di specificare un nuovo percorso di database per uno o più server di archiviazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsArchivingServer [-Identity <XdsGlobalRelativeIdentity>] [-ArchivingDatabase <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 modifica il percorso del database di archiviazione per il server di archiviazione ArchivingServer:atl-cs-001.litwareinc.com. In questo esempio il nuovo database si trova in ArchivingDatabase:atl-sql-001.litwareinc.com.

    Set-CsArchivingServer -Identity "ArchivingServer:atl-cs-001.litwareinc.com" -ArchivingDatabase "ArchivingDatabase:atl-sql-001.litwareinc.com"

## Descrizione dettagliata

I server di archiviazione consentono di salvare trascrizioni complete delle sessioni di messaggistica istantanea che vengono eseguite nell'organizzazione. In alcune organizzazioni può risultare utile disporre di copie delle sessioni di messaggistica istantanea. In altre organizzazioni in cui è necessario conservare le registrazioni di tutte le comunicazioni elettroniche può essere obbligatorio disporre delle copie delle sessioni di messaggistica istantanea.

Il server di archiviazione registra in un database di SQL Server la trascrizione di ogni sessione di messaggistica istantanea, oltre alle informazioni sulla data e l'ora in cui è avvenuta la sessione e sulle persone che vi hanno partecipato. Il percorso del database deve essere specificato durante l'installazione del server di archiviazione. Nella maggior parte dei casi non sarà necessario modificarlo. In caso tuttavia di un errore hardware o di un altro problema, è possibile far puntare il server di archiviazione a un nuovo database mediante il cmdlet **Set-CsArchivingServer**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsArchivingServer** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsArchivingServer"}

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
<td><p><em>ArchivingDatabase</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Posizione del servizio in cui si trova il nuovo database di archiviazione, ad esempio -ArchivingDatabase ArchivingDatabase:atl-sql-001.litwareinc.com. Quando si specifica il percorso del database, accertarsi di utilizzare la posizione del servizio e non il percorso SQL Server.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Posizione del servizio dell'istanza del server di archiviazione da modificare. Ad esempio: -Identity ArchivingServer:atl-cs-001.litwareinc.com. È possibile recuperare la posizione del servizio per tutti i server di archiviazione eseguendo questo comando:</p>
<p>Get-CsService –ArchivingServer | Select-Object Identity</p>
<p>È possibile omettere il prefisso &quot;ArchivingServer:&quot; quando si specifica un server di archiviazione, ad esempio -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p></p></td>
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

Nessuno. Il cmdlet **Set-CsArchivingServer** non accetta input inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CsArchivingServer** non restituisce alcun oggetto o valore. In realtà il cmdlet modifica le istanze dell'oggetto Microsoft.Rtc.Management.Xds.DisplayArchivingServer.

## Vedere anche

#### Ulteriori risorse

[Get-CsArchivingConfiguration](get-csarchivingconfiguration.md)

