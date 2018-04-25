---
title: Export-CsRgsConfiguration
TOCTitle: Export-CsRgsConfiguration
ms:assetid: 754513a4-0b46-44b7-8910-f865b1e0f037
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205011(v=OCS.15)
ms:contentKeyID: 49301006
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Export-CsRgsConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Esporta i dati da una configurazione esistente dell'applicazione Response Group. Questi dati, salvati come file ZIP, possono essere importati successivamente utilizzando il cmdlet **Import-CsRgsConfiguration**. La possibilità di esportare e importare dati di configurazione di Response Group si rivela particolarmente utile in scenari di ripristino di emergenza. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Export-CsRgsConfiguration -FileName <String> -Source <RgsIdentity> [-Force <SwitchParameter>] [-Owner <RgsIdentity>] [-RemoveExportedConfiguration <SwitchParameter>]

## Esempi

## Esempio 1

Il comando mostrato nell'esempio 1 esporta le impostazioni di configurazione di Response Group dal pool atl-rgs-001.litwareinc.com in un file il cui percorso è C:\\Exports\\Rgs.zip.

    Export-CsRgsConfiguration -Source "ApplicationServer:atl-rgs-001.litwareinc.com" -FileName "C:\Exports\Rgs.zip"

## Descrizione dettagliata

Il cmdlet **Export-CsRgsConfiguration** e il cmdlet [Import-CsRgsConfiguration](import-csrgsconfiguration.md) consentono di esportare i dati sull'implementazione corrente dell'applicazione Response Group, inclusi flussi di lavoro, code, gruppi di agenti, set di festività, orari di ufficio, file audio e impostazioni di configurazione dei servizi, per poi importare o reimportare tali informazioni. Questa possibilità può rivelarsi estremamente utile in uno scenario di ripristino di emergenza, ad esempio in caso di errore del server che ospita l'applicazione Response Group, oppure se si desidera semplicemente trasferire l'applicazione Response Group in un altro pool.

Si noti che il cmdlet **Export-CsRgsConfiguration** e il cmdlet **Import-CsRgsConfiguration** funzionano solo con Lync Server 2013. Se si desidera eseguire la migrazione di dati di Response Group da Microsoft Lync Server 2010 a Lync Server 2013, utilizzare invece il cmdlet [Move-CsRgsConfiguration](move-csrgsconfiguration.md).

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Export-CsRgsConfiguration"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Export-CsRgsConfiguration** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>FileName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Percorso del file ZIP da creare quando si esegue il cmdlet <strong>Export-CsRgsConfiguration</strong>. Ad esempio:</p>
<p>-FileName &quot;C:\Exports\RgsConfig.zip&quot;</p>
<p>Si noti che il comando avrà esito negativo se il file esiste già.</p></td>
</tr>
<tr class="even">
<td><p><em>Source</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>Identità dell'istanza di Response Group di cui vengono esportate le impostazioni di configurazione. Ad esempio:</p>
<p>-Source &quot;ApplicationServer:atl-rgs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Owner</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>Se si specifica questo parametro, le informazioni di configurazione per tutte le istanze di Response Group trovate nel pool designato verranno esportate, ad esempio:</p>
<p>-Owner &quot;atl-rgs-001.litwareinc.com&quot;</p></td>
</tr>
<tr class="odd">
<td><p><em>RemoveExportedConfiguration</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se si specifica questo parametro, l'istanza di Response Group verrà eliminata dopo l'esportazione delle informazioni di configurazione.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Export-CsRgsConfiguration** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Export-CsRgsConfiguration** crea file compressi con estensione zip.

## Vedere anche

#### Ulteriori risorse

[Import-CsRgsConfiguration](import-csrgsconfiguration.md)

