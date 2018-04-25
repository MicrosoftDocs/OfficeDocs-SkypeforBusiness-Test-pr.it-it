---
title: Remove-CsClsScenario
TOCTitle: Remove-CsClsScenario
ms:assetid: 747bd4d6-797e-4088-9303-6ceb65f66183
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205010(v=OCS.15)
ms:contentKeyID: 49300987
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsClsScenario

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove lo scenario di configurazione della registrazione centralizzata specificato. Uno scenario rappresenta una situazione o un componente particolare di Lync Server 2013, ad esempio la messaggistica istantanea e la presenza, che gli amministratori possono abilitare o disabilitare ai fini della traccia. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Remove-CsClsScenario -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 rimuove lo scenario WAC dalla raccolta globale di impostazioni di configurazione della registrazione centralizzata.

    Remove-CsClsScenario -Identity "site:Redmond/WAC"

## Esempio 2

Nell'esempio 2 lo scenario HybridVoice viene rimosso da tutte le impostazioni di configurazione della registrazione centralizzata in uso nell'organizzazione. A tale scopo, viene chiamato innanzitutto il cmdlet **Get-CsClsScenario** senza alcun parametro per restituire una raccolta di tutti gli scenari disponibili. La raccolta viene quindi inviata tramite pipe al cmdlet Where-Object, che seleziona tutti gli scenari in cui la proprietà Name è uguale a (-eq) HybridVoice. Gli scenari HybridVoice vengono quindi inviati tramite pipe al cmdlet **Remove-CsClsScenario**, che li elimina.

    Get-CsClsScenario | Where-Object {$_.Name -eq "HybridVoice" | Remove-CsClsScenario

## Descrizione dettagliata

Il servizio di registrazione centralizzata, che sostituisce gli strumenti OCSLogger e OCSTracer utilizzati in Microsoft Lync Server 2010, consente agli amministratori di gestire la registrazione e la traccia per tutti i computer e i pool che eseguono Lync Server 2013. La registrazione centralizzata consente agli amministratori di arrestare, avviare e configurare la registrazione per uno o più pool e computer utilizzando un solo comando. È ad esempio possibile utilizzare un comando per abilitare la registrazione del servizio Rubrica in tutti i server della Rubrica. Questo comportamento è diverso rispetto agli strumenti OCSLogger e OCSTracer, che devono essere gestiti singolarmente (avviati e arrestati individualmente) in ogni server. Il servizio di registrazione centralizzata inoltre consente agli amministratori di eseguire ricerche nei log di traccia dal comando utilizzando l'interfaccia della riga di comando Windows PowerShell e il cmdlet [Search-CsClsLogging](search-csclslogging.md).

La registrazione centralizzata si basa su una serie di scenari predefiniti che offrono un metodo di registrazione più dettagliato rispetto alle versioni precedenti di Lync Server. Questi scenari predeterminano automaticamente i componenti del server e la registrazione. In questo modo, un amministratore che abilita lo scenario RGS avrà la certezza che verranno registrate solo le informazioni pertinenti per il servizio Response Group e non ad esempio per il servizio del provider di servizi di audioconferenza.

Il cmdlet **Remove-CsClsScenario** consente di rimuovere scenari dalle impostazioni di configurazione della registrazione centralizzata.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt di Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsClsScenario"}

Pannello di controllo di Lync Server: le funzioni eseguite dal cmdlet **Remove-CsClsScenario** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Identificatore univoco dello scenario da rimuovere. Uno scenario è costituito da due parti: l'ambito in cui lo scenario è configurato, ovvero la raccolta di impostazioni di configurazione della registrazione centralizzata in cui si trova lo scenario, e il nome dello scenario stesso. Ad esempio:</p>
<p>-Identity &quot;site:Redmond/AddressBook&quot;</p>
<p>È inoltre possibile specificare solo l'ambito dello scenario. Ad esempio:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>In tal caso, verrà tuttavia rimossa l'intera raccolta di impostazioni di configurazione della registrazione centralizzata per l'ambito specificato, non solo gli scenari.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
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
<td><p>Descrive cosa accadrebbe eseguendo il comando senza però eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Remove-CsClsScenario** accetta istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Scenario\#Decorated inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsClsScenario** invece elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Scenario\#Decorated.

