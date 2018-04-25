---
title: Set-CsCdrConfiguration
TOCTitle: Set-CsCdrConfiguration
ms:assetid: 977f0d3e-796b-43a3-bc0c-82ea91741c52
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398774(v=OCS.15)
ms:contentKeyID: 49301420
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCdrConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una raccolta esistente di impostazioni di registrazione dettagli chiamata (CDR). La registrazione dettagli chiamata consente di tenere traccia dell'utilizzo delle sessioni di messaggistica istantanea peer-to-peer, delle chiamate telefoniche VoIP (Voice over Internet Protocol) e delle conferenze telefoniche. Questi dati sull'utilizzo includono informazioni sui chiamanti, sugli utenti chiamati, sulla data e ora della chiamata e sulla durata della conversazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsCdrConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsCdrConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EnableCDR <$true | $false>] [-EnablePurging <$true | $false>] [-Force <SwitchParameter>] [-KeepCallDetailForDays <UInt32>] [-KeepErrorReportForDays <UInt32>] [-PurgeHourOfDay <UInt32>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene impostata l'ora del giorno per l'eliminazione dei record obsoleti. In questo caso l'ora è impostata su 23 (le 11 di sera). Il parametro Identity viene utilizzato per garantire che le modifiche siano apportate solamente alle impostazioni di registrazione dettagli chiamata con l'identità site:Redmond.

    Set-CsCdrConfiguration -Identity site:Redmond -PurgeHourOfDay 23 

## ESEMPIO 2

L'esempio 2 è una variante del comando mostrato nell'esempio 1. In questo caso viene modificata la proprietà PurgeHourOfDay per ogni raccolta di impostazioni di configurazione di registrazione dettagli chiamata attualmente in uso nell'organizzazione. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsCdrConfiguration** senza parametri per restituire una raccolta di tutte le impostazioni di registrazione dettagli chiamata attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsCdrConfiguration**, che seleziona ogni elemento nella raccolta e cambia il valore della proprietà PurgeHourOfDay in 23.

    Get-CsCdrConfiguration | Set-CsCdrConfiguration -PurgeHourOfDay 23 

## ESEMPIO 3

Nell'esempio 3 viene mostrata un'altra variante del comando illustrato nell'esempio 1. In questo caso, viene modificata la proprietà PurgeHourOfDay per tutte le impostazioni di configurazione di registrazione dettagli chiamata configurate nell'ambito del sito. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsCdrConfiguration** con il parametro Filter. Il valore di filtro "site:\*" garantisce la restituzione delle sole impostazioni di registrazione dettagli chiamata la cui identità (Identity) inizia con il valore stringa "site:". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsCdrConfiguration**, che modifica la proprietà PurgeHourOfDay per ogni elemento della raccolta.

    Get-CsCdrConfiguration -Filter "site:*"| Set-CsCdrConfiguration -PurgeHourOfDay 23

## Descrizione dettagliata

La registrazione dettagli chiamata consente di tenere traccia dell'utilizzo delle funzionalità di Lync Server quali chiamate telefoniche VoIP, messaggistica istantanea, trasferimenti di file, conferenze audio/video (A/V) e sessioni di condivisione applicazioni. Con la registrazione dettagli chiamata (che è disponibile soltanto se è stato distribuito il servizio di monitoraggio) vengono registrate informazioni sull'utilizzo, come le parti coinvolte nella chiamata, la durata della chiamata, se sono stati trasferiti file o meno e così via. Non viene tuttavia registrata la chiamata stessa.

Con la registrazione dettagli chiamata, inoltre, viene tenuta traccia delle informazioni relative a errori delle chiamate: i dati di diagnostica dettagliati per sessioni peer-to-peer e per conferenze telefoniche.

L'amministratore è in grado di stabilire se la registrazione dei dettagli della chiamata debba o meno essere utilizzata nell'organizzazione; una volta abilitato il servizio di monitoraggio, l'abilitazione o la disabilitazione della registrazione sono operazioni estremamente semplici. Inoltre, è possibile prendere questa decisione a livello globale (nel qual caso la registrazione dettagli chiamata verrà abilitata o disabilitata all'interno di tutta l'organizzazione) o sito per sito. Ad esempio, si potrebbe utilizzare la registrazione dettagli chiamata nel sito Redmond ma non nel sito Paris.

Gli amministratori possono inoltre gestire il database di registrazione dettagli chiamata, ad esempio per specificare il numero di giorni di conservazione dei record prima dell'eliminazione dal database. Le modifiche come queste possono essere apportate con il cmdlet **Set-CsCdrConfiguration**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Set-CsCdrConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCdrConfiguration"}

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
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableCDR</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se la registrazione dettagli chiamata è abilitata. Il valore predefinito è True.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnablePurging</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se i record di registrazione dettagli chiamata saranno periodicamente eliminati dal database di registrazione dettagli chiamata. Se l'impostazione è True (il valore predefinito) i record verranno eliminati dopo il periodo specificato nelle proprietà KeepCallDetailForDays (per i record di registrazione dettagli chiamata) e KeepErrorReportForDays (per gli errori di registrazione dettagli chiamata). Se False, le registrazioni verranno mantenute indefinitamente.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco assegnato alla raccolta di impostazioni di configurazione di registrazione dettagli chiamata. Per fare riferimento alle impostazioni globali, utilizzare la sintassi seguente: -Identity global. Per fare riferimento a una raccolta configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Non è possibile utilizzare caratteri jolly per specificare un'identità.</p>
<p>Se questo parametro non viene specificato, il cmdlet <strong>Set-CsCdrConfiguration</strong> modificherà le impostazioni globali.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto CdrSettings</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>KeepCallDetailForDays</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica il numero di giorni per i quali i record di registrazione dettagli chiamata verranno conservati nel database di registrazione dettagli chiamata; eventuali registrazioni precedenti il numero specificato di giorni verranno automaticamente eliminate. L'eliminazione avviene solo se la proprietà EnablePurging è stata impostata su True.</p>
<p>È possibile impostare questa proprietà su qualsiasi valore intero compreso tra 1 e 2562 giorni (circa 7 anni). Il valore predefinito è 60.</p></td>
</tr>
<tr class="even">
<td><p><em>KeepErrorReportForDays</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica per quanti giorni verranno conservati i rapporti sugli errori di registrazione dettagli chiamata. I rapporti meno recenti rispetto al numero di giorni specificato saranno eliminati automaticamente. I rapporti sugli errori di registrazione dettagli chiamata sono rapporti diagnostici caricati da applicazioni client come Lync 2013.</p>
<p>È possibile impostare questa proprietà su qualsiasi valore intero compreso tra 1 e 2562 giorni (circa 7 anni). Il valore predefinito è 60.</p></td>
</tr>
<tr class="odd">
<td><p><em>PurgeHourOfDay</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica l'ora del giorno locale per l'eliminazione dei record scaduti dal database di registrazione dettagli chiamata. L'ora del giorno viene specificata nel formato 24 ore; 0 rappresenta la mezzanotte, 23 rappresenta le 11 di sera. È possibile specificare soltanto l'ora del giorno; è quindi possibile pianificare la cancellazione alle 4.00 del mattino, ma non alle 4.30 o alle 4.15. Il valore predefinito è 2 (2.00 del mattino). È consigliabile che la cancellazione avvenga in orari di non utilizzo.</p>
<p>La cancellazione del database si verifica solo se la proprietà EnablePurging è impostata su True.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings. Il cmdlet **Set-CsCdrConfiguration** accetta l'input di oggetti configurazione registrazione dettagli chiamata inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CsCdrConfiguration** non restituisce alcun oggetto o valore. Configura invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CDRSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsCdrConfiguration](get-cscdrconfiguration.md)  
[New-CsCdrConfiguration](new-cscdrconfiguration.md)  
[Remove-CsCdrConfiguration](remove-cscdrconfiguration.md)

