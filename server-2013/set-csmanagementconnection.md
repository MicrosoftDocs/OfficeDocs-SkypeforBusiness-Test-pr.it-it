---
title: Set-CsManagementConnection
TOCTitle: Set-CsManagementConnection
ms:assetid: f7cf19ba-6c56-4f74-9757-843e1ca0c9a1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413045(v=OCS.15)
ms:contentKeyID: 49302506
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsManagementConnection

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica la connessione di gestione all'archivio di gestione centrale. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsManagementConnection -Connection <String> -StoreProvider <FileSystem | Sql | Memory> [-Confirm [<SwitchParameter>]] [-EnableCaching <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando indicato nell'esempio 1 consente di modificare la connessione alla gestione eseguita all'istanza di SQL Server denominata rtcbackup sul computer atl-sql-001.litwareinc.com.

    Set-CsManagementConnection -StoreProvider Sql -Connection "atl-sql-001.litwareinc.com\rtcbackup"

## ESEMPIO 2

Nell'esempio 2, la connessione alla gestione era impostata sul file system ed, in particolare, sulla cartella C:\\TestTopology in un computer locale.

    Set-CsManagementConnection -StoreProvider FileSystem -Connection "C:\TestTopology"

## Descrizione dettagliata

I dati di configurazione di Lync Server sono archiviati nell'archivio di gestione centrale. È pertanto fondamentale che Windows PowerShell e i servizi di replica di gestione siano in grado di individuare questo database. Quando si installa Lync Server, in Servizi di dominio Active Directory viene creato un punto di controllo del servizio che fornisce informazioni sulla posizione di tale database. I computer in genere utilizzano questo punto di controllo del servizio per connettersi all'archivio di gestione centrale. Per visualizzare i dettagli alla base della connessione, ad esempio il computer in cui è in esecuzione l'archivio di gestione centrale e le informazioni sulla connessione SQL Server a tale archivio, è sufficiente eseguire il cmdlet **Get-CsManagementConnection**.

In linea di massima, dopo aver eseguito la connessione alla gestione non è necessario modificarla. In caso di problemi hardware o software, potrebbe tuttavia essere necessario utilizzare temporaneamente un'altra connessione. È ad esempio possibile configurare un computer per funzionare dalla replica locale. Il cmdlet **Set-CsManagementConnection** consente di fornire una nuova posizione per l'archivio di gestione centrale.

Tutte le modifiche apportate a Lync Server durante l'utilizzo di una connessione di gestione temporanea verranno rimosse non appena verrà ripristinata la connessione originale. Per effettuare tale ripristino, è possibile eseguire il cmdlet **Remove-CsManagementConnection**. Si supponga, ad esempio, di utilizzare temporaneamente il file system come provider di archivio, cambiando connessione di gestione e creando quindi diversi nuovi criteri vocali, per ognuno dei quali verranno create istanze come file XML. Ripristinando la connessione di gestione originale, questi nuovi criteri vocali verranno rimossi, in quanto non sono mai stati registrati nell'archivio di gestione centrale attualmente in uso.

Tenere inoltre presente che tutte le modifiche apportate eseguendo questo cmdlet hanno effetto solo sul computer locale. Non è pertanto possibile utilizzare il cmdlet **Set-CsManagementConnection** per cambiare la connessione di gestione in altri computer.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsManagementConnection** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins.

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
<td><p><em>Connection</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Le informazioni sulla posizione per l'istanza di SQL Server o la cartella del file system utilizzata come connessione di gestione.</p>
<p>Ad esempio, se la nuova connessione di gestione viene effettuata all'istanza di SQL Server denominata rtcbackup nel computer atl-sql-001.litwareinc.com, utilizzare la seguente sintassi: -Connection &quot;atl-sql-001.litwareinc.com\rtcbackup&quot;.</p>
<p>Se si desidera creare una connessione alla gestione per la cartella C:\TestTopology, utilizzare la seguente sintassi: -Connection &quot;C:\TestTopology&quot;. Se la cartella non esiste, verrà creata dal cmdlet <strong>Set-CsManagementConnection</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>StoreProvider</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Store.StoreProvider</p></td>
<td><p>Indica il tipo di archivio back-end usato per le informazioni di configurazione. Per archiviare i dati di configurazione in SQL Server, impostare StoreProvider nel modo seguente: -StoreProvider Sql. Per archiviare i dati di configurazione nel file system, usare la seguente sintassi: -StoreProvider FileSystem. Non modificare la proprietà StoreProvider, a meno che non si ricevano istruzioni in merito dal personale di supporto Microsoft.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableCaching</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Quando è impostato su True ($True), è abilitata la memorizzazione nella cache per la connessione di gestione.</p></td>
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

Nessuno. Il cmdlet **Set-CsManagementConnection** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Set-CsManagementConnection** non restituisce un valore o un oggetto. In realtà il cmdlet configura le istanze dell'oggetto Microsoft.Rtc.Management.Store.StoreProvider.

## Vedere anche

#### Ulteriori risorse

[Get-CsManagementConnection](get-csmanagementconnection.md)  
[Remove-CsManagementConnection](remove-csmanagementconnection.md)  
[Set-CsConfigurationStoreLocation](set-csconfigurationstorelocation.md)

