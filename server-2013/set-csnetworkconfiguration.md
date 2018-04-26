---
title: Set-CsNetworkConfiguration
TOCTitle: Set-CsNetworkConfiguration
ms:assetid: d54dc154-c092-4be9-8656-f7fec3fbd835
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398927(v=OCS.15)
ms:contentKeyID: 49302087
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica le impostazioni di una configurazione di rete. Questo cmdlet verrà utilizzato più frequentemente per abilitare o disabilitare il servizio Controllo di ammissione di chiamata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsNetworkConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BWPolicyProfiles <PSListModifier>] [-Confirm [<SwitchParameter>]] [-EnableBandwidthPolicyCheck <$true | $false>] [-Force <SwitchParameter>] [-InterNetworkRegionRoutes <PSListModifier>] [-InterNetworkSitePolicies <PSListModifier>] [-MediaBypassSettings <MediaBypassSettingsType>] [-NetworkRegionLinks <PSListModifier>] [-NetworkRegions <PSListModifier>] [-NetworkSites <PSListModifier>] [-Subnets <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando di questo esempio eseguirà un controllo di convalida rispetto all'intera configurazione del servizio Controllo di ammissione di chiamata e quindi, a seconda delle risposte ai messaggi di avviso restituiti, abiliterà il servizio Controllo di ammissione di chiamata. Se il servizio Controllo di ammissione di chiamata è già abilitato, ovvero se la proprietà EnableBandwidthPolicyCheck è True, e si esegue questo comando, verrà semplicemente eseguito il controllo di convalida.

    Set-CsNetworkConfiguration -EnableBandwidthPolicyCheck $True

## Descrizione dettagliata

L'oggetto configurazione di rete contiene tutte le impostazioni per l'intera configurazione del servizio Controllo di ammissione di chiamata in una distribuzione di Lync Server oltre alle impostazioni di bypass degli elementi multimediali. È possibile utilizzare questo cmdlet per modificare qualsiasi parte della configurazione del servizio Controllo di ammissione di chiamata ma è necessario utilizzarlo se si desidera modificare le impostazioni di bypass degli elementi multimediali. Per modificare la maggior parte delle impostazioni di configurazione del servizio, è consigliabile tuttavia utilizzare i cmdlet specifici per il tipo di oggetto. Per gestire, ad esempio, le aree di rete, utilizzare i cmdlet che finiscono con CsNetworkRegion anziché modificare il parametro NetworkRegions di questo cmdlet.

Questo cmdlet viene utilizzato principalmente per abilitare (e disabilitare) il servizio Controllo di ammissione di chiamata e per applicare le impostazioni di bypass degli elementi multimediali. Dopo aver configurato i diversi componenti necessari per la configurazione (ad esempio aree, siti e subnet), è necessario abilitare la configurazione affinché possa essere utilizzata. A tale scopo, impostare semplicemente il parametro EnableBandwidthPolicyCheck su True. Si noti che l'esecuzione di questo cmdlet con EnableBandwidthPolicyCheck impostato su True non abilita immediatamente il servizio Controllo di ammissione di chiamata. Prima dell'abilitazione vengono eseguiti una serie di controlli di convalida per garantire che la configurazione sia stata completata correttamente. Gli errori o le discrepanze rilevate nella configurazione comporteranno la visualizzazione di messaggi di avviso in cui verrà chiesto se si desidera continuare l'abilitazione del servizio Controllo di ammissione di chiamata nonostante esista un problema. Se si sceglie di continuare, premendo Invio o Y, la convalida proseguirà visualizzando altri messaggi se vengono rilevati nuovi errori.

Se si esegue tutto il processo di convalida scegliendo di proseguire a ogni avviso, EnableBandwidthPolicyCheck verrà impostato su True e il servizio verrà abilitato. È probabile tuttavia che non funzionerà come previsto finché non verranno risolti gli errori. Se in qualsiasi momento durante la convalida si sceglie di interrompere il processo, digitando N al messaggio di avviso, la convalida terminerà e EnableBandwidthPolicyCheck rimarrà impostato su False (valore predefinito).

Se EnableBandwidthPolicyCheck è già impostato su True, è possibile chiamare il cmdlet **Set-CsNetworkConfiguration** e passare il valore True al parametro EnableBandwidthPolicyCheck per eseguire la convalida senza modificare le impostazioni. Quando inoltre EnableBandwidthPolicyCheck è impostato su True, qualsiasi modifica che si tenta di effettuare chiamando il cmdlet **Set-CsNetworkConfiguration** attiverà di nuovo l'esecuzione del controllo di convalida.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsNetworkConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkConfiguration"}

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
<td><p><em>BWPolicyProfiles</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>Raccolta di tutti i profili dei criteri di larghezza di banda che possono essere assegnati a siti, criteri intersito e collegamenti aree di rete. Ogni profilo dei criteri di larghezza di banda contiene le limitazioni relative alla larghezza di banda (sia globali che di sessione) per le connessioni audio e/o video. Un elenco completo dei profili dei criteri di larghezza di banda può essere recuperato chiamando il cmdlet <strong>Get-CsNetworkBandwidthPolicyProfile</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableBandwidthPolicyCheck</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se questo parametro viene impostato su True, verrà un eseguito un controllo di convalida rispetto all'intera configurazione del servizio Controllo di ammissione di chiamata. Se tutti i controlli di convalida vengono superati o se si sceglie di ignorare tutti gli avvisi, il servizio Controllo di ammissione di chiamata verrà abilitato. Se un controllo di convalida non viene superato, è possibile scegliere di interrompere la convalida e in questo caso il valore di EnableBandwidthPolicyCheck non verrà modificato. È necessario che le route di regione siano definite tra ogni coppia di regione di rete per poter eseguire il controllo di convalida.</p>
<p>Se questo parametro viene impostato su False, il servizio Controllo di ammissione di chiamata verrà disabilitato.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Questo parametro non accetta un valore. Se si include questo parametro, tutte le modifiche apportate alla configurazione, compresa la relativa abilitazione, verranno implementate senza avvisi o controlli di convalida.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>XdsIdentity</p></td>
<td><p>Questo valore sarà sempre Global.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>NetworkConfigurationSettings</p></td>
<td><p>Riferimento a un oggetto configurazione di rete. Questo oggetto deve essere di tipo Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings, che può essere recuperato chiamando il cmdlet <strong>Get-CsNetworkConfiguration</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>InterNetworkRegionRoutes</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>Raccolta di tutte le route dell'area di rete definite nella configurazione del servizio Controllo di ammissione di chiamata. È possibile recuperare tutti i membri di questa raccolta chiamando il cmdlet <strong>Get-CsNetworkInterRegionRoute</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>InterNetworkSitePolicies</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>Raccolta di criteri intersito di rete definiti nella configurazione del servizio Controllo di ammissione di chiamata. È possibile recuperare tutti i membri di questa raccolta chiamando il cmdlet <strong>Get-CsNetworkInterSitePolicy</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>MediaBypassSettings</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>MediaBypassSettingsType</p></td>
<td><p>Riferimento a un oggetto che definisce le impostazioni globali di bypass degli elementi multimediali per la configurazione del servizio Controllo di ammissione di chiamata. L'impostazione di questo valore sovrascriverà tutte le impostazioni esistenti di bypass degli elementi multimediali. Per ottenere questo riferimento all'oggetto, chiamare il cmdlet <strong>New-CsNetworkMediaBypassConfiguration</strong> e assegnare le nuove impostazioni di configurazione a una variabile. Passare questa variabile al parametro MediaBypassSettings per modificare le impostazioni globali di bypass degli elementi multimediali.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionLinks</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>Raccolta di collegamenti dell'area di rete definiti nella configurazione del servizio Controllo di ammissione di chiamata. Ogni collegamento dell'area di rete definisce una connessione tra due aree e le limitazioni relative alla larghezza di banda da applicare alle connessioni tra tali aree. È possibile recuperare tutti i membri di questa raccolta chiamando il cmdlet <strong>Get-CsNetworkRegionLink</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegions</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>Raccolta di aree di rete, ciascuna delle quali rappresenta un hub o un backbone all'interno della rete, definite nella configurazione del servizio Controllo di ammissione di chiamata. È possibile recuperare tutti i membri di questa raccolta chiamando il cmdlet <strong>Get-CsNetworkRegion</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkSites</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>Raccolta di siti di rete, ciascuno dei quali rappresenta un ufficio o una località all'interno di un'area, definiti nella configurazione del servizio Controllo di ammissione di chiamata. È possibile recuperare tutti i membri di questa raccolta chiamando il cmdlet <strong>Get-CsNetworkSite</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>Subnets</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PSListModifier</p></td>
<td><p>Raccolta di subnet di rete (ciascuna delle quali associa un endpoint a un sito) definite nella configurazione del servizio Controllo di ammissione di chiamata. È possibile recuperare tutti i membri di questa raccolta chiamando il cmdlet <strong>Get-CsNetworkSubnet</strong>.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings. Accetta l'input da pipeline di un oggetto di configurazione di rete.

## Tipi restituiti

Il cmdlet **Set-CsNetworkConfiguration** non restituisce un valore o un oggetto. Il cmdlet modifica invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings.

## Vedere anche

#### Ulteriori risorse

[Remove-CsNetworkConfiguration](remove-csnetworkconfiguration.md)  
[Get-CsNetworkConfiguration](get-csnetworkconfiguration.md)  
[Get-CsNetworkSite](get-csnetworksite.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkMediaBypassConfiguration](new-csnetworkmediabypassconfiguration.md)

