---
title: New-CsPersistentChatComplianceConfiguration
TOCTitle: New-CsPersistentChatComplianceConfiguration
ms:assetid: a61b76a9-0e2b-4f64-b2fa-cddadc15451c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205163(v=OCS.15)
ms:contentKeyID: 49301570
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsPersistentChatComplianceConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta di impostazioni di configurazione della conformità di Chat persistente nell'ambito del sito o del servizio. La conformità di Chat persistente consente agli amministratori di gestire un archivio di elementi e attività di Chat persistente, tra cui nuovi messaggi, nuovi eventi, ad esempio un utente che accede a una chat o ne esce, caricamenti e download di file e ricerche nella cronologia di chat. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    New-CsPersistentChatComplianceConfiguration -Identity <XdsIdentity> [-AdapterName <String>] [-AdapterOutputDirectory <String>] [-AdapterType <String>] [-AddChatRoomDetails <$true | $false>] [-AddUserDetails <$true | $false>] [-Confirm [<SwitchParameter>]] [-CreateFileAttachmentsManifest <$true | $false>] [-CustomConfiguration <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-OneChatRoomPerOutputFile <$true | $false>] [-RunInterval <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 crea una nuova raccolta di impostazioni di configurazione della conformità di Chat persistente per il sito Redmond. In questo esempio le proprietà AddUserDetails e AddChatRoomDetails vengono entrambe impostate su True ($True).

    New-CsPersistentChatComplianceConfiguration -Identity "site:Redmond" -AddUserDetails $True -AddChatRoomDetails $True

## Esempio 2

Anche nell'esempio 2 viene illustrato come creare una nuova raccolta di impostazioni di configurazione della conformità di Chat persistente per il sito Redmond. In questo esempio la proprietà RunInterval viene impostata su 30 minuti (00 ore : 30 minuti : 00 secondi).

    New-CsPersistentChatComplianceConfiguration -Identity "site:Redmond" -RunInterval "00:30:00"

## Descrizione dettagliata

Il servizio Chat persistente, che sostituisce il servizio Group Chat utilizzato in Microsoft Lync Server 2010, offre alle organizzazioni funzionalità di messaggistica e collaborazione simili a quelle disponibili nei forum di discussione su Internet. Gli utenti possono scambiarsi messaggi in tempo reale, ma possono anche rivedere le conversazioni e riavviarle in qualsiasi momento. Le conversazioni possono basarsi su argomenti specifici ed essere disponibili per chiunque o solo per un insieme selezionato di utenti. Analogamente, è possibile configurare singole chat room in modo che i messaggi possano essere inseriti da qualsiasi utente o solo da relatori designati.

Molte organizzazioni, ad esempio organizzazioni che operano nel settore sanitario o finanziario, sono tenute a conservare archivi di tutte le comunicazioni elettroniche, incluse le eventuali conversazioni effettuate utilizzando il servizio Chat persistente. Lync Server 2013 consente di creare un database di conformità separato contenente un archivio dettagliato di tutto ciò che si verifica nelle chat room di Chat persistente. La conformità di Chat persistente può essere abilitata o disabilitata nell'ambito del sito o del servizio, ovvero può essere abilitata o disabilitata per un pool di Chat persistente specifico. La conformità di Chat persistente inoltre può essere gestita solo utilizzando l'interfaccia della riga di comando Windows PowerShell. Nel Pannello di controllo di Lync Server 2013 non sono disponibili opzioni per la gestione della conformità di Chat persistente.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsPersistentChatComplianceConfiguration"}

Pannello di controllo di Lync Server: le funzioni eseguite dal cmdlet **New-CsPersistentChatComplianceConfiguration** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>XdsIdentity</p></td>
<td><p>Identificatore univoco delle nuove impostazioni della conformità di Chat persistente da creare. Le nuove impostazioni di conformità possono essere create nell'ambito del sito o del servizio (solo per il servizio del server Chat persistente). Per creare nuove impostazioni nell'ambito del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>Per creare nuove impostazioni nell'ambito del servizio, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;service:PersistentChatServer:atl-gc-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>AdapterName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Nome degli adattatori di Chat persistente utilizzati dalle impostazioni di conformità. Gli adattatori sono prodotti di terze parti in grado di convertire in un formato specifico i dati inclusi nel database di conformità.</p></td>
</tr>
<tr class="odd">
<td><p><em>AdapterOutputDirectory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Percorso completo della cartella in cui sono archiviati i dati dell'adattatore. È necessario disporre di una cartella separata per ogni adattatore.</p></td>
</tr>
<tr class="even">
<td><p><em>AdapterType</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Specifica il nome di dominio completo di un tipo gestito .NET che implementa l'interfaccia Microsoft.Rtc.Internal.Chat.Server.Compliance.IComplianceAdapter. Questo adattatore viene fornito da terze parti o può essere impostato sull'adattatore XML interno &quot;Microsoft.Rtc.Internal.Chat.Server.Compliance.XmlAdapter.compliance&quot;.</p>
<p>Se non si specifica un tipo di adattatore, Chat persistente non salverà i dati di conformità.</p></td>
</tr>
<tr class="odd">
<td><p><em>AddChatRoomDetails</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se impostato su True, vengono forniti all'adattatore dettagli aggiuntivi su ogni chat room. In questo modo è possibile che le dimensioni dei dati di conformità aumentino in modo significativo.</p>
<p>Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>AddUserDetails</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se impostato su True, vengono forniti all'adattatore dettagli aggiuntivi su ogni utente di chat room. In questo modo è possibile che le dimensioni dei dati di conformità aumentino in modo significativo.</p>
<p>Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>CreateFileAttachmentsManifest</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se impostato su True, verranno creati file di output aggiuntivi per tenere traccia dei trasferimenti di file all'interno delle chat room. Tali file hanno estensione ATTACH e vengono copiati nel percorso specificato da AdapterOutputDirectory.</p></td>
</tr>
<tr class="odd">
<td><p><em>CustomConfiguration</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Script di trasformazione XSLT che consente a Chat persistente di salvare i dati di conformità in un formato personalizzato progettato personalmente.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
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
<td><p>Intervallo di tempo che il server attende prima di generare il file di output successivo. Il parametro RunInterval deve essere specificato nel formato giorni.ore:minuti:secondi. Ad esempio, per specificare un intervallo di 30 minuti (valore predefinito), utilizzare la sintassi seguente:</p>
<p>-RunInterval 00:30:00</p>
<p>Il parametro RunInterval può essere impostato su qualsiasi valore compreso tra 1 minuto (00:01.00) e 30 giorni (30.00:00:00) inclusi. Il valore predefinito è 15 minuti (00:15:00).</p></td>
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

Nessuno. Il cmdlet **New-CsPersistentChatComplianceConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **New-CsPersistentChatComplianceConfiguration** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.PersistentChat.PersistentChatComplianceConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsPersistentChatComplianceConfiguration](get-cspersistentchatcomplianceconfiguration.md)  
[Remove-CsPersistentChatComplianceConfiguration](remove-cspersistentchatcomplianceconfiguration.md)  
[Set-CsPersistentChatComplianceConfiguration](set-cspersistentchatcomplianceconfiguration.md)

