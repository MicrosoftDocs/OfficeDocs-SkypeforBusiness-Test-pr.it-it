---
title: Test-CsVoiceTestConfiguration
TOCTitle: Test-CsVoiceTestConfiguration
ms:assetid: 1c87ef27-0542-49b0-9125-512fd6ed187d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398260(v=OCS.15)
ms:contentKeyID: 49299858
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsVoiceTestConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Esegue configurazioni vocali di test per garantire che il routing e i criteri vocali funzionino come previsto. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsVoiceTestConfiguration -TestCaseInputObject <TestConfiguration> [-Dialplan <LocationProfile>] [-RouteSettings <PstnRoutingSettings>] [-VoicePolicy <VoicePolicy>] <COMMON PARAMETERS>

    Test-CsVoiceTestConfiguration -DialedNumber <String> -Dialplan <LocationProfile> -VoicePolicy <VoicePolicy> [-RouteSettings <PstnRoutingSettings>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>]

## Esempi

## ESEMPIO 1

Con questo esempio viene eseguito un test della configurazione vocale TestConfig1. Per prima cosa viene eseguito il cmdlet **Get-CsVoiceTestConfiguration** per recuperare la configurazione con Identity TestConfig1. Tale oggetto di configurazione viene quindi inviato tramite pipe al cmdlet **Test-CsVoiceTestConfiguration**.

    Get-CsVoiceTestConfiguration -Identity TestConfig1 | Test-CsVoiceTestConfiguration

## ESEMPIO 2

L'Esempio 2 è identico all'Esempio 1, tranne per il fatto che, invece di inviare tramite pipe i risultati dell'operazione Get direttamente al cmdlet Test, l'oggetto viene prima memorizzato nella variabile $a e successivamente viene fornito come valore del parametro TestCaseInputObject per essere utilizzato come configurazione di test.

    $a = Get-CsVoiceTestConfiguration -Identity TestConfig1
    Test-CsVoiceTestConfiguration -TestCaseInputObject $a

## ESEMPIO 3

In questo esempio viene eseguita una configurazione di test senza doverla prima definire con il cmdlet **New-CsVoiceTestConfiguration**. Invece di passare un oggetto TestConfiguration creato in precedenza, in questo esempio viene mostrato come configurare un test "immediato" specificando il numero di telefono da testare, il dial plan e il criterio vocale su cui eseguire il test.

Nella prima riga dell'esempio viene utilizzato il cmdlet **Get-CsDialPlan** per recuperare il dial plan Global. L'oggetto dial plan recuperato viene assegnato alla variabile $dp. Nella seconda riga viene eseguita la stessa operazione con il criterio vocale, utilizzando il cmdlet **Get-CsVoicePolicy** per recuperare il criterio vocale Global e assegnarlo alla variabile $vp.

È infine possibile eseguire il test. Viene perciò chiamato il cmdlet **Test-CsVoiceTestConfiguration**, passando il numero di telefono da testare al parametro DialedNumber, il dial plan recuperato nella riga 1 (archiviato in $dp) al parametro Dialplan e il criterio vocale recuperato nella riga 2 (archiviato in $vp) al parametro VoicePolicy.

Si noti che l'output per l'esempio 3 non includerà lo stato dei risultati previsti. Se si desidera confrontare i risultati ottenuti con quelli previsti, è necessario definire questi ultimi con il cmdlet **New-CsVoiceTestConfiguration** e chiamare il cmdlet **Test-CsVoiceTestConfiguration** come mostrato negli esempi 1 e 2.

    $dp = Get-CsDialPlan -Identity Global
    $vp = Get-CsVoicePolicy -Identity Global
    Test-CsVoiceTestConfiguration -DialedNumber 4255551212 -Dialplan $dp -VoicePolicy $vp

## Descrizione dettagliata

Prima di implementare route vocali e criteri vocali, è buona norma testarli su diversi numeri di telefono per garantire che i risultati siano quelli previsti. L'esecuzione di questo cmdlet con le impostazioni di parametro appropriate consente di eseguire questi test.

Questo cmdlet consente di testare un numero di telefono rispetto alla route vocale, all'utilizzo, al dial plan e ai criteri vocali, per verificare i risultati desiderati o per confrontare il risultato effettivo con quello previsto. Le configurazioni vocali da testare possono essere definite immettendo i parametri appropriati individualmente oppure utilizzando il cmdlet **New-CsVoiceTestConfiguration**.

Se si immettono i valori per i parametri DialedNumber, DialPlan e VoicePolicy, l'output includerà il numero convertito, la regola di normalizzazione utilizzata per creare la conversione, la route utilizzata e l'utilizzo PSTN. Se invece si immette un valore per il parametro TestCaseInputObject, è possibile anche verificare se i risultati ottenuti corrispondono a quelli previsti specificati per l'oggetto test al momento della creazione con il cmdlet **New-CsVoiceTestConfiguration**.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Test-CsVoiceTestConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsVoiceTestConfiguration"}

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
<td><p><em>DialedNumber</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il numero di telefono su cui eseguire il test. Il numero viene normalizzato in base al dial plan, alla route e al criterio, quindi viene visualizzato come output.</p>
<p>Questo parametro è obbligatorio, tranne nel caso in cui sia stato fornito un valore al parametro TestCaseInputObject. Non è possibile specificare sia DialedNumber sia TestCaseInputObject. (TestCaseInputObject contiene già un DialedNumber nell'oggetto).</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Dialplan</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile</p></td>
<td><p>Un riferimento a un oggetto dial plan del dial plan da utilizzare durante l'esecuzione del test. ﻿Per recuperare questi oggetti dial plan è possibile utilizzare il cmdlet <strong>Get-CsDialPlan</strong>.</p>
<p>Questo parametro è obbligatorio se è stato specificato anche il parametro DialedNumber. Non utilizzare questo parametro se si utilizza il parametro TestCaseInputObject. L'oggetto in questo parametro deve corrispondere al dial plan specificato in TestCaseInputObject, pertanto l'uso di questo parametro si rivela ridondante.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>TestCaseInputObject</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration</p></td>
<td><p>Un oggetto contenente un riferimento alla configurazione vocale da testare. Per recuperare questo riferimento oggetto è possibile utilizzare il cmdlet <strong>Get-CsVoiceTestConfiguration</strong>.</p>
<p>Se si utilizza il cmdlet con questo parametro, non è possibile specificare DialedNumber. È preferibile non specificare nemmeno Dialplan o VoicePolicy, in quanto risulterebbero ridondanti rispetto ai valori nell'oggetto configurazione di test vocale.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>VoicePolicy</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoicePolicy</p></td>
<td><p>Un riferimento a un oggetto criterio vocale del criterio vocale da utilizzare durante l'esecuzione del test. Per recuperare gli oggetti criterio vocale è possibile utilizzare il cmdlet <strong>Get-CsVoicePolicy</strong>.</p>
<p>Questo parametro è obbligatorio se è stato specificato anche il parametro DialedNumber. Non utilizzare questo parametro se si utilizza il parametro TestCaseInputObject. L'oggetto in questo parametro deve corrispondere al criterio vocale specificato in TestCaseInputObject, pertanto l'uso di questo parametro si rivela ridondante.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>RouteSettings</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PstnRoutingSettings</p></td>
<td><p>Riferimento a un oggetto contenente tutte le route vocali disponibili nell'installazione di Lync Server. Per recuperare questo oggetto, è possibile utilizzare il cmdlet <strong>Get-CsRoutingConfiguration</strong>.</p>
<p>È possibile utilizzare questo parametro sia con il parametro DialedNumber sia con il parametro TestCaseInputObject.</p>
<p></p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration. Accetta l'input tramite pipeline di un oggetto configurazione di test vocale.

## Tipi restituiti

Questo cmdlet restituisce un oggetto di tipo Microsoft.Rtc.Management.Voice.OcsVoiceTestResult.

## Vedere anche

#### Ulteriori risorse

[New-CsVoiceTestConfiguration](new-csvoicetestconfiguration.md)  
[Remove-CsVoiceTestConfiguration](remove-csvoicetestconfiguration.md)  
[Set-CsVoiceTestConfiguration](set-csvoicetestconfiguration.md)  
[Get-CsVoiceTestConfiguration](get-csvoicetestconfiguration.md)  
[Get-CsDialPlan](get-csdialplan.md)  
[Get-CsVoicePolicy](get-csvoicepolicy.md)  
[Get-CsRoutingConfiguration](get-csroutingconfiguration.md)

