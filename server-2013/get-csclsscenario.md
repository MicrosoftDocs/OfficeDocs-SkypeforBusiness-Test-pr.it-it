---
title: Get-CsClsScenario
TOCTitle: Get-CsClsScenario
ms:assetid: 8f0c5f52-c000-4e27-82a2-534a50b11a98
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205091(v=OCS.15)
ms:contentKeyID: 49301302
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsClsScenario

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni su uno o più scenari di configurazione della registrazione centralizzata. Uno scenario rappresenta una situazione o un componente particolare di Lync Server 2013, ad esempio la messaggistica istantanea e la presenza, che gli amministratori possono abilitare o disabilitare ai fini della traccia. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsClsScenario [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsClsScenario [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce le informazioni su tutti gli scenari di registrazione centralizzata attualmente in uso nell'organizzazione.

    Get-CsClsScenario

## Esempio 2

Nell'esempio 2 vengono restituite le informazioni su un singolo scenario di registrazione centralizzata, ovvero lo scenario VoiceMail incluso nella raccolta di impostazioni globali.

    Get-CsClsScenario -Identity "global/VoiceMail"

## Esempio 3

Nell'esempio 3 vengono restituite informazioni su tutti gli scenari predefiniti attualmente in uso. A tale scopo, nel comando viene innanzitutto chiamato il cmdlet **Get-CsClsScenario** senza alcun parametro. In questo modo viene restituita una raccolta di tutti gli scenari disponibili. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo gli scenari contenenti (-match) un provider denominato "AsMcu".

    Get-CsClsScenario | Where-Object {$_.Provider.Name -match "AsMcu"}

## Esempio 4

Nell'esempio 4 vengono restituite informazioni dettagliate per la proprietà Provider dello scenario globale VoiceMail. A tale scopo, viene innanzitutto utilizzato il cmdlet **Get-CsClsScenario** per restituire tutti i valori delle proprietà dello scenario globale VoiceMail. Queste informazioni vengono quindi inviate tramite pipe al cmdlet Select-Object, che utilizza il parametro ExpandProperty per "espandere" il valore della proprietà Provider. In questo modo tutti i dati archiviati nella proprietà Provider vengono visualizzati in un formato facilmente leggibile.

    Get-CsClsScenario -Identity "global/VoiceMail" | Select-Object -ExpandProperty Provider

## Descrizione dettagliata

Il servizio di registrazione centralizzata, che sostituisce gli strumenti OCSLogger e OCSTracer utilizzati in Microsoft Lync Server 2010, consente agli amministratori di gestire la registrazione e la traccia per tutti i computer e i pool che eseguono Lync Server 2013. La registrazione centralizzata consente agli amministratori di arrestare, avviare e configurare la registrazione per uno o più pool e computer utilizzando un solo comando. È ad esempio possibile utilizzare un comando per abilitare la registrazione del servizio Rubrica in tutti i server della Rubrica. Questo comportamento è diverso rispetto agli strumenti OCSLogger e OCSTracer, che devono essere gestiti singolarmente (avviati e arrestati individualmente) in ogni server. Il servizio di registrazione centralizzata inoltre consente agli amministratori di eseguire ricerche nei log di traccia dal comando utilizzando l'interfaccia della riga di comando Windows PowerShell e il cmdlet [Search-CsClsLogging](search-csclslogging.md).

La registrazione centralizzata si basa su una serie di scenari predefiniti che offrono un metodo di registrazione più dettagliato rispetto alle versioni precedenti di Lync Server. Questi scenari predeterminano automaticamente i componenti del server e la registrazione. In questo modo, un amministratore che abilita lo scenario RGS avrà la certezza che verranno registrate solo le informazioni pertinenti per il servizio Response Group e non ad esempio per il servizio del provider di servizi di audioconferenza.

Per restituire informazioni su tutti gli scenari di registrazione centralizzata disponibili per l'utilizzo nell'organizzazione, utilizzare il cmdlet **Get-CsClsScenario**.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsClsScenario"}

Pannello di controllo di Lync Server: le funzioni eseguite dal cmdlet **Get-CsClsScenario** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare caratteri jolly per restituire uno o più scenari. Ad esempio, per restituire tutti gli scenari HybridVoice, indipendentemente dall'ambito in cui tali scenari sono stati configurati, utilizzare la sintassi seguente:</p>
<p>-Filter &quot;*HybridVoice*&quot;</p>
<p>Non è possibile utilizzare i parametri Identity e Filter nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco dello scenario da restituire. Uno scenario è costituito da due parti: l'ambito in cui lo scenario è configurato, ovvero la raccolta di impostazioni di configurazione della registrazione centralizzata in cui si trova lo scenario, e il nome dello scenario stesso. Ad esempio:</p>
<p>-Identity &quot;site:Redmond/AddressBook&quot;</p>
<p>È inoltre possibile specificare solo l'ambito dello scenario. Ad esempio:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>In questo caso, verranno restituiti tutti gli scenari configurati per l'utilizzo nel sito Redmond.</p>
<p>Se questo parametro non viene specificato, il cmdlet <strong>Get-CsClsScenario</strong> restituirà informazioni su tutti gli scenari di registrazione centralizzata.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati degli scenari dalla replica locale dell'archivio di gestione centrale anziché direttamente da tale archivio.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsScenario** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsScenario** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Scenario\#Decorated.

