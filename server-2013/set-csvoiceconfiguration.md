---
title: Set-CsVoiceConfiguration
TOCTitle: Set-CsVoiceConfiguration
ms:assetid: dbab35ac-9a55-41d2-a726-9a26b2ff8e85
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398967(v=OCS.15)
ms:contentKeyID: 49302173
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoiceConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un elenco di configurazioni di test vocali. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsVoiceConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoiceConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-VoiceTestConfigurations <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Per modificare una configurazione di test vocale all'interno di una configurazione vocale sono necessari diversi passaggi. In questo esempio, si inizia recuperando l'oggetto configurazione vocale chiamando il cmdlet **Get-CsVoiceConfiguration**. L'oggetto recuperato (sarà solo uno) viene assegnato alla variabile $a.

Nella riga 2 di questo esempio viene recuperato dalla variabile $a il contenuto della proprietà VoiceTestConfigurations, che è una raccolta di oggetti di configurazione di test vocale. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che cerca nella raccolta stessa l'oggetto di configurazione di test vocale con nome uguale alla stringa TestConfig2. Tale oggetto viene assegnato alla variabile $b.

Successivamente, l'oggetto configurazione di test vocale TestConfig2 viene modificato assegnando nuovi valori alle proprietà DialedNumber e ExpectedTranslatedNumber. Aggiornando l'oggetto viene aggiornato anche l'oggetto nella variabile $a, che tuttavia rimane ancora solo in memoria. Per ultimo, è necessario salvare le modifiche passando $a al parametro Instance del cmdlet **Set-CsVoiceConfiguration**.

Questo non è il modo consigliato per modificare una configurazione vocale. Per modificare una configurazione di test vocale, modificare semplicemente le singole configurazioni di test vocale con il cmdlet **Set-CsVoiceTestConfiguration**, come mostrato di seguito:

Set-CsVoiceTestConfiguration -Identity TestConfig2 -DialedNumber 5551212 -ExpectedTranslatedNumber +5551212

Questa unica riga permette di eseguire le stesse operazioni mostrate nell'esempio 1.

    $a = Get-CsVoiceConfiguration
    $b = $a.VoiceTestConfigurations | Where-Object {$_.Name -eq "TestConfig2"}
    $b.DialedNumber = "5551212"
    $b.ExpectedTranslatedNumber = "+5551212"
    Set-CsVoiceConfiguration -Instance $a

## Descrizione dettagliata

Le configurazioni di test vocali sono utilizzate per testare un numero di telefono a fronte di criteri vocali, route e dial plan specifici. Questo cmdlet può essere utilizzato per modificare le configurazioni di test vocali da un elenco contenente tutte le configurazioni di test vocali per una distribuzione di Lync Server.

Questo cmdlet modifica un oggetto di tipo VoiceConfiguration. Questo oggetto è semplicemente un oggetto contenitore per configurazioni di test vocali. Pertanto, l'uso di questo cmdlet non è consigliato. Per modificare le configurazioni vocali, modificare le singole configurazioni di test vocale chiamando il cmdlet**Set-CsVoiceTestConfiguration**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsVoiceConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoiceConfiguration"}

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
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>XdsIdentity</p></td>
<td><p>L'ambito di questo oggetto. L'unico valore possibile per questo parametro è Global.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>VoiceConfiguration</p></td>
<td><p>Un riferimento per un oggetto configurazione vocale (Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceConfiguration). Un oggetto di questo tipo può essere recuperato chiamando il cmdlet <strong>Get-CsVoiceConfiguration</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>VoiceTestConfigurations</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>Un elenco di tutte le configurazioni di test vocali (oggetti Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration) definite per la distribuzione di Lync Server.</p>
<p>È possibile modificare i singoli oggetti di configurazione di test vocale utilizzando il cmdlet <strong>Set-CsVoiceTestConfiguration</strong>. Questa è la modalità consigliata per modificare le configurazioni in questo elenco.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceConfiguration. Il cmdlet **Set-CsVoiceConfiguration** accetta l'input da pipeline di un oggetto di configurazione vocale.

## Tipi restituiti

Il cmdlet **Set-CsVoiceConfiguration** non restituisce un valore o un oggetto. Il cmdlet configura piuttosto le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceConfiguration.

## Vedere anche

#### Ulteriori risorse

[Remove-CsVoiceConfiguration](remove-csvoiceconfiguration.md)  
[Get-CsVoiceConfiguration](get-csvoiceconfiguration.md)  
[New-CsVoiceTestConfiguration](new-csvoicetestconfiguration.md)  
[Set-CsVoiceTestConfiguration](set-csvoicetestconfiguration.md)  
[Get-CsVoiceTestConfiguration](get-csvoicetestconfiguration.md)

