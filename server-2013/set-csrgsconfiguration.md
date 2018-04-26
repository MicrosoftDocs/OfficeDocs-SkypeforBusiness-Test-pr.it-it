---
title: Set-CsRgsConfiguration
TOCTitle: Set-CsRgsConfiguration
ms:assetid: 259cec4c-0152-4c8f-8aa6-51cefc1b55c9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425728(v=OCS.15)
ms:contentKeyID: 49299962
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsRgsConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica le impostazioni di configurazione per l'applicazione Response Group. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsRgsConfiguration -Identity <RgsIdentity> [-AgentRingbackGracePeriod <Int16>] [-DefaultMusicOnHoldFile <AudioFile>] [-DisableCallContext <$true | $false>] <COMMON PARAMETERS>

    Set-CsRgsConfiguration -Instance <ServiceSettings> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 modifica la proprietà AgentRingbackGracePeriod per le impostazioni di configurazione dell'applicazione Response Group trovate nel servizio ApplicationServer:atl-cs-001.litwareinc.com. In questo esempio, AgentRingbackGracePeriod è impostato su 30 secondi.

    Set-CsRgsConfiguration -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -AgentRingbackGracePeriod 30

## ESEMPIO 2

Nell'esempio 2 viene modificato il valore AgentRingbackGracePeriod per tutte le impostazioni di configurazione di Response Group presenti nell'organizzazione. A tale scopo, nel comando vengono innanzitutto utilizzati il cmdlet **Get-CsService** e il parametro ApplicationServer per restituire le informazioni relative a tutti i computer dell'organizzazione in cui è in esecuzione il Servizio applicazione. La raccolta restituita viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i computer la cui proprietà Applications contiene l'applicazione "urn:application:RGS". Tale valore indica che l'applicazione Response Group è in esecuzione nel server.

Tali computer vengono quindi inviati tramite pipe al cmdlet **ForEach-Object**. **ForEach-Object** individua i singoli computer della raccolta e utilizza **Set-CsRgsConfiguration** per impostare su 30 secondi il parametro AgentRingbackGracePeriod delle impostazioni di configurazione di Response Group del computer.

    Get-CsService -ApplicationServer | Where-Object {$_.Applications -contains "urn:application:RGS"} | ForEach-Object {Set-CsRgsConfiguration -Identity $_.Identity -AgentRingbackGracePeriod 30}

## ESEMPIO 3

I comandi mostrati nell'esempio 3 importano un file audio (C:\\Media\\WhileYouWait.wav) e quindi assegnano il file alla proprietà DefaultMusicOnHoldFile. Per eseguire questa attività, nel primo comando viene utilizzato **Import-CsRgsAudioFile** per importare il file audio nell'applicazione Response Group trovata in ApplicationServer:atl-cs-001.litwareinc.com. Oltre al parametro Identity (che specifica la posizione del servizio), viene utilizzato il parametro FileName per specificare il nome del file da importare.

Ugualmente importante è il parametro Content, che viene utilizzato per importare il file audio. L'importazione di file viene eseguita chiamando il cmdlet **Get-Content** seguito dal percorso del file da importare. **Get-Content** richiede inoltre di impostare il tipo di codifica su byte e ReadCount su 0. L'impostazione di ReadCount su 0 garantisce che l'intero file venga letto in una singola operazione. Il file importato viene quindi archiviato in una variabile denominata $x.

Dopo che è stato importato il file, viene chiamato **Set-CsRgsConfiguration** per impostare la proprietà DefaultMusicOnHoldFile sul file audio archiviato in $x.

    $x = Import-CsRgsAudioFile -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -FileName "WhileYouWait.wav" -Content (Get-Content C:\Media\WhileYouWait.wav -Encoding byte -ReadCount 0)
    
    Set-CsRgsConfiguration -Identity "service:ApplicationServer:atl-cs-001.litwareinc.com" -DefaultMusicOnHoldFile $x

## Descrizione dettagliata

L'applicazione Response Group consente di instradare automaticamente le chiamate telefoniche a entità come il supporto tecnico o la linea del servizio clienti. Quando qualcuno chiama un numero di telefono designato, la chiamata può essere instradata automaticamente all'insieme appropriato di agenti di Response Group. In alternativa, la chiamata può essere instradata a una coda del sistema IVR (Interactive Voice Response). In questa coda potrebbe essere posta una serie di domande (ad esempio, "Sta chiamando per un ordine ﻿in corso?") e quindi il chiamante, in base alle risposte date, potrebbe ottenere le informazioni desiderate o essere instradato a un agente di Response Group.

Il cmdlet **Set-CsRgsConfiguration** consente di modificare le proprietà di un'istanza dell'applicazione Response Group.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsRgsConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsRgsConfiguration"}

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
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>Nome del servizio che ospita le impostazioni di configurazione di Response Group. Ad esempio: -Identity &quot;service:ApplicationServer:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.ServiceSettings</p></td>
<td><p>Riferimento oggetto per le impostazioni di configurazione di Response Group Service da modificare. Un riferimento oggetto in genere viene recuperato utilizzando il cmdlet <strong>Get-CsRgsConfiguration</strong> e assegnando il valore restituito a una variabile. Questo comando ad esempio restituisce un riferimento oggetto alle impostazioni di configurazione trovate nel servizio ApplicationServer:atl-cs-001.litwareinc.com e archivia tale riferimento in una variabile denominata $x:</p>
<p>$x = Get-CsRgsConfiguration -Identity service:ApplicationServer:atl-cs-001.litwareinc.com</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>AgentRingbackGracePeriod</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int16</p></td>
<td><p>Se un agente rifiuta una chiamata, l'AgentRingbackGracePeriod rappresenta il tempo (in secondi) che deve trascorrere prima che la chiamata ritorni allo stesso agente. Il periodo di tolleranza può essere impostato su un valore intero tra 30 e 600 secondi (10 minuti) inclusi. Il valore predefinito è 60 secondi.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultMusicOnHoldFile</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.AudioFile</p></td>
<td><p>Rappresenta la musica che, per impostazione predefinita, sarà riprodotta ogni volta che il chiamante sarà lasciato in attesa. La musica predefinita viene riprodotta se un flusso di lavoro di Response Group non ha definito una musica specifica per l'attesa.</p>
<p>La proprietà DefaultMusicOnHoldFile deve essere configurata utilizzando un riferimento oggetto creato mediante il cmdlet <strong>Import-CsRgsAudioFile</strong>.</p>
<p>Se DefaultMusicOnHold è uguale a un valore Null (valore predefinito) e per un flusso di lavoro non è definita una musica di attesa personalizzata, ogni volta che un chiamate viene lasciato in attesa, verrà riprodotta la musica di attesa predefinita configurata automaticamente durante l'installazione di Lync Server.</p></td>
</tr>
<tr class="even">
<td><p><em>DisableCallContext</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se questo parametro è impostato su False (valore predefinito), ogni agente sarà in grado di vedere il contesto chiamata (informazioni come il tempo di attesa del chiamante o le domande e le risposte del flusso di lavoro) ogni volta che viene ricevuta una chiamata. Queste informazioni sono visibili nell'ambito di Lync. Se impostato su True, le informazioni sul contesto chiamata non vengono inoltrate agli agenti quando viene ricevuta una chiamata.</p>
<p>Il contesto della chiamata viene utilizzato solo con le code del sistema IVR.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.ServiceSettings. **Set-CsRgsConfiguration** accetta le istanze da pipeline dell'oggetto impostazioni dell'applicazione Response Group.

## Tipi restituiti

**Set-CsRgsConfiguration** non restituisce alcun oggetto o valore. Il cmdlet configura invece istanze esistenti dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.ServiceSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsRgsConfiguration](get-csrgsconfiguration.md)  
[Move-CsRgsConfiguration](move-csrgsconfiguration.md)

