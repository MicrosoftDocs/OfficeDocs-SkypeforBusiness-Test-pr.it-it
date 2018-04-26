---
title: Remove-CsCdrConfiguration
TOCTitle: Remove-CsCdrConfiguration
ms:assetid: 64352746-a03c-434a-9baf-4d9cd630e9da
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398451(v=OCS.15)
ms:contentKeyID: 49300784
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCdrConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove la raccolta specificata di impostazioni di registrazione dettagli chiamata (CDR). La registrazione dettagli chiamata consente di tenere traccia dell'utilizzo delle sessioni di messaggistica istantanea peer-to-peer, delle chiamate telefoniche VoIP (Voice over Internet Protocol) e delle conferenze telefoniche. Questi dati sull'utilizzo includono informazioni sui chiamanti, sugli utenti chiamati, sulla data e ora della chiamata e sulla durata della conversazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsCdrConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene utilizzato il cmdlet **Remove-CsCdrConfiguration** per rimuovere le impostazioni di registrazione dettagli chiamata assegnate al sito Redmond. L'utilizzo del parametro Identity garantisce che vengano rimosse solo le impostazioni assegnate al sito specificato.

    Remove-CsCdrConfiguration -Identity site:Redmond

## ESEMPIO 2

Il comando riportato nell'esempio 2 rimuove tutte le impostazioni di registrazione dettagli chiamata assegnate nell'ambito del sito. A tale scopo, nel comando vengono innanzitutto utilizzati il cmdlet **Get-CsCdrConfiguration** e il parametro Filter per recuperare le impostazioni di registrazione dettagli chiamata appropriate. Il valore stringa "site:\*" assicura che vengano restituite solo le impostazioni con valore Identity che inizia con i caratteri "site:". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsCdrConfiguration**, che elimina tutti gli elementi della raccolta.

    Get-CsCdrConfiguration -Filter site:* | Remove-CsCdrConfiguration

## ESEMPIO 3

Nell'esempio 3 vengono eliminate tutte le impostazioni di registrazione dettagli chiamata con proprietà KeepCallDetailForDays impostata su un valore inferiore a 30 giorni. A tale scopo, il comando chiama il cmdlet **Get-CsCdrConfiguration** senza ulteriori parametri per restituire una raccolta di tutte le impostazioni di registrazione dettagli chiamata attualmente in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni con proprietà KeepCallDetailForDays impostata su un valore inferiore a 30 giorni. La raccolta filtrata viene quindi inviata tramite pipe a **Remove-CsCdrConfiguration**, che elimina ogni elemento presente nella raccolta.

    Get-CsCdrConfiguration | Where-Object {$_.KeepCallDetailForDays -lt 30} | Remove-CsCdrConfiguration

## Descrizione dettagliata

La registrazione dettagli chiamata consente di tenere traccia dell'utilizzo delle funzionalità di Lync Server quali chiamate telefoniche VoIP, messaggistica istantanea, trasferimenti di file, conferenze audio/video (A/V) e sessioni di condivisione applicazioni. Con la registrazione dettagli chiamata (che è disponibile soltanto se è stato distribuito il servizio di monitoraggio) vengono registrate informazioni sull'utilizzo, come le parti coinvolte nella chiamata, la durata della chiamata, se sono stati trasferiti file o meno e così via. Non viene tuttavia registrata la chiamata stessa.

Con la registrazione dettagli chiamata, inoltre, viene tenuta traccia delle informazioni relative a errori delle chiamate: dati di diagnostica dettagliati sia per sessioni peer-to-peer che per le chiamate al servizio di conferenza.

In qualità di amministratore è possibile specificare se utilizzare la registrazione dettagli chiamata nell'organizzazione. Se è stato distribuito il servizio di monitoraggio, è possibile abilitare o disabilitare la registrazione dettagli chiamata senza difficoltà. È inoltre possibile applicare questa scelta globalmente (nel qual caso la funzionalità di registrazione dettagli chiamata verrà abilitata o disabilitata nell'intera organizzazione) o a livello di singolo sito, utilizzando ad esempio questa funzionalità nel sito Redmond, ma non nel sito Paris.

Le impostazioni specifiche per il sito create tramite il cmdlet **New-CsCdrConfiguration** possono essere rimosse successivamente utilizzando il cmdlet **Remove-CsCdrConfiguration**. Dopo la rimozione delle impostazioni specifiche per il sito, la registrazione dettagli chiamata relativa a tale sito verrà gestita automaticamente in base alle impostazioni di configurazione globali di tale funzionalità.

È inoltre possibile eseguire il cmdlet **Remove-CsCdrConfiguration** per le impostazioni globali della funzionalità registrazione dettagli chiamata. Poiché tuttavia le impostazioni globali non possono essere rimosse, verranno ripristinati i relativi valori predefiniti. Si supponga ad esempio di aver impostato su 90 il valore della proprietà KeepCallDetailForDays nelle impostazioni globali. Se si esegue il cmdlet **Remove-CsCdrConfiguration** per le impostazioni globali, verrà ripristinato il valore predefinito di tale proprietà, ovvero 60.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsCdrConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCdrConfiguration"}

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
<td><p>Identificatore univoco delle impostazioni di configurazione di registrazione dettagli chiamata da rimuovere. Per &quot;rimuovere&quot; le impostazioni globali, utilizzare la seguente sintassi: -Identity global. Come già evidenziato, le impostazioni globali non vengono effettivamente rimosse, bensì vengono ripristinati i valori predefiniti delle relative proprietà. Per rimuovere le impostazioni dall'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Non è possibile utilizzare caratteri jolly quando si specifica il parametro Identity.</p></td>
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
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings. Il cmdlet **Remove-CsCdrConfiguration** accetta l'input di oggetti configurazione registrazione dettagli chiamata inviato tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet piuttosto elimina le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsCdrConfiguration](get-cscdrconfiguration.md)  
[New-CsCdrConfiguration](new-cscdrconfiguration.md)  
[Set-CsCdrConfiguration](set-cscdrconfiguration.md)

