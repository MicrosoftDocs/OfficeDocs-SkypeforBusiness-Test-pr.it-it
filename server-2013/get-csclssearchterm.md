---
title: Get-CsClsSearchTerm
TOCTitle: Get-CsClsSearchTerm
ms:assetid: 89a6cc1d-5cbe-42ef-b5a0-127068a0f78a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205061(v=OCS.15)
ms:contentKeyID: 49301240
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsClsSearchTerm

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui termini di ricerca della registrazione centralizzata disponibili per l'utilizzo nell'organizzazione. I termini di ricerca facilitano la definizione delle informazioni personali disponibili per il personale addetto all'assistenza tecnica che esegue ricerche nei log di traccia centralizzati. L'utilizzo dei termini di ricerca è previsto con Skype for Business online.

Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsClsSearchTerm [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsClsSearchTerm [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce le informazioni su tutti i termini di ricerca attualmente in uso nell'organizzazione.

    Get-CsClsSearchTerm

## Esempio 2

Nell'esempio 2 vengono restituite le informazioni per un singolo termine di ricerca, ovvero il termine di ricerca Phone trovato nella raccolta globale di impostazioni di configurazione della registrazione centralizzata.

    Get-CsClsSearchTerm -Identity "global/Phone"

## Esempio 3

Il comando riportato nell'esempio 3 restituisce le informazioni per tutti i termini di ricerca URI. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsClsSearchTerm**senza alcun parametro. In questo modo viene restituita una raccolta di tutti i termini di ricerca disponibili. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i termini in cui la proprietà Type è uguale a (-eq) URI.

    Get-CsClsSearchTerm | Where-Object {$_.Type -eq "URI"}

## Esempio 4

Nell'esempio 4 vengono restituite le informazioni per tutti i termini di ricerca in cui la proprietà Inserts include il valore stringa "ItemE164". A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsClsSearchTerm** per restituire una raccolta di tutti i termini di ricerca disponibili. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona i termini per i quali la proprietà Inserts include (-match) il valore stringa "ItemE164".

    Get-CsClsSearchTerm | Where-Object {$_.Inserts -match "ItemE164"}

## Descrizione dettagliata

Il servizio di registrazione centralizzata, che sostituisce gli strumenti OCSLogger e OCSTracer utilizzati in Microsoft Lync Server 2010, consente agli amministratori di gestire la registrazione e la traccia per tutti i computer e i pool che eseguono Lync Server 2013. La registrazione centralizzata consente agli amministratori di arrestare, avviare e configurare la registrazione per uno o più pool e computer utilizzando un solo comando. È ad esempio possibile utilizzare un comando per abilitare la registrazione del servizio Rubrica in tutti i server della Rubrica. Questo comportamento è diverso rispetto agli strumenti OCSLogger e OCSTracer, che devono essere gestiti singolarmente (avviati e arrestati individualmente) in ogni server. Il servizio di registrazione centralizzata inoltre consente agli amministratori di eseguire ricerche nei log di traccia dal comando utilizzando l'interfaccia della riga di comando Windows PowerShell e il cmdlet [Search-CsClsLogging](search-csclslogging.md).

In Lync Server 2013 gli amministratori possono utilizzare i termini di ricerca per nascondere al personale dell'assistenza tecnica che visualizza i file di log le informazioni personali. Ad esempio il nome dell'utente Ken Myer non verrebbe visualizzato utilizzando la console del supporto tecnico e potrebbe essere visualizzato piuttosto come FIRST1 LAST1. Analogamente, un numero di telefono, ad esempio +12065551219, potrebbe essere visualizzato come PHONE1.

Il cmdlet **Get-CsClsSearchTerm** restituisce informazioni sui termini di ricerca attualmente disponibili per l'utilizzo. I termini di ricerca sono basati sulla proprietà Inserts, che specifica le informazioni che verranno mascherate e la maschera che verrà sostituita per le informazioni personali.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt di Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsClsSearchTerm"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsClsSearchTerm** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Consente di utilizzare caratteri jolly per restituire uno o più termini di ricerca. Ad esempio, per restituire tutti i termini di ricerca CallID, indipendentemente dall'ambito in cui tali termini sono stati configurati, utilizzare la sintassi seguente:</p>
<p>-Filter &quot;*CallID*&quot;</p>
<p>Non è possibile utilizzare i parametri Identity e Filter nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco del termine di ricerca da restituire. Un termine di ricerca è costituito da due parti: l'ambito in cui il termine è configurato, ovvero la raccolta di impostazioni di configurazione della registrazione centralizzata in cui è possibile trovare il termine, e il nome del termine. Ad esempio:</p>
<p>-Identity &quot;site:Redmond/CallID&quot;</p>
<p>È inoltre possibile specificare solo l'ambito del termine di ricerca. Ad esempio:</p>
<p>-Identity &quot;site:Redmond&quot;</p>
<p>In questo caso, verranno restituiti tutti i termini di ricerca configurati per l'utilizzo nel sito Redmond.</p>
<p>Se questo parametro non viene specificato, il cmdlet <strong>Get-CsSearchTerm</strong> restituirà informazioni su tutti i termini di ricerca della registrazione centralizzata.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati dei termini di ricerca dalla replica locale dell'archivio di gestione centrale anziché direttamente da tale archivio.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsClsSearchTerm** non supporta l'input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsClsSearchTerm** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.SearchTerm\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Set-CsClsSearchTerm](set-csclssearchterm.md)

