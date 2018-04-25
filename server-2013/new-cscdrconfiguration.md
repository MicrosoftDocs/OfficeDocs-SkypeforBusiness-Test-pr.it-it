---
title: New-CsCdrConfiguration
TOCTitle: New-CsCdrConfiguration
ms:assetid: e5890ac3-7a6c-4609-a866-84c39b76d3a9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399018(v=OCS.15)
ms:contentKeyID: 49302277
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsCdrConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo insieme di impostazioni di registrazione dettagli chiamata (CDR). La registrazione dettagli chiamata consente di tenere traccia dell'utilizzo delle sessioni di messaggistica istantanea peer-to-peer, delle chiamate telefoniche VoIP (Voice over Internet Protocol) e delle conferenze telefoniche. Questi dati sull'utilizzo includono informazioni sui chiamanti, sugli utenti chiamati, sulla data e ora della chiamata e sulla durata della conversazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsCdrConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-EnableCDR <$true | $false>] [-EnablePurging <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-KeepCallDetailForDays <UInt32>] [-KeepErrorReportForDays <UInt32>] [-PurgeHourOfDay <UInt32>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nel comando dell'esempio 1 viene utilizzato il cmdlet **New-CsCdrConfiguration** per creare un nuovo insieme di impostazioni per la registrazione dettagli chiamata con valore Identity site:Redmond. Oltre al valore Identity site:Redmond, le nuove impostazioni presentano anche la proprietà EnableCDR impostata su False. Poiché le impostazioni del sito hanno la precedenza sulle impostazioni globali, la registrazione dettagli chiamata non verrà utilizzata nel sito Redmond, indipendentemente dal fatto che tale funzionalità sia stata o meno abilitata nell'ambito globale.

    New-CsCdrConfiguration -Identity site:Redmond -EnableCDR $False

## ESEMPIO 2

Nell'esempio 2 viene utilizzato il parametro InMemory per mostrare come è possibile creare una nuova raccolta di impostazioni di configurazione per la registrazione dettagli chiamata che inizialmente esistano soltanto in memoria. A tale scopo, nell'esempio vengono innanzitutto utilizzati il cmdlet **New-CsCdrConfiguration** e il parametro InMemory per creare una raccolta virtuale di impostazioni con valore Identity site:Redmond. La raccolta virtuale viene archiviata nella variabile $x. Se la raccolta non fosse archiviata in una variabile, verrebbe creata e quindi scomparirebbe immediatamente.

Una volta creata la raccolta virtuale, con il comando mostrato nella riga 2 viene impostato il valore della proprietà EnableCDR su False ($False). Nella riga 3 viene quindi utilizzato il cmdlet **Set-CsCdrConfiguration** per trasformare la raccolta virtuale $x in una raccolta effettiva di impostazioni di configurazione per la registrazione dettagli chiamata, che viene applicata al sito Redmond. Se il cmdlet **Set-CsCdrConfiguration** non venisse chiamato, la raccolta virtuale scomparirebbe non appena termina la sessione di Windows PowerShell o non appena viene eliminata la variabile $x.

    $x = New-CsCdrConfiguration -Identity site:Redmond -InMemory
    $x.EnableCDR = $False
    Set-CsCdrConfiguration -Instance $x

## Descrizione dettagliata

La registrazione dettagli chiamata consente di tenere traccia dell'utilizzo di funzionalità di Lync Server quali chiamate VoIP, messaggistica istantanea, trasferimenti di file, conferenze audio/video e sessioni di condivisione delle applicazioni. Con la registrazione dettagli chiamata, disponibile soltanto se è stato distribuito il servizio di monitoraggio, vengono registrate informazioni sull'utilizzo, tra cui le parti coinvolte nella chiamata, la durata della stessa e l'eventuale trasferimento di file. Non viene invece effettuata una registrazione della chiamata vera e propria.

Con la registrazione dettagli chiamata, inoltre, viene tenuta traccia delle informazioni relative a errori delle chiamate: i dati di diagnostica dettagliati sia per le sessioni peer-to-peer che per le chiamate al servizio di conferenza.

L'amministratore può decidere se utilizzare o meno la registrazione dettagli chiamata nell'organizzazione. Se il servizio di monitoraggio è stato distribuito, l'abilitazione o la disabilitazione di tale funzionalità è un'operazione estremamente semplice. È inoltre possibile applicare questa scelta globalmente (nel qual caso la funzionalità di registrazione dettagli chiamata verrà abilitata o disabilitata nell'intera organizzazione) o a livello del singolo sito (ad esempio, è possibile decidere di utilizzare la funzionalità nel sito Redmond, ma non nel sito Paris).

Il cmdlet **New-CsCdrConfiguration** consente di creare nuove raccolte di impostazioni per la registrazione dettagli chiamata nell'ambito del sito. (Le nuove impostazioni non possono essere create nell'ambito globale.) Ciascun sito può ospitare solo una singola raccolta di tali impostazioni. Ciò significa che non è possibile creare una nuova raccolta per il sito Redmond se il sito dispone già di un set di impostazioni di configurazione per registrazione dettagli chiamata. Se si tenta di eseguire questa operazione, il comando avrà esito negativo.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsCdrConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsCdrConfiguration"}

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
<td><p>Rappresenta l'identificatore univoco da assegnare alla nuova raccolta delle impostazioni di configurazione per registrazione dettagli chiamata. Poiché è possibile creare nuove raccolte solo nell'ambito del sito, il valore Identity avrà sempre il prefisso &quot;site:&quot; seguito dal nome del sito, come, ad esempio, &quot;site:Redmond&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableCDR</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se la registrazione dettagli chiamata è abilitata o meno. Il valore predefinito è True.</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePurging</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se le registrazioni dettagli chiamata saranno eliminate periodicamente dal relativo database. Se il parametro è impostato su True (valore predefinito), i dati verranno eliminati dopo il periodo di tempo specificato nelle proprietà KeepCallDetailForDays (registrazioni dettagli chiamata) e KeepErrorReportForDays (errori di registrazione dettagli chiamata). Se False, le registrazioni verranno mantenute indefinitamente.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>KeepCallDetailForDays</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica per quanti giorni le registrazioni dettagli chiamata verranno conservate nel relativo database. Le eventuali registrazioni antecedenti al numero di giorni specificato verranno eliminate automaticamente. (Si noti che la cancellazione avverrà soltanto se la proprietà EnablePurging è stata impostata su True.)</p>
<p>KeepCallDetailForDays può essere impostato su qualsiasi valore intero compreso tra 1 e 2562 giorni (circa 7 anni). Il valore predefinito è 60.</p></td>
</tr>
<tr class="even">
<td><p><em>KeepErrorReportForDays</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica per quanti giorni verranno conservate le segnalazioni errori per registrazione dettagli chiamata. Le eventuali segnalazioni errori antecedenti al numero di giorni specificato verranno eliminate automaticamente. Le segnalazioni errori di registrazione dettagli chiamata sono rapporti diagnostici caricati da applicazioni client come Lync 2013.</p>
<p>È possibile impostare questa proprietà su qualsiasi valore intero compreso tra 1 e 2562 giorni (circa 7 anni). Il valore predefinito è 60.</p></td>
</tr>
<tr class="odd">
<td><p><em>PurgeHourOfDay</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>Indica l'ora del giorno locale per l'eliminazione dei record scaduti dal database di registrazione dettagli chiamata. L'ora del giorno viene specificata nel formato 24 ore, con lo 0 che corrisponde alla mezzanotte (00.00) e il 23 che corrisponde alle 23.00. Si noti che è possibile indicare solo l'ora del giorno. È pertanto possibile pianificare l'esecuzione della cancellazione per le 04.00, ma non per le 04.30 o le 04.15. Il valore predefinito è 2, che corrisponde alle 02.00. È consigliabile che la cancellazione avvenga in orari di non utilizzo.</p>
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

Nessuno. Il cmdlet **New-CsCdrConfiguration** non accetta input inviato tramite pipeline.

## Tipi restituiti

Crea istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CallDetailRecording.CdrSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsCdrConfiguration](get-cscdrconfiguration.md)  
[Remove-CsCdrConfiguration](remove-cscdrconfiguration.md)  
[Set-CsCdrConfiguration](set-cscdrconfiguration.md)

