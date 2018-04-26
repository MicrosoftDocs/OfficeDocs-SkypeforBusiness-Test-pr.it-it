---
title: Set-CsNetworkSite
TOCTitle: Set-CsNetworkSite
ms:assetid: 221a099c-72c4-4eb0-8812-6b2b7639a9ee
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398295(v=OCS.15)
ms:contentKeyID: 49299917
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkSite

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un sito di rete esistente che è stato definito per il servizio Controllo di ammissione di chiamata o per servizio di chiamate di emergenza Enhanced 9-1-1 (E9-1-1). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsNetworkSite [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkSite [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BWPolicyProfileID <String>] [-BypassID <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-EnableLocationBasedRouting <$true | $false>] [-Force <SwitchParameter>] [-LocationPolicy <String>] [-NetworkRegionID <String>] [-VoiceRoutingPolicy <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con questo esempio viene modificato il sito di rete denominato Vancouver. Il nome del sito da modificare viene specificato come valore del parametro Identity. Il sito Vancouver viene spostato in una nuova area geografica, in questo caso Canada, quindi è necessario modificare il parametro NetworkRegionID. Dal momento che è stato fornito un NetworkRegionID ma che non è stato specificato un valore per BypassID, il valore di BypassID viene generato automaticamente. Un eventuale ID di bypass esistente sarà sovrascritto.

    Set-CsNetworkSite -Identity Vancouver -NetworkRegionID Canada

## ESEMPIO 2

Con l'esempio 2 viene modificato il profilo dei criteri di larghezza di banda associato al sito Vancouver. Il nome del sito viene specificato come valore del parametro Identity. Viene quindi specificato un valore per il parametro BWPolicyProfileID: LowBWLimits. Per questo sito saranno utilizzati i criteri associati a tale profilo.

    Set-CsNetworkSite -Identity Vancouver - BWPolicyProfileID LowBWLimits

## Descrizione dettagliata

I siti di rete sono gli uffici o le località configurate in ogni area geografica di una distribuzione CAC o E9-1-1. Questo cmdlet consente di modificare le impostazioni di un sito esistente, ad esempio l'area a cui è associato il sito, la descrizione del sito e il profilo dei criteri di larghezza di banda associato.

Utenti autorizzati a eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati ad eseguire il cmdlet **Set-CsNetworkSite** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkSite"}

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
<td><p><em>BWPolicyProfileID</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Identità del profilo dei criteri per la larghezza di banda che definirà le limitazioni per questo sito. È possibile recuperare un elenco dei profili disponibili chiamando il cmdlet <strong>Get-CsNetworkBandwidthPolicyProfile</strong>.</p>
<p>Se si specifica un valore per questo parametro, è necessario specificare anche un valore per il parametro NetworkRegionID.</p></td>
</tr>
<tr class="even">
<td><p><em>BypassID</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Identificatore univoco globale (GUID). Questo GUID viene utilizzato per mappare i siti di rete alle impostazioni di bypass multimediale in una configurazione di rete di Controllo di ammissione di chiamata o E9-1-1. Utilizzare questo valore BypassID nella chiamata al cmdlet <strong>New-CsNetworkMediaBypassConfiguration</strong>.</p>
<p>Se si specifica un valore per questo parametro, è necessario specificare anche un valore per il parametro NetworkRegionID. Se non si specifica un valore per questo parametro ma si specifica un NetworkRegionID, viene generato automaticamente un BypassID.</p>
<p>Se si specifica un valore in modo esplicito, il valore deve essere nel formato GUID (ad esempio, 3b24a047-dce6-48b2-9f20-9fbff17ed62a). È consigliabile specificare un valore per NetworkRegionID e consentire la generazione automatica del valore BypassID. Se si immette un valore manualmente, verrà visualizzata una richiesta di conferma per verificare che l'utente non desideri la generazione automatica del valore.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Stringa che descrive il sito. Questo parametro può essere utilizzato per fornire una spiegazione dello scopo o della posizione del sito più descrittiva di quanto non possa essere espresso con il solo parametro Identity.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableLocationBasedRouting</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Quando questo parametro è impostato su True, il routing vocale viene gestito considerando sia la posizione dell'utente che effettua la chiamata sia la posizione dell'utente che riceve la chiamata. Il valore predefinito è False.</p></td>
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
<td><p>Identificatore univoco del sito di rete da modificare. I siti vengono creati solo nell'ambito globale, pertanto non è necessario specificare un ambito. In realtà, è sufficiente specificare l'ID del sito di rete.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>DisplayNetworkSiteType</p></td>
<td><p>Riferimento a un oggetto sito di rete (un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType). Questo oggetto può essere recuperato chiamando il cmdlet <strong>Get-CsNetworkSite</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocationPolicy</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Nome dei criteri percorso associati a questo sito. I criteri percorso assegnano specifiche impostazioni per le chiamate di emergenza al sito. Per recuperare un elenco dei criteri percorso, chiamare il cmdlet <strong>Get-CsLocationPolicy</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'identità dell'area di rete a cui è associato questo sito. Questo parametro deve contenere un valore se si desidera fornire un BypassID (manualmente o tramite la generazione automatica) o se la proprietà EnableBandwidthPolicyCheck della configurazione della rete è impostata su True. È possibile recuperare le impostazioni di configurazione della rete chiamando il cmdlet <strong>Get-CsNetworkConfiguration</strong>.</p>
<p>Se in questo sito esiste già un BypassID e non si specifica un valore per il parametro BypassID, il BypassID esistente viene sovrascritto da un BypassID generato automaticamente.</p></td>
</tr>
<tr class="odd">
<td><p><em>VoiceRoutingPolicy</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Criterio di routing vocale per utente da assegnare al sito. Ad esempio:</p>
<p>-VoiceRoutingPolicy &quot;RedmondVoiceRouting”</p>
<p>Si noti che è necessario specificare un criterio per utente. I criteri globali e/o del sito non possono essere assegnati a un sito mediante il parametro VoiceRoutingPolicy.</p>
<p>Questo parametro è stato introdotto nella versione di febbraio 2013 di Lync Server 2013.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType. Consente di accettare l'input da pipeline di oggetti sito di rete.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Modifica un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType.

## Vedere anche

#### Ulteriori risorse

[New-CsNetworkSite](new-csnetworksite.md)  
[Remove-CsNetworkSite](remove-csnetworksite.md)  
[Get-CsNetworkSite](get-csnetworksite.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkMediaBypassConfiguration](new-csnetworkmediabypassconfiguration.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)  
[Get-CsNetworkConfiguration](get-csnetworkconfiguration.md)

