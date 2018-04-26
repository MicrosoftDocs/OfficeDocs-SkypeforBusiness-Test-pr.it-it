---
title: Clear-CsDeviceUpdateFile
TOCTitle: Clear-CsDeviceUpdateFile
ms:assetid: 34c5bb61-fcba-4e93-bb21-83b9611f3045
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425835(v=OCS.15)
ms:contentKeyID: 49300139
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Clear-CsDeviceUpdateFile

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Elimina i file di aggiornamento dei dispositivi rifiutati e non più associati ad alcun dispositivo. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Clear-CsDeviceUpdateFile -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di eliminare tutti i file di aggiornamento dei dispositivi dal servizio WebServer:atl-cs-001.litwareinc.com che non sono più associati al dispositivo.

    Clear-CsDeviceUpdateFile -Identity "service:WebServer:atl-cs-001.litwareinc.com"

## Descrizione dettagliata

Ogni volta che sul sistema vengono caricati degli aggiornamenti dei dispositivi, viene creata una corrispondente regola di aggiornamento dei dispositivi. Per impostazione predefinita, questa nuova regola di aggiornamento dei dispositivi viene assegnata allo stato Pending; ciò significa che la regola può essere scaricata e installata su dispositivi di prova ma non su dispositivi in produzione. In questo modo, è possibile provare gli aggiornamenti prima di renderli disponibili agli utenti. Se il test riesce, è possibile utilizzare il cmdlet **Approve-CsDeviceUpdateRule** per rendere questo aggiornamento disponibile agli utenti.

Se il test non riesce, è possibile utilizzare il cmdlet **Reset-CsDeviceUpdateRule** o **Restore-CsDeviceUpdateRule** per rifiutare un aggiornamento. Quando si eseguono questi cmdlet, l'aggiornamento dei dispositivi viene dissociato dalla regola corrispondente. A quel punto, gli amministratori possono utilizzare il cmdlet **Clear-CsDeviceUpdateFile** per rimuovere dal server gli aggiornamenti dissociati.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Clear-CsDeviceUpdateFile** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Clear-CsDeviceUpdateFile"}

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
<td><p>Identificatore univoco del servizio che ospita i file di aggiornamento dei dispositivi. Ad esempio, questa sintassi consente di eliminare i file di aggiornamento dei dispositivi dal servizio servizi Web per il pool atl-cs-001.litwareinc.com: -Identity &quot;service:WebServer:atl-cs-001.litwareinc.com&quot;.</p></td>
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
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
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

Nessuno. Il cmdlet **Clear-CsDeviceUpdateFile** non accetta input da pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Clear-CsDeviceUpdateFile** non restituisce alcun valore.

## Vedere anche

#### Ulteriori risorse

[Clear-CsDeviceUpdateLog](clear-csdeviceupdatelog.md)  
[Get-CsDeviceUpdateConfiguration](get-csdeviceupdateconfiguration.md)

