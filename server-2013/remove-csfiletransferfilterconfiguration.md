---
title: Remove-CsFileTransferFilterConfiguration
TOCTitle: Remove-CsFileTransferFilterConfiguration
ms:assetid: faae4d4b-ea8b-4d50-9c46-16a075476642
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413064(v=OCS.15)
ms:contentKeyID: 49302535
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsFileTransferFilterConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove la configurazione specificata del filtro di trasferimento dei file di messaggistica istantanea. Le impostazioni del filtro di trasferimento dei file di messaggistica istantanea vengono utilizzate per impedire a un utente di trasferire determinati tipi di file con un messaggio istantaneo. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsFileTransferFilterConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 il cmdlet **Remove-CsFileTransferFilterConfiguration** viene utilizzato per rimuovere la configurazione del filtro di trasferimento dei file con identità site:Redmond.

    Remove-CsFileTransferFilterConfiguration -Identity site:Redmond

## ESEMPIO 2

Nell'esempio 2 vengono rimosse tutte le configurazioni del filtro di trasferimento dei file nell'ambito del sito. Per eseguire questa attività, nel comando vengono innanzitutto utilizzati il cmdlet **Get-CsFileTransferFilterConfiguration** e il parametro Filter per restituire tutte le configurazioni nell'ambito del sito. Il valore del filtro "site:\*" indica al cmdlet **Get-CsFileTransferFilterConfiguration** di restituire solo le configurazioni in cui l'identità inizia con la stringa "site:". La raccolta filtrata delle configurazioni viene quindi inviata tramite pipe al cmdlet **Remove-CsFileTransferFilterConfiguration**, che elimina ogni elemento nella raccolta.

    Get-CsFileTransferFilterConfiguration -Filter site:* | Remove-CsFileTransferFilterConfiguration

## ESEMPIO 3

Nell'esempio 3 viene illustrato come rimuovere tutte le configurazioni del filtro di trasferimento dei file che sono attualmente disabilitate. A tal scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsFileTransferFilterConfiguration** per restituire una raccolta di tutte le configurazioni del filtro di trasferimento dei file che sono attualmente in uso nell'organizzazione. Tali informazioni vengono quindi inviate tramite pipe al cmdlet **Where-Object**, che seleziona solo le configurazioni del filtro di trasferimento dei file in cui la proprietà Enabled è uguale a (-eq) False ($False). La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsFileTransferFilterConfiguration**, che procede a rimuovere ogni elemento nella raccolta filtrata.

    Get-CsFileTransferFilterConfiguration | Where-Object {$_.Enabled -eq $False} | Remove-CsFileTransferFilterConfiguration

## Descrizione dettagliata

Durante l'invio di messaggi istantanei, gli utenti possono allegare e inviare file agli altri partecipanti alla conversazione. Tuttavia è possibile configurare Lync Server in modo che i file con determinate restrizioni, in genere le estensioni dei tipi di file che possono essere potenzialmente dannosi, non possano essere inviati tramite un client Lync Server.

Il cmdlet **Remove-CsFileTransferFilterConfiguration** consente di eliminare la configurazione di un filtro di trasferimento di file. Nel caso di configurazioni nell'ambito del sito, verranno rimosse dal cmdlet **Remove-CsFileTransferFilterConfiguration** e gli utenti del sito erediteranno automaticamente la configurazione globale del filtro di trasferimento dei file. Il cmdlet **Remove-CsFileTransferFilterConfiguration** può anche essere eseguito in relazione alla configurazione globale. In questo caso, però, la configurazione globale non verrà rimossa; in realtà, per tutti i valori delle proprietà in tale configurazione verranno ripristinati i valori predefiniti.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Remove-CsFileTransferFilterConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsFileTransferFilterConfiguration"}

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
<td><p>Identificatore univoco della configurazione del trasferimento dei file da rimuovere. Per fare riferimento alla configurazione globale, utilizzare la seguente sintassi: -Identity global. Per fare riferimento a una configurazione nell'ambito del sito, utilizzare una sintassi analoga alla seguente: -Identity site:Redmond. Non è possibile utilizzare valori con caratteri jolly per specificare un'identità.</p></td>
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
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.FileTransferFilterConfiguration. Accetta l'invio tramite pipe di oggetti di configurazione del filtro di trasferimento dei file.

## Tipi restituiti

Questo cmdlet non restituisce un valore o un oggetto. In realtà, il cmdlet rimuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.ImFilter.FileTransferFilterConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsFileTransferFilterConfiguration](new-csfiletransferfilterconfiguration.md)  
[Set-CsFileTransferFilterConfiguration](set-csfiletransferfilterconfiguration.md)  
[Get-CsFileTransferFilterConfiguration](get-csfiletransferfilterconfiguration.md)

