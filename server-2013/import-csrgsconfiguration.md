---
title: Import-CsRgsConfiguration
TOCTitle: Import-CsRgsConfiguration
ms:assetid: c4977e34-7a62-4cb7-b8ec-bacb471b3de4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205245(v=OCS.15)
ms:contentKeyID: 49301923
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsRgsConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Importa i dati di configurazione di Response Group precedentemente esportati utilizzando il cmdlet **Export-CsRgsConfiguration**. La possibilità di esportare e importare dati di configurazione di Response Group si rivela particolarmente utile in scenari di ripristino di emergenza. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Import-CsRgsConfiguration -Destination <RgsIdentity> -FileName <String> [-Force <SwitchParameter>] [-OverwriteOwner <SwitchParameter>] [-ReplaceExistingRgsSettings <SwitchParameter>] [-ResolveNameConflicts <SwitchParameter>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 importa una raccolta di impostazioni dell'applicazione Response Group esportata precedentemente e quindi applica tali impostazioni all'installazione di Response Group ospitata dal server applicazioni in atl-cs-001.litwareinc.com.

    Import-CsRgsConfiguration -FileName "C:\Export\RgsExport.zip" -Destination "ApplicationServer:atl-cs-001.litwareinc.com"

## Descrizione dettagliata

Il cmdlet [Export-CsRgsConfiguration](export-csrgsconfiguration.md) e il cmdlet **Import-CsRgsConfiguration** consentono di esportare i dati sull'implementazione corrente dell'applicazione Response Group, inclusi flussi di lavoro, code, gruppi di agenti, set di festività, orari di ufficio, file audio e impostazioni di configurazione dei servizi, per poi importare o reimportare tali informazioni. Questa possibilità può rivelarsi estremamente utile in uno scenario di ripristino di emergenza, ad esempio in caso di errore del server che ospita l'applicazione Response Group, oppure se si desidera semplicemente trasferire l'applicazione Response Group in un altro pool.

Si noti che il cmdlet **Export-CsRgsConfiguration** e il cmdlet **Import-CsRgsConfiguration** funzionano solo con Lync Server 2013. Se si desidera eseguire la migrazione di dati di Response Group da Microsoft Lync Server 2010 a Lync Server 2013, utilizzare invece il cmdlet [Move-CsRgsConfiguration](move-csrgsconfiguration.md).

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsRgsConfiguration"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Import-CsRgsConfiguration** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Destination</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>Identità dell'istanza di Response Group in cui vengono importate le impostazioni di configurazione. Ad esempio:</p>
<p>-Destination &quot;ApplicationServer:atl-rgs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>FileName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Percorso del file ZIP creato dal cmdlet <strong>Export-CsRgsConfiguration</strong>. Ad esempio:</p>
<p>-FileName &quot;C:\Exports\RgsConfig.zip&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>OverwriteOwner</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se viene specificato questo parametro, il proprietario corrente degli oggetti di Response Group verrà sovrascritto con l'identità del servizio del nuovo pool di Response Group.</p></td>
</tr>
<tr class="odd">
<td><p><em>ReplaceExistingRgsSettings</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Quando viene specificato questo parametro, tutte le impostazioni del servizio esistenti per il pool di destinazione vengono sostituite dalle impostazioni importate. Se il parametro non viene specificato, le impostazioni del servizio resteranno invariate e verrà importato solo l'oggetto Response Group, ad esempio flussi di lavoro e gruppi di agenti.</p></td>
</tr>
<tr class="even">
<td><p><em>ResolveNameConflicts</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se viene specificato questo parametro, i nomi duplicati verranno risolti aggiungendo un numero identificativo univoco. Se ad esempio sono presenti due flussi di lavoro denominati Help Desk Workflow, uno dei due verrà ridenominato Help Desk Workflow (2).</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Import-CsRgsConfiguration** non accetta input da pipeline.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Export-CsRgsConfiguration](export-csrgsconfiguration.md)

