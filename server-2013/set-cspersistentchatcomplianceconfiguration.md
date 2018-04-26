---
title: Set-CsPersistentChatComplianceConfiguration
TOCTitle: Set-CsPersistentChatComplianceConfiguration
ms:assetid: 615625f8-574a-4832-8d3f-26721cd124d8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204949(v=OCS.15)
ms:contentKeyID: 49300745
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPersistentChatComplianceConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una raccolta esistente di impostazioni di configurazione della conformità di Chat persistente. La conformità di Chat persistente consente agli amministratori di gestire un archivio di elementi e attività di Chat persistente, tra cui nuovi messaggi, nuovi eventi, ad esempio un utente che accede a una chat o ne esce, caricamenti e download di file e ricerche nella cronologia di chat. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsPersistentChatComplianceConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsPersistentChatComplianceConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AdapterName <String>] [-AdapterOutputDirectory <String>] [-AdapterType <String>] [-AddChatRoomDetails <$true | $false>] [-AddUserDetails <$true | $false>] [-Confirm [<SwitchParameter>]] [-CreateFileAttachmentsManifest <$true | $false>] [-CustomConfiguration <String>] [-Force <SwitchParameter>] [-OneChatRoomPerOutputFile <$true | $false>] [-RunInterval <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Nell'esempio 1 la proprietà RunInterval della raccolta globale di impostazioni di configurazione della conformità di Chat persistente viene impostata su 10 minuti: 00 ore : 10 minuti : 00 secondi.

    Set-CsPersistentChatComplianceConfiguration -Identity "global" -RunInterval "00:10:00"

## Esempio 2

Nell'esempio 2 la proprietà RunInterval di tutte le impostazioni di configurazione della conformità di Chat persistente attualmente in uso nell'organizzazione viene impostata su 10 minuti. A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsPersistentChatComplianceConfiguration** senza parametri per restituire una raccolta di tutte le impostazioni di conformità. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsPersistentChatComplianceConfiguration**, che modifica il valore della proprietà RunInterval di ogni elemento della raccolta impostandolo su 10 minuti.

    Get-CsPersistentChatComplianceConfiguration | Set-CsPersistentChatComplianceConfiguration  -RunInterval "00:10:00"

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Molte organizzazioni, ad esempio organizzazioni che operano nel settore sanitario o finanziario, sono tenute a conservare archivi di tutte le comunicazioni elettroniche, incluse le eventuali conversazioni effettuate utilizzando il servizio Chat persistente. Lync Server consente di creare un database di conformità separato contenente un archivio dettagliato di tutto ciò che si verifica nelle chat room di Chat persistente. La conformità di Chat persistente può essere abilitata o disabilitata nell'ambito del sito o del servizio, ovvero può essere abilitata o disabilitata per un pool di Chat persistente specifico. La conformità di Chat persistente inoltre può essere gestita solo utilizzando l'interfaccia della riga di comando Windows PowerShell. Nel Pannello di controllo di Lync Server 2013 non sono disponibili opzioni per la gestione della conformità di Chat persistente.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli del controllo di accesso basato sui ruoli creati personalmente), al prompt di Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPersistentChatComplianceConfiguration"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Set-CsPersistentChatComplianceConfiguration** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>AdapterName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Nome degli adattatori di Chat persistente. Gli adattatori sono prodotti di terze parti in grado di convertire in un formato specifico i dati inclusi nel database di conformità.</p></td>
</tr>
<tr class="even">
<td><p><em>AdapterOutputDirectory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Percorso completo della cartella in cui sono archiviati i dati dell'adattatore. È necessario disporre di una cartella separata per ogni adattatore.</p></td>
</tr>
<tr class="odd">
<td><p><em>AdapterType</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Specifica il nome di dominio completo di un tipo gestito .NET che implementa l'interfaccia Microsoft.Rtc.Internal.Chat.Server.Compliance.IComplianceAdapter. Questo adattatore viene fornito da terze parti o può essere impostato sull'adattatore XML interno &quot;Microsoft.Rtc.Internal.Chat.Server.Compliance.XmlAdapter.compliance&quot;.</p>
<p>Se non si specifica un tipo di adattatore, Chat persistente non salverà i dati di conformità.</p></td>
</tr>
<tr class="even">
<td><p><em>AddChatRoomDetails</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se impostato su True, vengono forniti all'adattatore dettagli aggiuntivi su ogni chat room. In questo modo è possibile che le dimensioni dei dati di conformità aumentino in modo significativo.</p>
<p>Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>AddUserDetails</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se impostato su True, vengono forniti all'adattatore dettagli aggiuntivi su ogni utente di chat room. In questo modo è possibile che le dimensioni dei dati di conformità aumentino in modo significativo.</p>
<p>Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>CreateFileAttachmentsManifest</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se impostato su True, verranno creati file di output aggiuntivi per tenere traccia dei trasferimenti di file all'interno delle chat room. Tali file hanno estensione ATTACH e vengono copiati nel percorso specificato da AdapterOutputDirectory.</p></td>
</tr>
<tr class="even">
<td><p><em>CustomConfiguration</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Script di trasformazione XSLT che consente a Chat persistente di salvare i dati di conformità in un formato personalizzato progettato personalmente.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>XdsIdentity</p></td>
<td><p>Identificatore univoco delle impostazioni di conformità di Chat persistente da modificare. Per modificare la raccolta globale, utilizzare la sintassi seguente:</p>
<p>-Identity &quot;global&quot;</p>
<p>Per modificare una raccolta di impostazioni configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>Per modificare una raccolta configurata nell'ambito del servizio, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;service:PersistentChatServer:atl-gc-001.litwareinc.com&quot;</p>
<p>Se questo parametro non viene incluso, il cmdlet <strong>Set-CsPersistentChatComplianceConfiguration</strong> modificherà la raccolta globale.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSObject</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>OneChatRoomPerOutputFile</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se impostato su True, vengono creati rapporti separati per ogni chat room. Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>RunInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>TimeSpan</p></td>
<td><p>Intervallo di tempo che il server attende prima di generare il file di output successivo. Il parametro RunInterval deve essere specificato nel formato giorni.ore:minuti:secondi. Ad esempio, per specificare un intervallo di 15 minuti (valore predefinito), utilizzare la sintassi seguente:</p>
<p>-RunInterval 00:15:00</p>
<p>Il parametro RunInterval può essere impostato su un valore compreso tra 1 minuto (00:01.00) e 30 giorni (30.00:00:00), estremi inclusi.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Set-CsPersistentChatComplianceConfiguration** accetta istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatComplianceConfiguration inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsPersistentChatComplianceConfiguration** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatComplianceConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsPersistentChatComplianceConfiguration](get-cspersistentchatcomplianceconfiguration.md)  
[New-CsPersistentChatComplianceConfiguration](new-cspersistentchatcomplianceconfiguration.md)  
[Remove-CsPersistentChatComplianceConfiguration](remove-cspersistentchatcomplianceconfiguration.md)

