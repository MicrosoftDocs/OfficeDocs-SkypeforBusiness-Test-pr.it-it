---
title: Remove-CsClsConfiguration
TOCTitle: Remove-CsClsConfiguration
ms:assetid: f10005f4-ae5c-4d9e-800f-48183b5182be
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619191(v=OCS.15)
ms:contentKeyID: 49302417
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsClsConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una o più raccolte di impostazioni di configurazione della registrazione centralizzata. Quest'ultima consente agli amministratori di abilitare o disabilitare contemporaneamente la traccia degli eventi su più computer. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Remove-CsClsConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'Esempio 1 rimuove le impostazioni di configurazione della registrazione centralizzata applicate al sito Redmond.

    Remove-CsClsConfiguration -Identity "site:Redmond"

## Esempio 2

Nell'esempio 2 vengono rimosse tutte le impostazioni di configurazione della registrazione centralizzata applicate all'ambito del sito. A questo scopo, il comando chiama prima il cmdlet **Get-CsClsConfiguration** insieme al parametro Filter. Il valore di filtro "site:\*" limita i dati restituiti alle impostazioni configurate nell'ambito del sito. Tali impostazioni vengono quindi inviate tramite pipe e rimosse mediante il cmdlet **Remove-CsClsConfiguration**.

    Get-CsClsConfiguration -Filter "site:*" | Remove-CsClsConfiguration

## Esempio 3

Nell'Esempio 3 vengono eliminate tutte le impostazioni di configurazione della registrazione centralizzata che consentono l'utilizzo di un file ETL maggiore di 20 MB. Per eseguire questa attività, il comando chiama innanzitutto il cmdlet **Get-CsClsConfiguration** senza parametri. Viene restituita una raccolta di tutte le impostazioni della registrazione centralizzata in uso nell'organizzazione. Tali impostazioni vengono quindi inviate tramite pipe al cmdlet **Where-Object** che seleziona solo quelle in cui la proprietà EtlFileRollverSizeMB è maggiore di (-gt) 20 MB. Le impostazioni che soddisfano tale criterio vengono infine inviate tramite pipe ed eliminate mediante il cmdlet **Remove-CsClsConfiguration**.

    Get-CsClsConfiguration | Where-Object {$_.EtlFileRolloverSizeMB -gt 20} | Remove-CsClsConfiguration

## Descrizione dettagliata

Il servizio di registrazione centralizzata (che sostituisce gli strumenti OCSLogger e OCSTracer utilizzati in Microsoft Lync Server 2010) consente agli amministratori di gestire la registrazione e la traccia per tutti i computer e i pool che eseguono Lync Server 2013. Grazie alla registrazione centralizzata, gli amministratori possono arrestare, avviare e configurare la registrazione per uno o più pool e computer utilizzando un singolo comando. È ad esempio possibile utilizzare un comando per abilitare la registrazione del servizio Rubrica su tutti i server Rubrica. Questa procedura non è invece eseguibile con gli strumenti OCSLogger e OCSTracer, che devono essere gestiti singolarmente (e anche arrestati e avviati singolarmente) su ogni server. Il servizio di registrazione centralizzata consente inoltre agli amministratori di effettuare ricerche nei log di traccia tramite il comando, utilizzando l'interfaccia della riga di comando Windows PowerShell e il cmdlet [Search-CsClsLogging](search-csclslogging.md).

La registrazione centralizzata si basa su una serie di scenari predefiniti che offrono un approccio più mirato alla registrazione rispetto alle versioni precedenti di Lync Server. Tali scenari prevedono componenti server e registrazione predefiniti per l'utente e di conseguenza un amministratore che abilita lo scenario RGS può essere sicuro che registrerà solo informazioni dei log rilevanti per il servizio Response Group e non, ad esempio, per il servizio del provider di servizi di audioconferenza.

È anche possibile definire scenari personalizzati utilizzando il cmdlet [New-CsClsScenario](new-csclsscenario.md).

La registrazione centralizzata viene gestita utilizzando raccolte di impostazioni di configurazione del servizio di registrazione centralizzata. Quando si installa Lync Server 2013, viene installato un set globale di queste impostazioni di configurazione. Gli amministratori possono inoltre aggiungere raccolte di impostazioni personalizzate nell'ambito del sito. Successivamente, è possibile rimuovere tali impostazioni con ambito sito mediante il cmdlet **Remove-CsClsConfiguration**. Si noti che il cmdlet può essere eseguito anche per la raccolta di impostazioni globali. In questo caso, tuttavia, la raccolta non viene rimossa, ma ne vengono ripristinati i valori predefiniti di tutte le proprietà.

Per restituire l'elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsClsConfiguration"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Remove-CsClsConfiguration** non sono disponibili in Pannello di controllo di Lync Server.

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
<td><p>Identificatore univoco della raccolta di impostazioni di configurazione della registrazione centralizzata da rimuovere. Per rimuovere le impostazioni globali, utilizzare la sintassi seguente:</p>
<p>-Identity &quot;global&quot;</p>
<p>Si noti che i criteri globali non possono essere rimossi realmente, ma piuttosto ne vengono ripristinati i valori predefiniti di tutte le proprietà.</p>
<p>Per rimuovere una raccolta configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>Si noti che non è consentito utilizzare i caratteri jolly per specificare l'identità (Identity).</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Visualizza una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione degli eventuali messaggi di errore non grave che potrebbero essere generati durante l'esecuzione del comando.</p></td>
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

Il cmdlet **Remove-CsClsConfiguration** accetta le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.CentralizedLoggingConfiguration inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsClsConfiguration** elimina invece le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.CentralizedLoggingConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsClsConfiguration](get-csclsconfiguration.md)  
[New-CsClsConfiguration](new-csclsconfiguration.md)  
[Set-CsClsConfiguration](set-csclsconfiguration.md)

