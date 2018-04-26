---
title: New-CsNetworkBandwidthPolicyProfile
TOCTitle: New-CsNetworkBandwidthPolicyProfile
ms:assetid: 84940891-37a6-45fc-972d-05b95aa71ba9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398675(v=OCS.15)
ms:contentKeyID: 49301194
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkBandwidthPolicyProfile

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo profilo dei criteri di larghezza di banda di rete. Questo cmdlet può essere inoltre utilizzato per impostare i criteri di larghezza di banda all'interno del profilo. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsNetworkBandwidthPolicyProfile -Identity <XdsGlobalRelativeIdentity> [-AudioBWLimit <String>] [-AudioBWSessionLimit <String>] [-BWPolicy <PSListModifier>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-VideoBWLimit <String>] [-VideoBWSessionLimit <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene creato un nuovo profilo dei criteri di larghezza di banda denominato LowBWLimits. A questo nuovo profilo verranno assegnati due criteri, un criterio audio e un criterio video (gli unici due criteri consentiti in Lync Server). Il criterio audio viene aggiunto al profilo utilizzando il parametro AudioBWLimit per assegnare un limite, in questo caso, di 2000 kbps alle connessioni audio complessive e il parametro AudioBWSessionLimit per assegnare un limite di 200 kbps per le singole sessioni audio. La stessa operazione viene eseguita per creare i limiti delle sessioni video, utilizzando però i parametri VideoBWLimit e VideoBWSessionLimit.

    New-CsNetworkBandwidthPolicyProfile -Identity LowBWLimits -AudioBWLimit 2000 -AudioBWSessionLimit 200 -VideoBWLimit 1400 -VideoBWSessionLimit 500

## Descrizione dettagliata

In Controllo di ammissione di chiamata (CAC) i criteri di larghezza di banda vengono utilizzati per definire le limitazioni della larghezza di banda per alcune modalità. In Lync Server è possibile assegnare limitazioni della larghezza di banda solo alle modalità audio e video. Questo cmdlet crea un profilo contenitore per questo tipo di criteri. Definire i singoli criteri nel contenitore specificando le limitazioni della larghezza di banda audio e video quando si chiama il cmdlet.

I profili dei criteri di larghezza di banda vengono applicati ai siti della rete chiamando il cmdlet **New-CsNetworkSite** o **Set-CsNetworkSite**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsNetworkBandwidthPolicyProfile** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkBandwidthPolicyProfile"}

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
<td><p>Un valore stringa che identifica in modo univoco il criterio. Tutte i profili dei criteri di larghezza di banda creati con ambito globale. L'ambito è pertanto univoco ed è necessario specificare solo un nome univoco, quando si crea un nuovo profilo dei criteri di larghezza di banda. Si noti che questo valore viene inserito anche nella proprietà BWPolicyProfileID del profilo.</p></td>
</tr>
<tr class="even">
<td><p><em>AudioBWLimit</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Larghezza di banda massima per tutte le connessioni audio. Se una singola sessione audio supera la limitazione della larghezza di banda audio, tale sessione non viene avviata.</p>
<p>Espressa in kbps. Ad esempio, un valore pari a 1000 equivale a 1000 kbps.</p>
<p>Se si fornisce un valore per questo parametro, non sarà possibile specificare un valore per il parametro BWPolicy.</p>
<p>Valore predefinito: se si specifica un valore per il parametro AudioBWSessionLimit, ma non per AudioBWLimit, per impostazione predefinita per AudioBWLimit verrà utilizzato il valore 0.</p></td>
</tr>
<tr class="odd">
<td><p><em>AudioBWSessionLimit</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Larghezza di banda massima per sessione audio. Espressa in kbps. Il valore deve essere uguale o maggiore di 40.</p>
<p>Se si fornisce un valore per questo parametro, non sarà possibile specificare un valore per il parametro BWPolicy.</p>
<p>Valore predefinito: se si specifica un valore per il parametro AudioBWLimit, ma non per AudioBWSessionLimit, per impostazione predefinita per AudioBWSessionLimit verrà utilizzato il valore 175.</p></td>
</tr>
<tr class="even">
<td><p><em>BWPolicy</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Un elenco di oggetti contenente i profili dei criteri di larghezza di banda. Ciascun oggetto dell'elenco è composto di una modalità di larghezza di banda, audio o video, una limitazione della larghezza di banda complessiva e una limitazione per sessione della larghezza di banda.</p>
<p>Se si fornisce un valore per questo parametro, non sarà possibile specificare un valore per il parametro AudioBWLimit, AudioBWSessionLimit, VideoBWLimit o VideoBWSessionLimit.</p>
<p>Gli oggetti nell'elenco possono essere creati chiamando il cmdlet <strong>New-CsNetworkBWPolicy</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Descrizione del profilo dei criteri di larghezza di banda. Ad esempio, è possibile utilizzare questo parametro per indicare l'utilizzo previsto del profilo.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoBWLimit</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Larghezza di banda massima per tutte le connessioni video. Se una singola sessione video supera la limitazione della larghezza di banda video, tale sessione non viene avviata.</p>
<p>Espressa in kbps. Ad esempio, un valore pari a 1000 equivale a 1000 kbps.</p>
<p>Se si fornisce un valore per questo parametro, non sarà possibile specificare un valore per il parametro BWPolicy.</p>
<p>Valore predefinito: se si specifica un valore per il parametro VideoBWSessionLimit, ma non per VideoBWLimit, per impostazione predefinita per VideoBWLimit verrà utilizzato il valore 0.</p></td>
</tr>
<tr class="even">
<td><p><em>VideoBWSessionLimit</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Larghezza di banda massima per sessione video. Espressa in kbps. Il valore deve essere pari a 100 o superiore.</p>
<p>Se si fornisce un valore per questo parametro, non sarà possibile specificare un valore per il parametro BWPolicy.</p>
<p>Valore predefinito: se si specifica un valore per il parametro VideoBWLimit, ma non per VideoBWSessionLimit, per impostazione predefinita per VideoBWSessionLimit verrà utilizzato il valore 700.</p></td>
</tr>
<tr class="odd">
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

Consente di creare un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType.

## Vedere anche

#### Ulteriori risorse

[Remove-CsNetworkBandwidthPolicyProfile](remove-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkBWPolicy](new-csnetworkbwpolicy.md)

