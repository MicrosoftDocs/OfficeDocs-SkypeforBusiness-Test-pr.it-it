---
title: Set-CsServerApplication
TOCTitle: Set-CsServerApplication
ms:assetid: b0f75629-b6c3-4958-b466-6c8a2f104819
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412850(v=OCS.15)
ms:contentKeyID: 49301691
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsServerApplication

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica i valori delle proprietà di un'applicazione server esistente. Le applicazioni server sono applicazioni ospitate da Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsServerApplication [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsServerApplication [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Critical <$true | $false>] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-Priority <Int32>] [-Script <String>] [-ScriptName <String>] [-Uri <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando illustrato nell'esempio 1 abilita l'applicazione server che presenta l'identità Registrar:atl-cs-001.litwareinc.com/ExumRouting. Poiché le identità devono essere univoche, il comando abiliterà una singola applicazione server.

    Set-CsServerApplication -Identity "Registrar:atl-cs-001.litwareinc.com/ExumRouting" -Enabled $True

## ESEMPIO 2

Nell'esempio 2 vengono abilitate tutte le applicazioni server attualmente disabilitate. A tale scopo, nel comando viene innanzitutto chiamato il cmdlet **Get-CsServerApplication** per restituire una raccolta di tutte le applicazioni server attualmente in uso nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona unicamente le applicazioni in cui la proprietà Enabled è uguale a False. La raccolta filtrata viene a sua volta inviata tramite pipe al cmdlet **Set-CsServerApplication**, che seleziona ogni elemento della raccolta e imposta la proprietà Enabled su True.

    Get-CsServerApplication | Where-Object {$_.Enabled -eq $False} | Set-CsServerApplication -Enabled $True

## Descrizione dettagliata

Le applicazioni server fanno riferimento ai singoli programmi eseguiti in Lync Server. Il cmdlet **Set-CsServerApplication** consente agli amministratori di modificare i valori delle proprietà di qualsiasi applicazione eseguita come parte di Lync Server.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsServerApplication** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsServerApplication"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Critical</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True (valore predefinito), Lync Server non verrà avviato se non è possibile avviare l'applicazione in questione. Se False, Lync Server verrà inviato indipendentemente dal fatto che sia possibile avviare l'applicazione o meno.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Impostare questo valore su True per abilitare l'applicazione. Impostare questo valore su False per disabilitare l'applicazione.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per il server applicazioni da modificare. Le identità delle applicazioni server sono composte dal servizio in cui è ospitata l'applicazione seguito dal nome dell'applicazione. Ad esempio, il server applicazioni denominato QoEAgent può avere un'identità analoga alla seguente: Registrar:atl-cs-001.litwareinc.com/QoEAgent.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto ServerApplication.Application</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Priority</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Indica l'ordine di esecuzione delle applicazioni server. L'applicazione con priorità 0 viene avviata per prima, l'applicazione con priorità 1 per seconda e così via. Ogni servizio che ospita un'applicazione server presenta il proprio set univoco di priorità. Il servizio di registrazione ad esempio può ospitare tre applicazioni con priorità corrispondenti pari a 0, 1 e 2. Analogamente, il servizio server perimetrale può disporre di 4 applicazioni con le priorità 0, 1, 2 e 3.</p>
<p>Se non si specifica una priorità, l'applicazione verrà automaticamente aggiunta al fondo dell'elenco delle priorità. Se si aggiunge o rimuove un'applicazione, le priorità delle altre applicazioni verranno modificate di conseguenza. Se ad esempio si elimina un'applicazione con priorità 0, per l'applicazione che precedentemente presentava la priorità 1 verrà automaticamente impostata la priorità 0.</p></td>
</tr>
<tr class="even">
<td><p><em>Script</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di associare l'applicazione server a uno script. Per aggiungere uno script a un'applicazione server, utilizzare una sintassi simile alla seguente:</p>
<p>-Script &quot;Update.ps1&quot;</p>
<p>Per rimuovere uno script, è sufficiente impostare la proprietà Script su un valore Null:</p>
<p>-Script $Null</p>
<p>Ogni applicazione server può essere associata a un solo script.</p></td>
</tr>
<tr class="odd">
<td><p><em>ScriptName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Percorso dello script MSPL (Microsoft SIP Processing Language) utilizzato dall'applicazione. MSPL è un linguaggio di scripting utilizzato per filtrare e instradare i messaggi SIP.</p></td>
</tr>
<tr class="even">
<td><p><em>Uri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URI (Uniform Resource Identifier) univoco dell'applicazione. Ad esempio, l'applicazione QoEAgent presenta l'URI http://www.microsoft.com/LCS/QoEAgent.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.ServerApplication.Application. Il cmdlet **Set-CsServerApplication** accetta istanze dell'oggetto applicazione server inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CsServerApplication** non restituisce un valore o un oggetto. Configura invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.ServerApplication.application.

## Vedere anche

#### Ulteriori risorse

[Get-CsServerApplication](get-csserverapplication.md)  
[New-CsServerApplication](new-csserverapplication.md)  
[Remove-CsServerApplication](remove-csserverapplication.md)

