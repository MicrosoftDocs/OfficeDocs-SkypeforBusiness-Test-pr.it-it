---
title: New-CsServerApplication
TOCTitle: New-CsServerApplication
ms:assetid: 045e6e65-8ad6-49af-8bfb-aa9045fa4dd8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398096(v=OCS.15)
ms:contentKeyID: 49299534
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsServerApplication

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova applicazione server. Le applicazioni server sono applicazioni ospitate da Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsServerApplication -Name <String> -Parent <String> <COMMON PARAMETERS>

    New-CsServerApplication -Identity <XdsIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -Uri <String> [-Confirm [<SwitchParameter>]] [-Critical <$true | $false>] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Priority <Int32>] [-Script <String>] [-ScriptName <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'Esempio 1 viene creata una nuova applicazione server con Identity EdgeServer:atl-edge-001.litwareinc.com/EdgeMonitor. Oltre a specificare l'identità (Identity), sono inclusi i parametri Uri e Critical. Questi parametri vengono utilizzati per specificare l'URI dell'applicazione e per indicare che l'applicazione non è considerata critica.

    New-CsServerApplication -Identity "EdgeServer:atl-edge-001.litwareinc.com/EdgeMonitor" -Uri http://www.litwareinc.com/edgemonitor -Critical $False

## ESEMPIO 2

I comandi riportati nell'esempio 2 dimostrano come creare una nuova applicazione server che inizialmente esiste solo in memoria. A tale scopo, il primo comando chiama il cmdlet **New-CsServerApplication** con due parametri: Identity (che specifica l'identità dell'applicazione) e InMemory (che indica che la nuova applicazione deve essere creata solo in memoria). L'oggetto applicazione server risultante viene quindi archiviato nella variabile $x.

Dopo la creazione di questa applicazione server virtuale, vengono utilizzati i comandi 2 e 3 per modificare rispettivamente i valori della proprietà Uri e della proprietà Critical. Il comando 4 infine viene utilizzato per trasformare l'applicazione server virtuale in un'applicazione server effettiva. Si noti che tale comando finale è obbligatorio. Se non si chiama il cmdlet **Set-CsServerApplication**, nessuna applicazione verrà configurata per EdgeServer:atl-edge-001.litwareinc.com/EdgeMonitor e l'applicazione virtuale verrà eliminata non appena si termina la sessione di Windows PowerShell o si elimina la variabile $x.

    $x = New-CsServerApplication -Identity "EdgeServer:atl-edge-001.litwareinc.com/EdgeMonitor" -InMemory
    $x.Uri = "http://www.litwareinc.com/edgemonitor"
    $x.Critical = $False
    Set-CsServerApplication -Instance $x

## Descrizione dettagliata

Le applicazioni server fanno riferimento ai singoli programmi eseguiti in Lync Server. Il cmdlet **New-CsServerApplication** consente agli amministratori di configurare nuove applicazioni server.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **New-CsServerApplication** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsServerApplication"}

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
<td><p>Identificatore univoco dell'applicazione server da creare. Le identità (Identity) dell'applicazione server sono composte dal servizio in cui viene ospitata l'applicazione e dal nome dell'applicazione. Ad esempio, l'applicazione server denominata QoEAgent potrebbe avere un'identità (Identity) simile alla seguente: service:Registrar:atl-cs-001.litwareinc.com/QoEAgent.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome descrittivo del servizio. Se si utilizza il parametro Identity, non è necessario includere il parametro Name durante la creazione di un nuovo servizio. Infatti, nella proprietà Name verrà automaticamente inserita la parte del nome dell'identità (Identity) dell'applicazione. Ad esempio, se si crea una nuova applicazione con Identity service:Registrar:atl-cs-001.litwareinc.com/TestService l'applicazione verrà denominata automaticamente TestService. Il parametro Name è obbligatorio solo se si utilizza il parametro Parent.</p></td>
</tr>
<tr class="odd">
<td><p><em>Parent</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Indica il servizio che ospiterà la nuova applicazione server. Se si utilizza il parametro Identity, non è necessario utilizzare il parametro Parent o il parametro Name perché l'identità (Identity) dell'applicazione combina i valori delle proprietà Parent e Name. Tuttavia, è possibile omettere il parametro Identity e utilizzare invece i parametri Parent e Name. In questo caso, il parametro Parent dovrà essere simile al seguente: -Parent &quot;Registrar:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Uri</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>URI (Uniform Resource Identifier) dell'applicazione. Ad esempio, l'applicazione QoEAgent ha l'URI http://www.microsoft.com/LCS/QoEAgent.</p></td>
</tr>
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
<td><p>Se impostato su True, Lync Server non verrà avviato a meno che l'applicazione non possa essere avviata. Se impostato su False, Lync Server verrà avviato indipendentemente dal fatto che l'applicazione possa essere avviata o meno. Se questo parametro non viene specificato, la proprietà Critical verrà impostata su True.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Impostare questo valore su True per abilitare l'applicazione. Impostare questo valore su False per disabilitare l'applicazione. Se questo parametro non viene specificato, la proprietà Enabled verrà impostata su False e la nuova applicazione risulterà disabilitata.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Indica l'ordine di esecuzione delle applicazioni server. L'applicazione con priorità 0 viene avviata per prima; l'applicazione con priorità 1 per seconda e così via. Si noti che ogni servizio che ospita un'applicazione server ha il proprio gruppo di priorità. Ad esempio, il servizio di registrazione può ospitare tre applicazioni con le corrispondenti priorità 0, 1 e 2. In modo simile, il servizio server perimetrale potrebbe avere 4 applicazioni con le priorità 0, 1, 2 e 3.</p>
<p>Se non si specifica una priorità, l'applicazione verrà aggiunta automaticamente nella parte inferiore dell'elenco delle priorità. Se si aggiunge o si rimuove un'applicazione, le priorità delle altre applicazioni verranno regolate di conseguenza. Ad esempio, se si elimina un'applicazione con priorità 0, l'applicazione che in precedenza aveva la priorità 1 avrà la priorità 0.</p></td>
</tr>
<tr class="odd">
<td><p><em>Script</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di associare l'applicazione server a uno script. Per aggiungere uno script a un'applicazione server, utilizzare una sintassi simile alla seguente:</p>
<p>-Script &quot;Update.ps1&quot;</p>
<p>Per rimuovere uno script, impostare semplicemente la proprietà Script su un valore Null:</p>
<p>-Script $Null</p>
<p>Ogni applicazione server può essere associata a un solo script.</p></td>
</tr>
<tr class="even">
<td><p><em>ScriptName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Percorso per lo script MSPL (Microsoft SIP Processing Language) utilizzato dall'applicazione (se presente). MSPL è un linguaggio di scripting utilizzato per filtrare ed eseguire il routing di messaggi SIP.</p></td>
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

Nessuno. Il cmdlet **New-CsServerApplication** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **New-CsServerApplication** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.ServerApplication.Application.

## Vedere anche

#### Ulteriori risorse

[Get-CsServerApplication](get-csserverapplication.md)  
[Remove-CsServerApplication](remove-csserverapplication.md)  
[Set-CsServerApplication](set-csserverapplication.md)

