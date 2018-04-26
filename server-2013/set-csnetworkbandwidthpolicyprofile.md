---
title: Set-CsNetworkBandwidthPolicyProfile
TOCTitle: Set-CsNetworkBandwidthPolicyProfile
ms:assetid: 519916b9-d5a0-476e-a516-9b8a3058daf2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398338(v=OCS.15)
ms:contentKeyID: 49300571
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkBandwidthPolicyProfile

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un profilo dei criteri di larghezza di banda di rete esistente. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsNetworkBandwidthPolicyProfile [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkBandwidthPolicyProfile [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AudioBWLimit <String>] [-AudioBWSessionLimit <String>] [-BWPolicy <PSListModifier>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-VideoBWLimit <String>] [-VideoBWSessionLimit <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio viene modificata la descrizione del profilo dei criteri di larghezza di banda con identità LowBWProfile. A tale scopo, viene chiamato il cmdlet **Set-CsNetworkBandwidthPolicyProfile** con due parametri: Identity, che specifica il nome del profilo da modificare, e Description, che specifica la nuova descrizione del profilo.

    Set-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile -Description "Policy for links of less than 10MB"

## ESEMPIO 2

Nell'esempio 2 vengono modificate le limitazioni complessive e per sessione delle trasmissioni video per il profilo dei criteri di larghezza di banda con Identity LowBWLimit. Una volta specificato il parametro Identity del profilo da modificare, viene utilizzato il parametro VideoBWLimit per impostare la limitazione video complessiva su 2500. Viene quindi utilizzato il parametro VideoBWSessionLimit per impostare la limitazione per sessione su 300. Questo comando consente di aggiungere un profilo o aggiornare un profilo video esistente per il profilo dei criteri di larghezza di banda LowBWLimit. I profili audio esistenti non subiranno modifiche.

    Set-CsNetworkBandwidthPolicyProfile -Identity LowBWLimit -VideoBWLimit 2500 -VideoBWSessionLimit 300

## ESEMPIO 3

In questo esempio viene creato un nuovo criterio di larghezza di banda, poi assegnato al profilo dei criteri di larghezza di banda con identità LowBWLimit. La prima riga dell'esempio è una chiamata al cmdlet **New-CsNetworkBWPolicy**. Questo cmdlet crea un nuovo profilo, in questo caso un profilo video (-BWPolicyModality video) con un limite complessivo di 5000 kbps (-BWLimit 5000) e un limite per sessione di 200 kbps (-BWSessionLimit 200). Questo nuovo oggetto profilo viene archiviato nella variabile $bp. Nella riga successiva dell'esempio viene chiamato il cmdlet **Set-CsNetworkBandwidthPolicyProfile** per modificare il profilo LowBWLimit (-Identity LowBWLimit). Viene utilizzato il parametro BWPolicy con il valore $bp. Questo parametro sostituisce tutti i criteri esistenti del profilo con il criterio appena creato e archiviato nella variabile $bp.

    $bp = New-CsNetworkBWPolicy -BWLimit 5000 -BWSessionLimit 200 -BWPolicyModality video
    Set-CsNetworkBandwidthPolicyProfile -Identity LowBWLimit -BWPolicy $bp

## ESEMPIO 4

Nell'esempio 4 viene aggiunto un nuovo criterio di larghezza di banda audio alla serie di criteri esistenti nel profilo LowBWProfile. Nella riga 1 viene chiamato il cmdlet **Get-CsNetworkBandwidthPolicyProfile** per recuperare il profilo con identità LowBWProfile. Tale profilo viene archiviato nella variabile $a. Nella riga successiva viene chiamato il cmdlet **New-CsNetworkBWPolicy** per creare un nuovo criterio di larghezza di banda. Si tratta di un criterio audio (-BWPolicyModality audio) con un limite complessivo di 2000 kbps (-BWLimit 2000) e un limite per sessione di 300 kbps (-BWSessionLimit 300). Questo nuovo criterio viene archiviato nella variabile $ap.

Nella riga 3 il nuovo criterio audio, archiviato in $ap, viene aggiunto al profilo recuperato nella riga 1 e archiviato nella variabile $a. Questa operazione viene eseguita chiamando il metodo Add della proprietà BWPolicy del profilo e passando un valore $ap. Ciò viene letto come "Aggiungi il nuovo criterio archiviato in $ap a BWPolicy del profilo LowBWProfile, archiviato in $a".

Viene infine chiamato il cmdlet **Set-CsNetworkBandwidthPolicyProfile** per aggiornare il profilo LowBWProfile. Viene utilizzato il parametro Instance passando un valore $a, che contiene il profilo modificato.

    $a = Get-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile
    $ap = New-CsNetworkBWPolicy -BWLimit 2000 -BWSessionLimit 300 -BWPolicyModality audio
    $a.BWPolicy.Add($ap)
    Set-CsNetworkBandwidthPolicyProfile -Instance $a

## ESEMPIO 5

L'esempio 5 produce gli stessi effetti dell' esempio 4: consente di aggiungere un nuovo profilo audio all'elenco dei criteri esistente del profilo LowBWProfile. Questo metodo richiede un numero minore di righe, ma è possibile che non sia altrettanto chiaro. È stato aggiunto al solo scopo di dimostrare che è possibile eseguire la stessa operazione in modi differenti.

Nella riga 1 viene creato un nuovo criterio di larghezza di banda audio, impostando un limite complessivo (2000) e un limite per sessione (300), quindi archiviando il nuovo oggetto nella variabile $ap. Viene quindi chiamato il cmdlet **Set-CsNetworkBandwidthPolicyProfile** per modificare il profilo con identità LowBWProfile. Per modificare l'elenco dei criteri all'interno del profilo viene utilizzato il parametro BWPolicy. Si noti il valore passato a questo parametro: @{add=$ap}. In Windows PowerShell questo è un modo per aggiungere un elemento a un elenco. Il valore inizia con un segno @, seguito da un gruppo di parentesi graffe {}. All'interno delle parentesi graffe è necessario specificare l'azione che si desidera eseguire sull'elenco. In questo caso si desidera aggiungere un elemento. È anche possibile rimuovere o sostituire gli elementi esistenti. Viene inserita l'azione (add) seguita da un segno di uguale, seguito dall'oggetto che si desidera aggiungere all'elenco, in questo caso il nuovo criterio archiviato nella variabile $ap.

    $ap = New-CsNetworkBWPolicy -BWLimit 2000 -BWSessionLimit 300 -BWPolicyModality audio
    Set-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile -BWPolicy @{add=$ap}

## Descrizione dettagliata

Come parte del controllo di ammissione di chiamata, viene utilizzato un criterio di larghezza di banda per definire le limitazioni relative alla larghezza di banda per alcune modalità. In Lync Server possono essere assegnate limitazioni della larghezza di banda solo alle modalità audio e video. Questo cmdlet modifica un profilo contenitore di questi criteri.

IMPORTANTE: se in un profilo sono presenti più criteri (ad esempio, un criterio audio e un criterio video), la modifica del profilo tramite l'utilizzo delle proprietà AudioBWLimit, AudioBWSessionLimit, VideoBWLimit o VideoBWSessionLimit rimuove tutti i criteri presenti nel profilo e li sostituisce con i nuovi valori. Se il profilo conteneva un criterio per la limitazione della modalità video e si imposta solo il parametro AudioBWLimit, il criterio video viene rimosso e viene creato un criterio audio.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Set-CsNetworkBandwidthPolicyProfile** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkBandwidthPolicyProfile"}

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
<td><p><em>AudioBWLimit</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Larghezza di banda massima per tutte le connessioni audio. Se una singola sessione audio supera la limitazione della larghezza di banda audio, tale sessione non viene avviata.</p>
<p>Espressa in kbps. Ad esempio, un valore pari a 1000 equivale a 1000 kbps.</p>
<p>Se si fornisce un valore per questo parametro, non sarà possibile specificare un valore per il parametro BWPolicy.</p>
<p>Valore predefinito: Se si specifica un valore per il parametro AudioBWSessionLimit, ma non per AudioBWLimit, il valore predefinito di quest'ultimo sarà 0.</p></td>
</tr>
<tr class="even">
<td><p><em>AudioBWSessionLimit</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Larghezza di banda massima per sessione audio. Espressa in kbps. Il valore deve essere pari a 40 o superiore.</p>
<p>Se si fornisce un valore per questo parametro, non sarà possibile specificare un valore per il parametro BWPolicy.</p>
<p>Valore predefinito: se si specifica un valore per il parametro AudioBWLimit, ma non per AudioBWSessionLimit, il valore predefinito di quest'ultimo sarà 175.</p></td>
</tr>
<tr class="odd">
<td><p><em>BWPolicy</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>Un elenco di oggetti contenente i profili dei criteri di larghezza di banda. Ciascun oggetto dell'elenco è composto di una modalità di larghezza di banda, audio o video, una limitazione della larghezza di banda complessiva e una limitazione per sessione della larghezza di banda.</p>
<p>Se si fornisce un valore per questo parametro, non sarà possibile specificare un valore per il parametro AudioBWLimit, AudioBWSessionLimit, VideoBWLimit o VideoBWSessionLimit.</p>
<p>Gli oggetti nell'elenco devono essere di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyType. Gli oggetti di questo tipo possono essere creati chiamando il cmdlet <strong>New-CsNetworkBWPolicy</strong>; è quindi possibile aggiungere il criterio risultante da questa operazione al profilo esistente, assegnando il nuovo profilo come valore a questo parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Descrizione del profilo dei criteri di larghezza di banda. Ad esempio, è possibile utilizzare questo parametro per indicare l'utilizzo previsto del profilo.</p></td>
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
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>Valore stringa che identifica in modo univoco il profilo dei criteri di larghezza di banda che si desidera modificare. Questo valore è identico alla proprietà BWPolicyProfileID del profilo e può essere modificato tramite la modifica del valore di questa proprietà. Ciò equivale a eseguire un'operazione di &quot;Taglia e incolla&quot;: tutte le proprietà del profilo vengono mantenute e viene modificato solo il nome. Tuttavia, questo valore non può essere modificato, se il profilo è assegnato a un sito.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>BWPolicyProfileType</p></td>
<td><p>Riferimento a un oggetto profilo dei criteri di larghezza di banda (un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType) che contiene le impostazioni che si desidera utilizzare per modificare il profilo. Questo oggetto può essere recuperato chiamando il cmdlet <strong>Get-CsNetworkBandwidthPolicyProfile</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoBWLimit</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Larghezza di banda massima per tutte le connessioni video. Se una singola sessione video supera la limitazione della larghezza di banda video, tale sessione non viene avviata.</p>
<p>Espressa in kbps. Ad esempio, un valore pari a 1000 equivale a 1000 kbps.</p>
<p>Se si fornisce un valore per questo parametro, non sarà possibile specificare un valore per il parametro BWPolicy.</p>
<p>Valore predefinito: se si specifica un valore per il parametro VideoBWSessionLimit, ma non per VideoBWLimit, il valore predefinito di quest'ultimo sarà 0.</p></td>
</tr>
<tr class="even">
<td><p><em>VideoBWSessionLimit</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Larghezza di banda massima per sessione video. Espressa in kbps. Il valore deve essere pari a 100 o superiore.</p>
<p>Se si fornisce un valore per questo parametro, non sarà possibile specificare un valore per il parametro BWPolicy.</p>
<p>Valore predefinito: se si specifica un valore per il parametro VideoBWLimit, ma non per VideoBWSessionLimi, il valore predefinito di quest'ultimo sarà 700.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType. Consente di accettare l'input da pipeline di oggetti profilo di larghezza di banda di rete.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Consente di modificare un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType.

## Vedere anche

#### Ulteriori risorse

[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Remove-CsNetworkBandwidthPolicyProfile](remove-csnetworkbandwidthpolicyprofile.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkBWPolicy](new-csnetworkbwpolicy.md)

