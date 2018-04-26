---
title: New-CsNetworkSite
TOCTitle: New-CsNetworkSite
ms:assetid: 55134dd4-eb2b-483b-8b3d-e9e42ac1acc2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398365(v=OCS.15)
ms:contentKeyID: 49300560
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkSite

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo sito di rete da utilizzare con il servizio Controllo di ammissione di chiamata o con il servizio di chiamate di emergenza (Enhanced 9-1-1). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsNetworkSite -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    New-CsNetworkSite -NetworkSiteID <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: -NetworkRegionID <String> [-BWPolicyProfileID <String>] [-BypassID <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-EnableLocationBasedRouting <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-LocationPolicy <String>] [-VoiceRoutingPolicy <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con questo esempio viene creato un nuovo sito di rete denominato Vancouver. Il nome del sito viene specificato come valore del parametro Identity. Viene inoltre specificato un valore per il parametro NetworkRegionID, che in questo esempio associa il sito alla regione NorthAmerica. Il valore BypassID sarà generato automaticamente. Non è consigliabile impostare manualmente un valore per BypassID.

Il comando in questo esempio non comprende il parametro BWPolicyProfileID. Se non viene aggiunto successivamente un valore con il cmdlet **Set-CsNetworkSite**, questo sito non presenterà limitazioni della larghezza di banda per le connessioni multimediali.

    New-CsNetworkSite -Identity Vancouver -NetworkRegionID NorthAmerica

## ESEMPIO 2

Con l'esempio 2 viene creato un nuovo sito di rete denominato Paris. Il nome del sito viene specificato come valore del parametro Identity. Come nell'esempio 1 viene specificato anche un valore per NetworkRegionID, questa volta corrispondente alla regione EMEA. Ancora una volta viene seguito il percorso consigliato, permettendo al cmdlet di generare il BypassID. A differenza dell'esempio 1, con questo esempio viene specificato anche un valore per il parametro BWPolicyProfileID: LowBWLimits. Per questo sito saranno utilizzati i criteri associati a tale profilo.

    New-CsNetworkSite -Identity Paris -NetworkRegionID EMEA -BWPolicyProfileID LowBWLimits

## Descrizione dettagliata

I siti di rete sono gli uffici o le postazioni configurati in ogni regione di una distribuzione CAC o per le chiamate di emergenza. Questo cmdlet consente di creare un nuovo sito e facoltativamente di associarlo a una regione. Ad esempio, un'area di rete per il Nord America potrebbe essere associata a siti di rete come Chicago, Redmond e Vancouver. Deve essere creato un sito di rete Controllo di ammissione di chiamata per ogni sito nell'organizzazione, anche se tale sito non presenta limiti della larghezza di banda.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **New-CsNetworkSite** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkSite"}

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
<td><p>Identificatore univoco del sito di rete appena creato. I siti vengono creati solo nell'ambito globale, quindi questo identificatore non deve specificare un ambito. Include invece una stringa univoca tra tutti i siti di rete nella distribuzione di Lync Server.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>L'identità dell'area di rete a cui è associato questo sito. Questo parametro deve contenere un valore se si desidera fornire un BypassID (manualmente o tramite la generazione automatica) o se la proprietà EnableBandwidthPolicyCheck della configurazione della rete è impostata su True. È possibile recuperare le impostazioni di configurazione della rete chiamando il cmdlet <strong>Get-CsNetworkConfiguration</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Questo valore è identico a Identity. Non è possibile specificare un valore sia per Identity sia per NetworkSiteID; il valore immesso per l'uno verrà automaticamente utilizzato anche per l'altro.</p></td>
</tr>
<tr class="even">
<td><p><em>BWPolicyProfileID</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>L'identità del profilo dei criteri di larghezza di banda che definisce i limiti della larghezza di banda per questo sito. È possibile recuperare un elenco dei profili disponibili chiamando il cmdlet <strong>Get-CsNetworkBandwidthPolicyProfile</strong>.</p>
<p>Se si specifica un valore per questo parametro, è necessario specificare anche un valore per il parametro NetworkRegionID.</p></td>
</tr>
<tr class="odd">
<td><p><em>BypassID</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Identificatore univoco globale (GUID). Questo GUID è utilizzato per mappare i siti di rete alle impostazioni di bypass multimediale con una configurazione di rete CAC o E9-1-1. Utilizzare questo valore BypassID nella chiamata al cmdlet <strong>New-CsNetworkMediaBypassConfiguration</strong>.</p>
<p>Se non si specifica un valore per questo parametro, un valore verrà generato automaticamente, ma solo se si specifica un valore per il parametro NetworkRegionID. Se non si fornisce un parametro NetworkRegionID, non viene generato alcun BypassID. Non è nemmeno possibile fornire esplicitamente un valore per il parametro BypassID senza specificare anche un valore per il parametro NetworkRegionID.</p>
<p>Se si specifica un valore in modo esplicito, il valore deve essere nel formato GUID (ad esempio, 3b24a047-dce6-48b2-9f20-9fbff17ed62a). La generazione automatica è la scelta consigliata. Se si immette manualmente un valore, viene visualizzata una richiesta di conferma per verificare che l'utente non desideri la generazione automatica del valore.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Una stringa che descrive il sito. Questo parametro può essere utilizzato per fornire una spiegazione dello scopo o della posizione del sito più descrittiva di quanto non possa essere espresso con il solo parametro Identity.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableLocationBasedRouting</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, il routing vocale verrà gestito in base alla posizione dell'utente che effettua la chiamata e dell'utente che riceve la chiamata. Il valore predefinito è False.</p></td>
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
<td><p><em>LocationPolicy</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nomi dei criteri percorso associati a questo sito. I criteri percorso assegnano specifiche impostazioni per le chiamate di emergenza al sito. È possibile recuperare un elenco dei criteri percorso chiamando il cmdlet <strong>Get-CsLocationPolicy</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>VoiceRoutingPolicy</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Criterio di routing vocale per utente da assegnare al sito. Ad esempio:</p>
<p>-VoiceRoutingPolicy &quot;RedmondVoiceRouting”</p>
<p>È necessario specificare un criterio per utente. Non è possibile assegnare criteri globali e/o sito a un sito che utilizza il parametro VoiceRoutingPolicy.</p>
<p>Questo parametro è stato introdotto nella versione di febbraio 2013 di Lync Server 2013.</p></td>
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

Crea un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType.

## Vedere anche

#### Ulteriori risorse

[Remove-CsNetworkSite](remove-csnetworksite.md)  
[Set-CsNetworkSite](set-csnetworksite.md)  
[Get-CsNetworkSite](get-csnetworksite.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkMediaBypassConfiguration](new-csnetworkmediabypassconfiguration.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)  
[Get-CsNetworkConfiguration](get-csnetworkconfiguration.md)

