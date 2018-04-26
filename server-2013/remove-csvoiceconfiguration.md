---
title: Remove-CsVoiceConfiguration
TOCTitle: Remove-CsVoiceConfiguration
ms:assetid: 9b173dde-fa8e-4966-aa58-deff34625560
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398804(v=OCS.15)
ms:contentKeyID: 49301457
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsVoiceConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Reimposta la configurazione vocale sui valori predefiniti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsVoiceConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con questo esempio la configurazione vocale Global (e solo questa) viene riportata ai valori predefiniti. Con questa operazione vengono eliminate tutte le configurazioni di test vocali definite, pertanto è stato aggiunto il parametro Confirm al fine di visualizzare un prompt che richiede di confermare l'operazione prima che abbia luogo la rimozione.

    Remove-CsVoiceConfiguration -Identity Global -Confirm

## Descrizione dettagliata

Le configurazioni di test vocali vengono utilizzate per verificare un numero di telefono rispetto a criteri vocali, route e dial plan specifici. Questo cmdlet rimuove solo la configurazione vocale globale, vale a dire un contenitore per tutte le configurazioni di test vocali definite per una distribuzione di Lync Server. Con la "rimozione", la configurazione vocale non viene realmente rimossa, in quanto l'istanza globale resta disponibile. In realtà, l'elenco di configurazioni di test vocali viene riportato all'impostazione predefinita, ovvero un elenco vuoto.

AVVISO: con la rimozione della configurazione vocale (che svuota l'elenco delle configurazioni di test vocali) vengono eliminate tutte le configurazioni di test vocali definite per una distribuzione di Lync Server. Dopo la chiamata a questo cmdlet, una chiamata al cmdlet **Get-CsVoiceTestConfiguration** non restituirà alcun risultato.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Remove-CsVoiceConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsVoiceConfiguration"}

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
<td><p>L'ambito della configurazione vocale da rimuovere. Questo valore deve essere Global.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceConfiguration. Accetta l'input tramite pipeline di un oggetto configurazione vocale.

## Tipi restituiti

Questo cmdlet rimuove (ripristina) un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoiceConfiguration.

## Vedere anche

#### Ulteriori risorse

[Set-CsVoiceConfiguration](set-csvoiceconfiguration.md)  
[Get-CsVoiceConfiguration](get-csvoiceconfiguration.md)  
[Remove-CsVoiceTestConfiguration](remove-csvoicetestconfiguration.md)  
[Get-CsVoiceTestConfiguration](get-csvoicetestconfiguration.md)

