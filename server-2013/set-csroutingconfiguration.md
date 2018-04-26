---
title: Set-CsRoutingConfiguration
TOCTitle: Set-CsRoutingConfiguration
ms:assetid: ab69c6e8-262a-4ecb-b1af-513383c494fe
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412811(v=OCS.15)
ms:contentKeyID: 49301635
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsRoutingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un elenco di route vocali. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsRoutingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsRoutingConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-EnableLocationBasedRouting <$true | $false>] [-Force <SwitchParameter>] [-Route <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

È necessario eseguire diverse operazioni per modificare una route vocale in una configurazione di routing. In questo esempio viene recuperato innanzitutto l'oggetto configurazione di routing mediante una chiamata al cmdlet **Get-CsRoutingConfiguration**. L'oggetto recuperato (sarà solo uno) viene assegnato alla variabile $a.

Nella riga 2 dell'esempio viene recuperato il contenuto della proprietà Route dalla variabile $a, che è una raccolta di oggetti route vocale. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, in cui vengono cercati nella raccolta tutti gli oggetti route vocale la cui proprietà Name corrisponde alla stringa LocalRoute. Tale oggetto viene assegnato alla variabile $b.

Successivamente l'oggetto route vocale LocalRoute viene modificato con l'assegnazione del valore $False alla proprietà SuppressCallerId. Aggiornando l'oggetto viene aggiornato anche l'oggetto nella variabile $a, che tuttavia rimane ancora solo in memoria. Nell'ultimo passaggio è necessario salvare le modifiche passando la variabile $a al parametro Instance del cmdlet **Set-CsRoutingConfiguration**.

Questo non è il metodo consigliato per la modifica di una configurazione di routing. Per modificare una configurazione di routing, è sufficiente modificare le singole route vocali con il cmdlet **Set-CsVoiceRoute**, come illustrato di seguito:

Set-CsVoiceRoute -Identity LocalRoute -SuppressCallerId $False

Questa unica riga permette di eseguire le stesse operazioni mostrate nell'esempio 1.

    $a = Get-CsRoutingConfiguration
    $b = $a.Route | Where-Object {$_.Name -match "LocalRoute"}
    $b.SuppressCallerId = $False
    Set-CsRoutingConfiguration -Instance $a

## Descrizione dettagliata

Le route vocali includono istruzioni che indicano a Lync Server come instradare le chiamate effettuate da utenti di VoIP aziendale ai numeri di telefono della rete PSTN (Public Switched Telephone Network) o di un centralino (PBX, Private Branch Exchange). Con questo cmdlet è possibile modificare le impostazioni di qualsiasi route vocale definita all'interno di una distribuzione di Lync Server.

L'utilizzo di questo cmdlet non è consigliato. Per modificare le configurazioni di routing, modificare le singole route vocali chiamando il cmdlet **Set-CsVoiceRoute**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsRoutingConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsRoutingConfiguration"}

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
<td><p><em>EnableLocationBasedRouting</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se impostato su True, il routing vocale verrà gestito tenendo conto della posizione sia dell'utente che effettua la chiamata che dell'utente che la riceve. Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>XdsIdentity</p></td>
<td><p>L'ambito della configurazione di routing. Questo valore deve essere Global.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PstnRoutingSettings</p></td>
<td><p>Oggetto configurazione di routing (Microsoft.Rtc.Management.WritablConfig.Policy.Voice.PstnRoutingSettings). Un oggetto di questo tipo può essere recuperato chiamando il cmdlet <strong>Get-CsRoutingConfiguration</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Route</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>Elenco di tutte le route vocali (oggetti Microsoft.Rtc.Management.WritableConfig.Policy.Voice.Route) definite per la distribuzione di Lync Server.</p>
<p>Per modificare i singoli oggetti route vocale è possibile utilizzare il cmdlet <strong>Set-CsVoiceRoute</strong>. Questo è il metodo consigliato per la modifica delle route in questo elenco.</p></td>
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

Oggetto Microsoft.Rtc.WritableConfig.Management.Policy.Voice.PSTNRoutingSettings. Accetta l'input da pipeline di un oggetto di configurazione di routing.

## Tipi restituiti

Il cmdlet **Set-CsRoutingConfiguration** non restituisce alcun oggetto o valore. Configura invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PstnRoutingSettings.

## Vedere anche

#### Ulteriori risorse

[New-CsRoutingConfiguration](new-csroutingconfiguration.md)  
[Remove-CsRoutingConfiguration](remove-csroutingconfiguration.md)  
[Get-CsRoutingConfiguration](get-csroutingconfiguration.md)  
[Set-CsVoiceRoute](set-csvoiceroute.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)

