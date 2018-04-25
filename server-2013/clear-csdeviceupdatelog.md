---
title: Clear-CsDeviceUpdateLog
TOCTitle: Clear-CsDeviceUpdateLog
ms:assetid: 9e549484-b79b-47ef-b83b-13a6e20b0c80
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412738(v=OCS.15)
ms:contentKeyID: 49301498
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Clear-CsDeviceUpdateLog

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Elimina tutti i file di controllo e di log del servizio Web Aggiornamento dispositivi la cui creazione è antecedente al numero di giorni specificato. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Clear-CsDeviceUpdateLog -DaysBack <Int32> -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di eseguire la connessione al servizio Web Aggiornamento dispositivi con Identity "service:WebServer:atl-cs-001.litwareinc.com" ed eliminare tutti i file di controllo e dei dispositivi creati più di 10 giorni prima.

    Clear-CsDeviceUpdateLog -Identity "service:WebServer:atl-cs-001.litwareinc.com" -DaysBack 10

## Descrizione dettagliata

Il servizio Web Aggiornamento dispositivi contiene un gran numero di file di log; tra questi vi sono i file di log dei controlli eseguiti dal servizio così come quelli caricati dai dispositivi client come, ad esempio, i cellulari. A seconda del numero di operazioni di aggiornamento dei dispositivi e del numero di dispositivi client presenti nell'organizzazione, in breve tempo il server potrebbe saturarsi con i file di log di questo servizio. Il cmdlet **Clear-CsDeviceUpdateLog** consente di ridurre il numero di file di log memorizzati sul server: è sufficiente utilizzare il cmdlet e specificare il tempo massimo (in giorni) di conservazione dei file. Superato quel periodo di tempo, i file di log vengono rimossi dal sistema.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Clear-CsDeviceUpdateLog** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Clear-CsDeviceUpdateLog"}

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
<td><p><em>DaysBack</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Int32</p></td>
<td><p>Numero massimo di giorni per la conservazione dei file di log. Una volta superato il valore specificato dal parametro DaysBack, i file di log verranno eliminati. Ad esempio, se si imposta DaysBack su 7, dopo 7 giorni di permanenza sul server i file di log verranno rimossi.</p>
<p>Questo parametro può essere impostato su qualsiasi numero intero compreso tra 1 e 30, inclusi.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco del servizio che ospita i file di log del servizio Web Aggiornamento dispositivi. Ad esempio, la seguente sintassi consente di eliminare i file di log del servizio Web Aggiornamento dispositivi da servizi Web per il pool atl-cs-001.litwareinc.com: -Identity &quot;service:WebServer:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Clear-CsDeviceUpdateLog** non accetta input tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Clear-CsDeviceUpdateLog** non restituisce alcun valore.

## Vedere anche

#### Ulteriori risorse

[Clear-CsDeviceUpdateFile](clear-csdeviceupdatefile.md)  
[Get-CsDeviceUpdateConfiguration](get-csdeviceupdateconfiguration.md)

