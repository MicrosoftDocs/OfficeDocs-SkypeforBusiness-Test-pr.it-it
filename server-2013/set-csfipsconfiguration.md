---
title: Set-CsFIPSConfiguration
TOCTitle: Set-CsFIPSConfiguration
ms:assetid: 920f58ce-e175-41ac-b681-5ac873091593
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205084(v=OCS.15)
ms:contentKeyID: 49301335
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsFIPSConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una raccolta esistente di impostazioni di configurazione FIPS (Federal Information Processing Standards). Gli standard FIPS sono un insieme di standard di sicurezza del Governo degli Stati Uniti da utilizzare nei computer gestiti da agenzie governative non militari e da appaltatori governativi. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Set-CsFIPSConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsFIPSConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-RequireFIPSCompliantMedia <$true | $false>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Nell'esempio 1 la proprietà RequireFIPSCompliantMedia delle impostazioni di configurazione FIPS globali viene impostata su True ($True).

    Set-CsFIPSConfiguration -Identity "global" -RequireFIPSCompliantMedia $True

## Descrizione dettagliata

Gli standard FIPS (Federal Information Processing Standards) sono una serie di linee guida e di standard applicati a computer utilizzati per collaborare con il Governo degli Stati Uniti. Alcuni standard FIPS ad esempio definiscono l'utilizzo di elementi quali la crittografia e le firme digitali. Per ulteriori informazioni, vedere la pagina Web all'indirizzo <http://www.itl.nist.gov/fipspubs/by-num.htm>. In Lync Server 2013 è disponibile un'opzione che consente al software di utilizzare solo algoritmi che soddisfano gli standard FIPS. In caso di collaborazione con il Governo degli Stati Uniti o con altri enti che applicano gli standard FIPS, è possibile abilitare la conformità FIPS in Lync Server 2013.

Considerare tuttavia che per la versione locale di Lync Server è disponibile una singola raccolta globale di impostazioni di configurazione FIPS. È possibile pertanto abilitare o disabilitare la conformità FIPS solo per l'intera implementazione di Lync Server e non in modo selettivo ad esempio per un singolo sito o per un singolo pool di registrazione. Se si abilita la conformità FIPS, esiste il rischio che si verifichino problemi di comunicazione con organizzazioni che non aderiscono pienamente agli standard FIPS.

Per impostazione predefinita, la conformità FIPS è disabilitata in Lync Server 2013.

Il cmdlet **Set-CsFIPSConfiguration** viene utilizzato per abilitare o disabilitare la conformità FIPS.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsFIPSConfiguration"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Set-CsFIPSConfiguration** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identità univoca delle impostazioni di configurazione FIPS da modificare. Poiché Lync Server 2013 supporta una sola raccolta globale di impostazioni FIPS, l'unica raccolta che può essere modificata è la raccolta globale:</p>
<p>-Identity global</p>
<p>Se non si include questo parametro, il cmdlet <strong>Set-CsFIPSConfiguration</strong> modificherà la raccolta globale.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>RequireFIPSCompliantMedia</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se questo parametro è impostato su True, Lync Server 2013 consentirà solo sessioni multimediali con entità che utilizzano algoritmi conformi agli standard FIPS per l'autenticazione e l'autorizzazione.</p>
<p>Se si richiede la conformità agli standard FIPS, gli utenti non potranno più connettersi al sistema utilizzando un A/V Edge Server di Microsoft Lync Server 2010. Sarà invece necessario aggiornare tutti i server perimetrali a Lync 2013.</p>
<p>Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account del tenant di Skype for Business online per il quale vengono modificate le impostazioni di configurazione FIPS, ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Set-CsFIPSConfiguration** accetta istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.FIPSConfiguration.FIPSConfiguration inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Set-CsFIPSConfiguration** invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.FIPSConfiguration.FIPSConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsFIPSConfiguration](get-csfipsconfiguration.md)  
[New-CsFIPSConfiguration](new-csfipsconfiguration.md)  
[Remove-CsFIPSConfiguration](remove-csfipsconfiguration.md)

