---
title: Get-CsBandwidthPolicyServiceConfiguration
TOCTitle: Get-CsBandwidthPolicyServiceConfiguration
ms:assetid: 9cb9cf59-c47e-40f6-9f9e-235b83329a69
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412727(v=OCS.15)
ms:contentKeyID: 49301456
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsBandwidthPolicyServiceConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera una o più configurazioni del servizio dei criteri di larghezza di banda. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsBandwidthPolicyServiceConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsBandwidthPolicyServiceConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono recuperate tutte le configurazioni del servizio dei criteri di larghezza di banda definiti nell'implementazione di Lync Server.

    Get-CsBandwidthPolicyServiceConfiguration

## ESEMPIO 2

Questo esempio consente di recuperare la configurazione del servizio dei criteri di larghezza di banda definita per il sito Redmond (-Identity site:Redmond).

    Get-CsBandwidthPolicyServiceConfiguration -Identity site:Redmond

## ESEMPIO 3

In questo esempio, viene utilizzato il parametro Filter per recuperare tutte le configurazioni del servizio dei criteri di larghezza di banda definite a livello di sito. Per fare ciò, si utilizza il valore site:\* per il parametro Filter. In questo modo, nella proprietà Identity di tutte le configurazioni del servizio dei criteri di larghezza di banda si cercheranno i valori che iniziano con site: e sono seguiti da qualsiasi altro carattere. Dal momento che nelle configurazioni a livello di sito, il valori Identity iniziano con site: e sono seguiti dal nome del sito, questo filtro individuerà tutte le configurazioni per tutti i siti.

    Get-CsBandwidthPolicyServiceConfiguration -Filter site:*

## ESEMPIO 4

Nell'esempio 4 vengono recuperate tutte le configurazioni del servizio dei criteri di larghezza di banda che consentono ai file di log di raggiungere una dimensione superiore a 4 MB. In questo esempio viene chiamato innanzitutto il cmdlet **Get-CsBandwidthPolicyServiceConfiguration**. Come nell'esempio 1, questo cmdlet recupera una raccolta di tutte le configurazioni definite nella distribuzione di Lync Server. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**. Il cmdlet **Where-Object** esamina gli elementi della raccolta uno alla volta. Per ogni elemento della raccolta, il cmdlet **Where-Object** verifica se il valore della proprietà MaxLogFileSizeMb è maggiore di (-gt) 4. In caso affermativo, tale elemento continua a far parte della raccolta ed è presente nell'output del comando. Se il valore di MaxLogFileSizeMb non è maggiore di 4, l'elemento verrà ignorato e non verrà restituito.

    Get-CsBandwidthPolicyServiceConfiguration | Where-Object {$_.MaxLogFileSizeMb -gt 4}

## Descrizione dettagliata

Il servizio Controllo di ammissione di chiamata consente di decidere se consentire l'avvio di sessioni di comunicazione in tempo reale, quali chiamate vocali o video, sulla base di vincoli di larghezza di banda. Nell'implementazione di Controllo di ammissione di chiamata in Lync Server, le aree, i siti e le subnet sono definiti in una rete insieme alle relazioni e ai collegamenti tra queste entità in modo da stabilire vincoli di larghezza di banda tra di essi. Il servizio Criteri di larghezza di banda è il componente che esegue la funzionalità Controllo di ammissione di chiamata nella distribuzione di Lync Server, consentendo di decidere se la larghezza di banda disponibile è sufficiente per eseguire la chiamata. Il cmdlet **Get-CsBandwidthPolicyServiceConfiguration** recupera le impostazioni per uno o più servizi dei criteri di larghezza di banda.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsBandwidthPolicyServiceConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsBandwidthPolicyServiceConfiguration"}

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
<td><p>Una stringa contenente uno o più caratteri jolly che verrà utilizzata per eseguire una ricerca tra le proprietà Identity di tutte le configurazioni del servizio dei criteri di larghezza di banda al fine di trovare tutte le configurazioni in cui Identity corrisponde al modello di caratteri jolly. Ad esempio, utilizzando per Filter il valore site:* si recupereranno tutte le configurazioni in cui i valori Identity iniziano con la stringa site: e terminano con una qualsiasi combinazione di caratteri.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>L'identificatore univoco della configurazione che si desidera recuperare. Questo identificatore è costituito dall'ambito (per la configurazione globale) o dall'ambito e dal nome (per la configurazione a livello di sito come, ad esempio, site:Redmond).</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare la configurazione del servizio dei criteri di larghezza di banda dalla copia locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Consente di recuperare uno o più oggetti di tipo Microsoft.Rtc.Management.WritableConfig.Settings.BandwidthPolicyServiceConfiguration.BandwidthPolicyServiceConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsBandwidthPolicyServiceConfiguration](new-csbandwidthpolicyserviceconfiguration.md)  
[Remove-CsBandwidthPolicyServiceConfiguration](remove-csbandwidthpolicyserviceconfiguration.md)  
[Set-CsBandwidthPolicyServiceConfiguration](set-csbandwidthpolicyserviceconfiguration.md)

