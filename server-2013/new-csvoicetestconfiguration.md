---
title: New-CsVoiceTestConfiguration
TOCTitle: New-CsVoiceTestConfiguration
ms:assetid: da312c27-bc89-46c3-a6c9-c098ed4e7df7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398961(v=OCS.15)
ms:contentKeyID: 49302152
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsVoiceTestConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea uno scenario di test utilizzabile per verificare i numeri di telefono rispetto a route e regole specificate. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsVoiceTestConfiguration -Name <String> <COMMON PARAMETERS>

    New-CsVoiceTestConfiguration -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-DialedNumber <String>] [-ExpectedRoute <String>] [-ExpectedTranslatedNumber <String>] [-ExpectedUsage <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-TargetDialplan <String>] [-TargetVoicePolicy <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene creata una nuova configurazione di test vocale con valori predefiniti, la cui identità è TestConfig1.

    New-CsVoiceTestConfiguration -Identity TestConfig1

## ESEMPIO 2

In questo esempio viene creata una nuova configurazione di test vocale denominata TestConfig1 e il parametro TargetLocationProfile viene impostato su site:Redmond1. Ciò consentirà di testare il numero, l'utilizzo e la route previsti utilizzando le impostazioni del dial plan per il sito Redmond1.

In questo esempio TestConfig1 viene dichiarata senza specificare il parametro Identity. Il parametro Identity è di tipo posizionale, per cui il primo valore del comando che segue il nome del cmdlet viene riconosciuto dal cmdlet come identità.

    New-CsVoiceTestConfiguration TestConfig1 -TargetDialplan site:Redmond1

## ESEMPIO 3

In questo esempio viene creata una nuova configurazione di test vocale denominata TestConfig1. Questa configurazione utilizzerà i valori predefiniti per testare il parametro DialedNumber 5551212 su un output previsto (ExpectedTranslatedNumber) di +5551212. La previsione si basa sulle regole di normalizzazione associate al dial plan che verrà utilizzato quando verrà eseguito un test su questo oggetto. Il test deve essere eseguito utilizzando il cmdlet **Test-CsVoiceTestConfiguration**.

    New-CsVoiceTestConfiguration -Identity TestConfig1 -DialedNumber 5551212 -ExpectedTranslatedNumber +5551212

## Descrizione dettagliata

Prima di implementare route vocali e criteri vocali, è opportuno testarli su diversi numeri di telefono per garantire che i risultati siano quelli previsti. ﻿È possibile eseguire questi test creando scenari di prova con questo cmdlet.

Il cmdlet **New-CsVoiceTestConfiguration** definisce la route vocale, l'utilizzo, il dial plan e il criterio vocale su cui testare un numero di telefono specificato. Tutte queste informazioni possono essere definite e recuperate utilizzando altri cmdlet. Per ulteriori dettagli, vedere le descrizioni dei parametri di questo argomento.

Per testare le configurazioni create con questo cmdlet è possibile utilizzare il cmdlet **Test-CsVoiceTestConfiguration**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsVoiceTestConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsVoiceTestConfiguration"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Una stringa che identifica in modo univoco questo scenario di test.</p>
<p>Questa stringa può essere lunga fino a 32 caratteri e può contenere caratteri alfanumerici oltre alla barra rovesciata (\), il punto (.) o il carattere di sottolineatura (_).</p>
<p>Il valore di questo parametro non include l'ambito perché l'oggetto può essere creato solo con ambito globale. Di conseguenza è richiesto solamente un nome univoco.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Questo parametro contiene lo stesso valore del parametro Identity. Se il parametro Identity è specificato, non è possibile includere il parametro Name nel comando. Allo stesso modo, se il parametro Name è specificato, non è possibile specificare il parametro Identity.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DialedNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il numero di telefono da utilizzare per testare criteri, utilizzi e così via.</p>
<p>Deve contenere al massimo 512 caratteri.</p>
<p>Valore predefinito: 1234</p></td>
</tr>
<tr class="odd">
<td><p><em>ExpectedRoute</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome della route vocale che si prevede di utilizzare durante il test di configurazione. Se si utilizza una route diversa, basata sul criterio vocale e sul dial plan di destinazione, il test non riuscirà. Per recuperare le route vocali disponibili è possibile chiamare il cmdlet <strong>Get-CsVoiceRoute</strong>.</p>
<p>Deve contenere al massimo 256 caratteri.</p></td>
</tr>
<tr class="even">
<td><p><em>ExpectedTranslatedNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il numero di telefono nel formato che si prevede di voler visualizzare dopo la conversione. È il valore del parametro DialedNumber dopo la normalizzazione. Se si esegue il cmdlet <strong>Test-CsVoiceTestConfiguration</strong> e DialedNumber non risulta uguale al valore in ExpectedTranslatedNumber, il risultato del test sarà negativo (Fail).</p>
<p>Deve contenere al massimo 512 caratteri.</p>
<p>Valore predefinito: +1234</p></td>
</tr>
<tr class="odd">
<td><p><em>ExpectedUsage</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il nome dell'utilizzo PSTN che si prevede di utilizzare durante il test di configurazione. Se viene impiegato un utilizzo PSTN diverso, in base ai criteri vocali e al dial plan di destinazione, il test non riuscirà. Per recuperare gli utilizzi disponibili, chiamare il cmdlet <strong>Get-CsPstnUsage</strong>.</p>
<p>Deve contenere al massimo 256 caratteri.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetDialplan</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>L'identità del dial plan da utilizzare per questo test. Per recuperare i dial plan, chiamare il cmdlet <strong>Get-CsDialPlan</strong>.</p>
<p>Deve contenere al massimo 40 caratteri.</p>
<p>Valore predefinito: Global</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetVoicePolicy</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>L'identità dei criteri vocali su cui eseguire il test. Per recuperare i criteri vocali è possibile chiamare il cmdlet <strong>Get-CsVoicePolicy</strong>.</p>
<p>Deve contenere al massimo 40 caratteri.</p>
<p>Valore predefinito: Global</p></td>
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

Nessuno.

## Tipi restituiti

Questo cmdlet crea un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration

## Vedere anche

#### Ulteriori risorse

[Remove-CsVoiceTestConfiguration](remove-csvoicetestconfiguration.md)  
[Set-CsVoiceTestConfiguration](set-csvoicetestconfiguration.md)  
[Get-CsVoiceTestConfiguration](get-csvoicetestconfiguration.md)  
[Test-CsVoiceTestConfiguration](test-csvoicetestconfiguration.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)  
[Get-CsPstnUsage](get-cspstnusage.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)

