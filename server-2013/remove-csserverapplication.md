---
title: Remove-CsServerApplication
TOCTitle: Remove-CsServerApplication
ms:assetid: 55325d8c-9c67-4e88-868d-ce62bc11322e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398366(v=OCS.15)
ms:contentKeyID: 49300561
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsServerApplication

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un'applicazione server esistente. Le applicazioni server sono applicazioni ospitate da Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsServerApplication -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con l'esempio 1 viene rimossa l'applicazione server con identità service:EdgeServer:atl-edge-001.litwareinc.com/EdgeMonitor Poiché le identità devono essere univoche, il comando non eliminerà mai più di una applicazione.

    Remove-CsServerApplication -Identity "service:EdgeServer:atl-edge-001.litwareinc.com/EdgeMonitor"

## ESEMPIO 2

Nell'esempio 2 vengono rimosse tutte le applicazioni server non critiche. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsServerApplication** per restituire una raccolta di tutte le applicazioni server attualmente in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le applicazioni in cui la proprietà Critical è uguale a False. Tale raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsServerApplication**, che elimina ogni elemento della raccolta.

    Get-CsServerApplication | Where-Object {$_.Critical -eq $False} | Remove-CsServerApplication

## ESEMPIO 3

Nell'esempio 3 vengono eliminate tutte le applicazioni server configurate per l'utilizzo da parte del servizio EdgeServer:atl-cs-001.litwareinc.com. A tale scopo, viene utilizzato il cmdlet **Get-CsServerApplication** con il parametro Filter. Il valore di filtro "service:EdgeServer:atl-cs-001.litwareinc.com/\*" restituisce tutte le applicazioni la cui identità inizia con i caratteri "service:EdgeServer:atl-cs-001.litwareinc.com/". A sua volta, la raccolta viene inviata tramite pipe al cmdlet **Remove-CsServerApplication**, che elimina ogni applicazione da EdgeServer:atl-cs-001.litwareinc.com.

    Get-CsServerApplication -Filter "service:EdgeServer:atl-cs-001.litwareinc.com/*" | Remove-CsServerApplication

## Descrizione dettagliata

Le applicazioni server fanno riferimento ai singoli programmi che vengono eseguiti in Lync Server. Il cmdlet **Remove-CsServerApplication** consente agli amministratori di rimuovere qualsiasi applicazione in esecuzione come parte di Lync Server. L'eliminazione di un'applicazione server non equivale alla disinstallazione dell'applicazione. Quando si esegue il cmdlet **Remove-CsServerApplication**, l'applicazione non viene più eseguita in Lync Server. Il software tuttavia non viene disinstallato e l'applicazione può essere abilitata di nuovo eseguendo il cmdlet **New-CsServerApplication**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Remove-CsServerApplication** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsServerApplication }

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
<td><p>Un identificatore univoco per l'applicazione server da rimuovere. Le identità delle applicazioni server sono composte dal servizio in cui è ospitata l'applicazione seguito dal nome dell'applicazione. Ad esempio, il server applicazioni denominato QoEAgent può avere un'identità analoga alla seguente: service:Registrar:atl-cs-001.litwareinc.com/QoEAgent.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.ServerApplication.Application. Il cmdlet **Remove-CsServerApplication** accetta le istanze dell'oggetto applicazione server inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Remove-CsServerApplication** elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.ServerApplication.Application.

## Vedere anche

#### Ulteriori risorse

[Get-CsServerApplication](get-csserverapplication.md)  
[New-CsServerApplication](new-csserverapplication.md)  
[Set-CsServerApplication](set-csserverapplication.md)

