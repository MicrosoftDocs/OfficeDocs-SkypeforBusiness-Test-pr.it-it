---
title: Set-CsClsSearchTerm
TOCTitle: Set-CsClsSearchTerm
ms:assetid: 57ccaf25-31ab-4059-8dc4-144f29f3af68
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204911(v=OCS.15)
ms:contentKeyID: 49300596
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsClsSearchTerm

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica uno o più termini di ricerca della registrazione centralizzata. I termini di ricerca facilitano la definizione delle informazioni personali disponibili per il personale addetto all'assistenza tecnica che esegue ricerche nei log di traccia centralizzati. L'utilizzo dei termini di ricerca è previsto con Skype for Business online.

Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsClsSearchTerm [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsClsSearchTerm [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Inserts <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio imposta la proprietà Inserts per il termine di ricerca "site:Redmond/IP". In questo esempio è configurata una singola proprietà Inserts: ItemURI.

    Set-CsClsSearchTerm -Identity "site:Redmond/IP" -Inserts "ItemURI"

## Descrizione dettagliata

Il servizio di registrazione centralizzata, che sostituisce gli strumenti OCSLogger e OCSTracer utilizzati in Microsoft Lync Server 2010, consente agli amministratori di gestire la registrazione e la traccia per tutti i computer e i pool che eseguono Lync Server 2013. La registrazione centralizzata consente agli amministratori di arrestare, avviare e configurare la registrazione per uno o più pool e computer utilizzando un solo comando. È ad esempio possibile utilizzare un comando per abilitare la registrazione del Servizio Rubrica in tutti i server della Rubrica. Questo comportamento è diverso rispetto agli strumenti OCSLogger e OCSTracer, che devono essere gestiti singolarmente (avviati e arrestati individualmente) in ogni server. Il servizio di registrazione centralizzata inoltre consente agli amministratori di eseguire ricerche nei log di traccia dal comando utilizzando l'interfaccia della riga di comando Windows PowerShell e il cmdlet [Search-CsClsLogging](search-csclslogging.md).

In Skype for Business online gli amministratori possono utilizzare i termini di ricerca per nascondere le informazioni personali al personale dell'assistenza tecnica che visualizza i file di log. Ad esempio, il nome dell'utente Ken Myer non verrebbe visualizzato utilizzando la console del supporto tecnico e potrebbe essere visualizzato piuttosto come FIRST1 LAST1. Analogamente, un numero di telefono, ad esempio +12065551219, potrebbe essere visualizzato come PHONE1.

Il cmdlet **Set-CsClsSearchTerm** consente di modificare i termini di ricerca attualmente assegnati a una raccolta di impostazioni di configurazione della registrazione centralizzata.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsClsSearchTerm"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Set-CsClsSearchTerm** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco del termine di ricerca da modificare. Un termine di ricerca è costituito da due parti: l'ambito in cui il termine è configurato, ovvero la raccolta di impostazioni di configurazione della registrazione centralizzata in cui è possibile trovare il termine, e il nome del termine. Ad esempio:</p>
<p>-Identity &quot;site:Redmond/CallID&quot;</p>
<p>Non è possibile utilizzare caratteri jolly quando si specifica l'identità.</p></td>
</tr>
<tr class="even">
<td><p><em>Inserts</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Specifica il modo in cui le informazioni personali vengono mascherate durante la visualizzazione dei file di log. Ad esempio, l'Insert &quot;ItemURI&quot; indica che le informazioni relative all'URI dell'utente devono essere mascherate. Un URI utente come sip:kenmyer@litwareinc.com ad esempio verrà visualizzato come un URI generico che nasconde il nome utente, ma mantiene il nome di dominio:</p>
<p>Sip:USER1@litwareinc.com</p>
<p>Gli Insert mascherano elementi quali nomi utente e nomi computer, numeri di telefono e indirizzi IP.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Consente di passare un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Set-CsClsSearchTerm** accetta le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.SearchTerm\#Decorated inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsClsSearchTerm** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.SearchTerm\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsClsSearchTerm](get-csclssearchterm.md)

