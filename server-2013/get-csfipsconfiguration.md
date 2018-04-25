---
title: Get-CsFIPSConfiguration
TOCTitle: Get-CsFIPSConfiguration
ms:assetid: 56d29011-187f-4034-a5ed-71625087bf36
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204904(v=OCS.15)
ms:contentKeyID: 49300584
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsFIPSConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle impostazioni di configurazione FIPS (Federal Information Processing Standards) attualmente in uso nell'organizzazione. Gli standard FIPS sono un insieme di standard di sicurezza del Governo degli Stati Uniti da utilizzare nei computer gestiti da agenzie governative non militari e da appaltatori governativi. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsFIPSConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsFIPSConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Tenant <Guid>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 restituisce le informazioni su tutte le impostazioni di configurazione FIPS in uso nell'organizzazione. Si noti che esiste una sola istanza globale di impostazione di configurazione FIPS.

    Get-CsFIPSConfiguration

## Descrizione dettagliata

Gli standard FIPS (Federal Information Processing Standards) sono una serie di linee guida e di standard applicati a computer utilizzati per collaborare con il Governo degli Stati Uniti. Alcuni standard FIPS ad esempio definiscono l'utilizzo di elementi quali la crittografia e le firme digitali. Per ulteriori informazioni, vedere la pagina Web all'indirizzo <http://www.itl.nist.gov/fipspubs/by-num.htm>. In Lync Server 2013 è disponibile un'opzione che consente al software di utilizzare solo algoritmi che soddisfano gli standard FIPS. In caso di collaborazione con il Governo degli Stati Uniti o con altri enti che applicano gli standard FIPS, è possibile abilitare la conformità FIPS in Lync Server 2013.

Considerare tuttavia che per la versione locale di Lync Server è disponibile una sola raccolta globale di impostazioni di configurazione FIPS. È possibile pertanto abilitare o disabilitare la conformità FIPS solo per l'intera implementazione di Lync Server e non in modo selettivo, ad esempio per un singolo sito o per un singolo pool di registrazione. Se si abilita la conformità FIPS, esiste il rischio che si verifichino problemi di comunicazione con organizzazioni che non aderiscono pienamente agli standard FIPS.

Per impostazione predefinita, la conformità FIPS è disabilitata in Lync Server 2013.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsFIPSConfiguration"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet Get-CsFIPSConfiguration non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare valori con caratteri jolly per fare riferimento a una raccolta di impostazioni di configurazione FIPS. Poiché è possibile disporre di una sola istanza globale di queste impostazioni, il parametro Filter non è necessario. Se lo si preferisce, è tuttavia possibile utilizzare la sintassi seguente per fare riferimento alle impostazioni globali:</p>
<p>-Filter &quot;g*&quot;</p>
<p>Questa sintassi recupera tutte le impostazioni di configurazione FIPS la cui identità inizia con la lettera &quot;g&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identità univoca delle impostazioni di configurazione FIPS. Dal momento che è possibile disporre di una sola istanza globale di tali impostazioni, non è necessario specificare un'identità nella chiamata al cmdlet <strong>Get-CsFIPSConfiguration</strong>. Se lo si preferisce, è tuttavia possibile utilizzare la sintassi seguente per fare riferimento alle impostazioni globali:</p>
<p>-Identity global</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione FIPS dalla replica locale dell'archivio di gestione centrale anziché direttamente dall'archivio di gestione centrale.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di Skype for Business online di cui devono essere recuperate le impostazioni di configurazione FIPS.</p>
<p>Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsFIPSConfiguration** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsFIPSConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.FIPSConfiguration.FIPSConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsFIPSConfiguration](new-csfipsconfiguration.md)  
[Remove-CsFIPSConfiguration](remove-csfipsconfiguration.md)  
[Set-CsFIPSConfiguration](set-csfipsconfiguration.md)

