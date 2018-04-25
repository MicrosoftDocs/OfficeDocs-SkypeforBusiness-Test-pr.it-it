---
title: Remove-CsFIPSConfiguration
TOCTitle: Remove-CsFIPSConfiguration
ms:assetid: b7e43419-0154-4fed-bfc6-9053335ce5d8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205201(v=OCS.15)
ms:contentKeyID: 49301756
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsFIPSConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una o più raccolte di impostazioni di configurazione FIPS (Federal Information Processing Standards). Gli standard FIPS sono un insieme di standard di sicurezza del Governo degli Stati Uniti da utilizzare nei computer gestiti da agenzie governative non militari e da appaltatori governativi. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Remove-CsFIPSConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Nell'esempio 1 le proprietà della raccolta globale di impostazioni di configurazione FIPS vengono reimpostate sui rispettivi valori predefiniti.

    Remove-CsFIPSConfiguration -Identity "Global"

## Descrizione dettagliata

Gli standard FIPS (Federal Information Processing Standards) sono una serie di linee guida e di standard applicati a computer utilizzati per collaborare con il Governo degli Stati Uniti. Alcuni standard FIPS ad esempio definiscono l'utilizzo di elementi quali la crittografia e le firme digitali. Per ulteriori informazioni, vedere la pagina Web all'indirizzo <http://www.itl.nist.gov/fipspubs/by-num.htm>. In Lync Server 2013 è disponibile un'opzione che consente al software di utilizzare solo algoritmi che soddisfano gli standard FIPS. In caso di collaborazione con il Governo degli Stati Uniti o con altri enti che applicano gli standard FIPS, è possibile abilitare la conformità FIPS in Lync Server 2013.

Considerare tuttavia che per la versione locale di Lync Server è disponibile una singola raccolta globale di impostazioni di configurazione FIPS. È possibile pertanto abilitare o disabilitare la conformità FIPS solo per l'intera implementazione di Lync Server e non in modo selettivo ad esempio per un singolo sito o per un singolo pool di registrazione. Se si abilita la conformità FIPS, esiste il rischio che si verifichino problemi di comunicazione con organizzazioni che non aderiscono pienamente agli standard FIPS.

Per impostazione predefinita, la conformità FIPS è disabilitata in Lync Server 2013.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli di controllo di accesso basato sui ruoli personalizzati creati dall'utente, al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsFIPSConfiguration

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet Remove-CsFIPSConfiguration non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identità univoca delle impostazioni di configurazione FIPS da rimuovere. Poiché Lync Server 2013 supporta una sola raccolta globale di impostazioni FIPS, l'unica raccolta che può essere eliminata è la raccolta globale:</p>
<p>-Identity global</p>
<p>In questo caso, la raccolta globale non verrà effettivamente rimossa dal sistema. Lync Server 2013 non supporta l'eliminazione delle impostazioni globali. L'unica proprietà di tale raccolta, RequireFIPSCompliantMedia, verrà invece reimpostata sul relativo valore predefinito, ovvero False.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account del tenant di Skype for Business online per le impostazioni di configurazione FIPS da eliminare, ad esempio:</p>
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

Il cmdlet **Remove-CsFIPSConfiguration** accetta istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.FIPSConfiguration.FIPSConfiguration inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsFIPSConfiguration** invece elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.FIPSConfiguration.FIPSConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsFIPSConfiguration](get-csfipsconfiguration.md)  
[New-CsFIPSConfiguration](new-csfipsconfiguration.md)  
[Set-CsFIPSConfiguration](set-csfipsconfiguration.md)

