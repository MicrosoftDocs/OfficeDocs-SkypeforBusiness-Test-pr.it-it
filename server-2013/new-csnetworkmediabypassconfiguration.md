---
title: New-CsNetworkMediaBypassConfiguration
TOCTitle: New-CsNetworkMediaBypassConfiguration
ms:assetid: 24055ae5-7fc8-4ca5-9e65-ac3a1f17b405
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425718(v=OCS.15)
ms:contentKeyID: 49299939
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkMediaBypassConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea nuove impostazioni globali per il bypass multimediale. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsNetworkMediaBypassConfiguration [-AlwaysBypass <$true | $false>] [-BypassID <String>] [-Enabled <$true | $false>] [-EnableDefaultBypassID <$true | $false>] [-EnabledForAudioVideoConferences <$true | $false>] [-ExternalBypassMode <Off | ICE | Any>] [-InternalBypassMode <Off | ICE | Any>]

## Esempi

## ESEMPIO 1

I comandi di questo esempio abilitano il bypass multimediale e lo configurano per tentare sempre il bypass. La prima riga dell'esempio è una chiamata al cmdlet **New-CsNetworkMediaBypassConfiguration**. A questo cmdlet vengono passati due parametri, AlwaysBypass ed Enabled, impostandoli entrambi su True ($true). Con l'impostazione di Enabled su True viene abilitato il bypass multimediale, mentre impostando AlwaysBypass su True si garantisce il tentativo di applicare il bypass multimediale per tutte le chiamate. Con l'impostazione di questi due parametri viene automaticamente generato un valore per la proprietà BypassID. Il cmdlet **New-CsNetworkMediaBypassConfiguration** crea l'oggetto solo in memoria, pertanto l'oggetto viene assegnato alla variabile $a.

La configurazione del bypass multimediale viene memorizzata con le impostazioni di configurazione della rete. Di conseguenza, nella riga 2 dell'esempio vengono salvate le modifiche di configurazione del bypass multimediale apportate alla configurazione di rete chiamando il cmdlet **Set-CsNetworkConfiguration** e passando al parametro MediaBypassSettings l'oggetto di configurazione del bypass multimediale ($a) creato nella riga 1.

    $a = New-CsNetworkMediaBypassConfiguration -AlwaysBypass $true -Enabled $true
    Set-CsNetworkConfiguration -MediaBypassSettings $a

## ESEMPIO 2

Non esiste un cmdlet **Set-CsNetworkMediaBypassConfiguration** in Lync Server, quindi per modificare le impostazioni esistenti occorre creare una nuova configurazione (come mostrato nell'esempio 1) per sostituire la configurazione esistente, oppure è necessario modificare le impostazioni recuperando quelle esistenti, cambiandole e poi salvando le modifiche con il cmdlet **Set-CsNetworkConfiguration**. Con questo esempio viene dimostrata la disattivazione dell'opzione AlwaysBypass con quest'ultima possibilità.

Nella prima riga dell'esempio vengono recuperate le impostazioni di bypass multimediale esistenti. A tale scopo, viene chiamato il cmdlet **Get-CsNetworkConfiguration**. La chiamata a questo cmdlet si trova tra parentesi per garantire che il cmdlet venga completato prima che siano eseguite altre parti del comando. Il cmdlet **Get-CsNetworkConfiguration** recupera tutte le impostazioni per un'intera configurazione di rete. Poiché in questo caso sono rilevanti esclusivamente le impostazioni di bypass multimediale, è necessario specificare la proprietà MediaBypassSettings per recuperare solo queste impostazioni. Le impostazioni vengono assegnate alla variabile $a.

Nella riga 2 vengono modificate le impostazioni archiviate nella variabile $a assegnando il valore False ($false) alla proprietà AlwaysBypass. Nella riga 3 infine viene chiamato il cmdlet **Set-CsNetworkConfiguration**, passando al parametro MediaBypassSettings la variabile $a, che salva la modifica apportata nella proprietà AlwaysBypass.

    $a = (Get-CsNetworkConfiguration).MediaBypassSettings
    $a.AlwaysBypass = $false
    Set-CsNetworkConfiguration -MediaBypassSettings $a

## Descrizione dettagliata

Questo cmdlet consente di creare impostazioni globali per il bypass multimediale delle connessioni audio.

A differenza della maggior parte dei cmdlet di tipo New- in Lync Server, questo cmdlet non salva immediatamente la nuova configurazione, ma crea le impostazioni unicamente in memoria. L'oggetto creato da questo cmdlet deve essere salvato in una variabile e quindi assegnato alla proprietà MediaBypassSettings della configurazione di rete. Per informazioni dettagliate, vedere la sezione Esempi di questo argomento.

Le impostazioni create con questo cmdlet possono essere recuperate solo accedendo alla proprietà MediaBypassSettings della configurazione di rete globale. Per recuperare queste impostazioni, eseguire questo comando: (Get-CsNetworkConfiguration).MediaBypassSettings.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, il cmdlet **New-CsNetworkMediaBypassConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkMediaBypassConfiguration"}

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
<td><p><em>AlwaysBypass</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Impostando questo parametro su True viene effettuato un tentativo di bypass multimediale per tutte le chiamate.</p>
<p>Impostare il valore di questo parametro su True solo se il servizio Controllo di ammissione di chiamata non è implementato o è disabilitato. Impostare questo parametro su True solo per le distribuzioni in cui:</p>
<p>- Non è necessario il controllo della larghezza di banda.</p>
<p>- Non è necessaria una configurazione con granularità fine per determinare quando dovrebbe avvenire il bypass.</p>
<p>- Esiste la piena connettività tra gateway e client.</p>
<p>Se il parametro Enabled è impostato su True e AlwaysBypass è impostato su False, la logica di bypass utilizzerà i siti e le regioni di configurazione della rete per determinare quando è possibile il bypass.</p>
<p>Se si imposta AlwaysBypass su True ma non si imposta anche il valore del parametro Enabled su True, viene visualizzato un messaggio di avviso. L'impostazione Ignora sempre viene ignorata se l'opzione Abilitato è impostata su false.</p>
<p>Impostando sia AlwaysBypass sia Enabled su True viene generato automaticamente un ID di bypass che sarà memorizzato nella proprietà BypassID.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="even">
<td><p><em>BypassID</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>ID di bypass multimediale. Se il parametro AlwaysBypass è impostato su True e viene fornito un valore per questo parametro, il valore BypassID sarà associato a tutte le subnet. Se AlwaysBypass è False, il valore BypassID viene associato a tutte le subnet che non sono presenti nelle regioni e nei siti di configurazione della rete.</p>
<p>Questo ID deve essere nel formato di un GUID (ad esempio, 96f14dea-5170-429a-b92b-f1cb909c4bb6). Tuttavia, in genere non è necessario impostare o modificare questo parametro. Questo valore viene generato automaticamente quando Enabled è impostato su True e quando 1) AlwaysBypass è impostato su True o 2) il parametro EnableDefaultBypassID è impostato su True.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>L'impostazione di questo parametro su True consente di abilitare il bypass multimediale. A questo punto le decisioni di bypass saranno basate sul valore dell'impostazione AlwaysBypass, secondo quanto riportato di seguito:</p>
<p>- Se AlwaysBypass è True, il bypass viene tentato per tutte le chiamate.</p>
<p>- Se AlwaysBypass è False, utilizzare la regione e il sito di configurazione della rete per determinare se il bypass è possibile.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableDefaultBypassID</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Questo valore viene applicato solo se AlwaysBypass è impostato su False.</p>
<p>Impostando questo valore su True viene generato automaticamente un ID di bypass, che sarà memorizzato nella proprietà BypassID.</p>
<p>Questo parametro è utile quando esiste un core ben connesso a siti remoti che presentano collegamenti con larghezza di banda vincolata. L'amministratore deve definire solamente le subnet associate ai siti remoti attraverso le aree e i siti di configurazione di rete. Eventuali subnet associate al core non devono essere definite e tra queste subnet sarà tentato automaticamente il bypass.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnabledForAudioVideoConferences</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se deve essere utilizzato il bypass multimediale per le conferenze audio/video. Il valore predefinito è False ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalBypassMode</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>BypassModeEnumType</p></td>
<td><p>Riservato per utilizzi futuri. Il bypass multimediale esterno non è supportato in Lync Server.</p>
<p>Valore predefinito: Off</p></td>
</tr>
<tr class="odd">
<td><p><em>InternalBypassMode</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>BypassModeEnumType</p></td>
<td><p>Il valore di questo parametro stabilisce quando i client che si connettono dall'interno della rete dell'organizzazione possono tentare l'esecuzione del bypass multimediale. Se Enabled è impostato su True, questo valore viene automaticamente cambiato in Any. Altri valori di questo parametro sono riservati per l'uso in futuro.</p>
<p>Valore predefinito: Off</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Consente di creare un riferimento oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.MediaBypassSettingsType.

## Vedere anche

#### Ulteriori risorse

[Get-CsNetworkConfiguration](get-csnetworkconfiguration.md)  
[Set-CsNetworkConfiguration](set-csnetworkconfiguration.md)

