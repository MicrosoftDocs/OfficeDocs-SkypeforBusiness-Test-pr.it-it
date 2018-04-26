---
title: Remove-CsDiagnosticConfiguration
TOCTitle: Remove-CsDiagnosticConfiguration
ms:assetid: b15293bf-d0d1-4322-ab1d-10b54636746a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412853(v=OCS.15)
ms:contentKeyID: 49301695
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsDiagnosticConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una o più raccolte di impostazioni di configurazione della diagnostica attualmente in uso nell'organizzazione. Tali impostazioni vengono utilizzate per determinare se il traffico proveniente o diretto verso un determinato dominio o URI (Uniform Resource Identifier) viene registrato nei file di log di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsDiagnosticConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono eliminate le impostazioni di configurazione della diagnostica con l'identità site:Redmond.

    Remove-CsDiagnosticConfiguration -Identity site:Redmond

## ESEMPIO 2

Con il comando riportato nell'esempio 2 vengono eliminate tutte le impostazioni di configurazione della diagnostica definite nell'ambito del sito. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsDiagnosticConfiguration** con il parametro Filter. Il valore di filtro "site:\*" restituisce solo i dati relativi alle impostazioni con valore Identity che inizia con i caratteri "site:". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsDiagnosticConfiguration**, che rimuove ogni elemento della raccolta.

    Get-CsDiagnosticConfiguration -Filter site:* | Remove-CsDiagnosticConfiguration

## ESEMPIO 3

Con il comando riportato nell'esempio 3 vengono eliminate tutte le impostazioni di configurazione della diagnostica attualmente in uso nell'organizzazione. A tale scopo, viene chiamato innanzitutto il cmdlet **Get-CsDiagnosticConfiguration** senza alcun parametro per restituire una raccolta di tutte le impostazioni di configurazione della diagnostica attualmente in uso nell'organizzazione. Questi elementi vengono quindi inviati tramite pipe al cmdlet **Remove-CsDiagnosticConfiguration**, che rimuove ogni elemento della raccolta.

    Get-CsDiagnosticConfiguration | Remove-CsDiagnosticConfiguration

## Descrizione dettagliata

Se si abilita la registrazione per Lync Server, per impostazione predefinita verrà incluso nei file di log il traffico diretto o proveniente da un qualsiasi dominio o URI. In questo modo, nei file di log verrà inclusa la maggior quantità di informazioni possibile.

Esiste tuttavia il rischio che una tale quantità di informazioni risulti eccessiva. Se ad esempio si verificano problemi di connettività con un determinato dominio, è possibile limitare la registrazione al traffico tra la rete e il dominio specifico. In questo modo risulterà più semplice identificare i record pertinenti e potrebbero pertanto essere agevolate la diagnosi e la risoluzione del problema.

Le impostazioni di configurazione della diagnostica consentono di specificare i domini o gli URI che verranno registrati nei file di log. Se è abilitato un filtro di diagnostica, verrà registrato solo il traffico diretto o proveniente dai domini specificati. Lync Server consente di creare impostazioni di configurazione della diagnostica e di applicare filtri di diagnostica nell'ambito del sito. Ciò consente a sua volta di applicare ad esempio filtri al sito Redmond lasciando disabilitati i filtri negli altri siti.

È possibile utilizzare il cmdlet **Remove-CsDiagnosticConfiguration** per rimuovere le impostazioni di configurazione della diagnostica create nell'ambito del sito. Il cmdlet **Remove-CsDiagnosticConfiguration** può essere eseguito anche per le impostazioni di configurazione della diagnostica globali. In questo caso tuttavia la raccolta non verrà eliminata, in quanto in Lync Server le raccolte globali non possono essere eliminate. La rimozione di una raccolta globale tuttavia fa sì che per tutte le relative proprietà vengano ripristinati i valori predefiniti. Tutti i filtri aggiunti alla raccolta verranno pertanto rimossi.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsDiagnosticConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsDiagnosticConfiguration"}

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
<td><p>Identificatore univoco delle impostazioni di configurazione della diagnostica da rimuovere. Per rimuovere le impostazioni configurate nell'ambito del sito, utilizzare una sintassi simile a quella riportata di seguito: -Identity &quot;site:Redmond&quot;.</p>
<p>Il cmdlet <strong>Remove-CsDiagnosticConfiguration</strong> può anche essere eseguito per le impostazioni globali di configurazione. In questo caso, utilizzare la sintassi -Identity global. Le impostazioni globali non verranno effettivamente rimosse, ma verranno ripristinati i valori predefiniti di tutte le relative proprietà.</p>
<p></p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.DiagnosticFilterSettings. Il cmdlet **Remove-CsDiagnosticConfiguration** accetta istanze dell'oggetto impostazioni filtro di diagnostica inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsDiagnosticConfiguration** invece elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.DiagnosticFilterSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsDiagnosticConfiguration](get-csdiagnosticconfiguration.md)  
[New-CsDiagnosticConfiguration](new-csdiagnosticconfiguration.md)  
[Set-CsDiagnosticConfiguration](set-csdiagnosticconfiguration.md)

