---
title: Set-CsVoiceTestConfiguration
TOCTitle: Set-CsVoiceTestConfiguration
ms:assetid: 7b95fc95-ec0e-4bb3-aed1-e8b72e305999
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398614(v=OCS.15)
ms:contentKeyID: 49301090
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceTestConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica uno scenario di test utilizzabile per verificare i numeri di telefono rispetto a route e regole specificate. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsVoiceTestConfiguration [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceTestConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-DialedNumber <String>] [-ExpectedRoute <String>] [-ExpectedTranslatedNumber <String>] [-ExpectedUsage <String>] [-Force <SwitchParameter>] [-TargetDialplan <String>] [-TargetVoicePolicy <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con questo esempio il numero composto della configurazione di test vocale per TestConfig1 viene impostato su 14255551212. È il numero che verrà controllato rispetto al criterio vocale e alla route per garantire che la normalizzazione avvenga come previsto e per garantire l'applicazione delle route e dei dial plan corretti.

    Set-CsVoiceTestConfiguration -Identity TestConfig1 -DialedNumber 14255551212

## ESEMPIO 2

Con questo esempio vengono modificate le impostazioni per la configurazione di test vocale TestConfig1. Il comando imposta TargetDialplan sul dial plan per site:Redmond1. Dal momento che una modifica al dial plan comporta un cambiamento nelle regole di normalizzazione, è stato modificato anche ExpectedTranslationNumber per riflettere quanto ci si aspetta dalle regole di normalizzazione per tale dial plan.

    Set-CsVoiceTestConfiguration -Identity TestConfig1 -TargetDialplan site:Redmond1 -ExpectedTranslatedNumber "+912065551212"

## Descrizione dettagliata

Prima di implementare route vocali e criteri vocali, è buona norma testarli su diversi numeri di telefono per garantire che i risultati siano quelli previsti. Per farlo è possibile modificare gli scenari di test con questo cmdlet.

Il cmdlet **Set-CsVoiceTestConfiguration** consente di modificare la route vocale, l'utilizzo, il profilo di località, il profilo di numerazione locale (dial plan) e il criterio vocale rispetto a cui testare un numero di telefono specificato. Tutte queste informazioni possono essere definite e recuperate utilizzando altri cmdlet, come specificato nelle descrizioni dei parametri per questo argomento.

Per testare le configurazioni modificate con questo cmdlet è possibile utilizzare il cmdlet **Test-CsVoiceTestConfiguration**.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsVoiceTestConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceTestConfiguration"}

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
<td><p>SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DialedNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Il numero di telefono da utilizzare per testare criteri, utilizzi e così via.</p>
<p>Deve contenere al massimo 512 caratteri.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExpectedRoute</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Il nome della route vocale che si prevede di utilizzare durante il test di configurazione. Se viene utilizzata una route diversa, basata sul dial plan di destinazione e sul criterio vocale, il test non riesce. Per recuperare le route vocali disponibili, utilizzare il cmdlet <strong>Get-CsVoiceRoute</strong>.</p>
<p>Deve contenere al massimo 256 caratteri.</p></td>
</tr>
<tr class="even">
<td><p><em>ExpectedTranslatedNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Il numero di telefono nel formato che si desidera dopo la conversione. È il valore del parametro DialedNumber dopo la normalizzazione. Se si esegue il cmdlet <strong>Test-CsVoiceTestConfiguration</strong> e DialedNumber non risulta uguale al valore di ExpectedTranslatedNumber, il risultato del test sarà Fail.</p>
<p>Deve contenere al massimo 512 caratteri.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExpectedUsage</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Il nome dell'utilizzo PSTN che si prevede di utilizzare durante il test di configurazione. Se viene implementato un diverso utilizzo PSTN, basato sul dial plan di destinazione e sul criterio vocale, il test non riesce. Per recuperare gli utilizzi disponibili, chiamare il cmdlet <strong>Get-CsPstnUsage</strong>.</p>
<p>Deve contenere al massimo 256 caratteri.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>Una stringa che identifica in modo univoco lo scenario di test da modificare.</p>
<p>Il valore di questo parametro non include l'ambito perché l'oggetto può essere creato solo con ambito globale. Di conseguenza è richiesto solo il nome.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>TestConfiguration</p></td>
<td><p>Un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration che contiene una configurazione di test vocale esistente con le modifiche che si desidera apportare a tale configurazione. Un oggetto di questo tipo può essere recuperato utilizzando il cmdlet <strong>Get-CsVoiceTestConfiguraton</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetDialplan</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'identità del dial plan da utilizzare per il test. Per recuperare i dial plan, utilizzare il cmdlet <strong>Get-CsDialPlan</strong>.</p>
<p>Deve contenere al massimo 40 caratteri.</p></td>
</tr>
<tr class="even">
<td><p><em>TargetVoicePolicy</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'identità del criterio vocale per cui eseguire il test. Per recuperare i criteri vocali, chiamare il cmdlet <strong>Get-CsVoicePolicy</strong>.</p>
<p>Deve contenere al massimo 40 caratteri.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration. Accetta l'input tramite pipeline di oggetti configurazione di test vocale.

## Tipi restituiti

Questo cmdlet restituisce un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsVoiceTestConfiguration](new-csvoicetestconfiguration.md)  
[Remove-CsVoiceTestConfiguration](remove-csvoicetestconfiguration.md)  
[Get-CsVoiceTestConfiguration](get-csvoicetestconfiguration.md)  
[Test-CsVoiceTestConfiguration](test-csvoicetestconfiguration.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)  
[Get-CsPstnUsage](get-cspstnusage.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)

