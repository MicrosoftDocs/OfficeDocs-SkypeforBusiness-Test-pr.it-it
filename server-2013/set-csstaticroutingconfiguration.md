---
title: Set-CsStaticRoutingConfiguration
TOCTitle: Set-CsStaticRoutingConfiguration
ms:assetid: 8f3e923e-f1e1-4a22-8252-5ef24fbc3cb3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398724(v=OCS.15)
ms:contentKeyID: 49301303
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsStaticRoutingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica una raccolta esistente di impostazioni di configurazione del routing statico. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsStaticRoutingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsStaticRoutingConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Route <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di copiare una route da una raccolta di route statiche globale e poi di assegnare quella route ad una seconda raccolta di route statiche, quella con l'identità service:Registrar:atl-cs-001.litwareinc.com. Per completare questa attività, il primo comando nell'esempio si collega alla raccolta globale e restituisce un oggetto di riferimento alle route con MatchUri litwareinc.com e MatchOnlyPhoneUri uguali a a True.

A tale scopo, il comando chiama il cmdlet **Get-CsStaticRoutingConfiguration** per restituire informazioni dalla raccolta di configurazioni del routing statico nell'ambito globale. Questi dati vengono quindi inviati tramite pipe al **Select-Object**, che utilizza il parametro ExpandProperty per espandere i valori della proprietà Route. Il valori espansi (che rappresentano le route assegnate alla raccolta) vengono quindi inviati tramite pipe al cmdlet **Where-Object**, che seleziona la route in cui la proprietà MatchUri è uguale a litwareinc.com e la proprietà MatchOnlyPhoneUri è uguale a True. La route restituita viene archiviata in una variabile denominata $x.

Dopo che è stata recuperata la route, il secondo comando nell'esempio la aggiunge alla raccolta service: Registrar:atl-cs-001.litwareinc.com. A tale scopo, viene chiamato il cmdlet **Set-CsStaticRoutingConfiguration** con il parametro Route. Il valore di parametro @{Add=$x} indica al cmdlet **Set-CsStaticRoutingConfiguration** di aggiungere la route archiviata nella variabile $x alla raccolta contenuta nella proprietà Route.

    $x = Get-CsStaticRoutingConfiguration -Identity global | Select-Object -ExpandProperty Route | Where-Object {$_.MatchUri -eq "litwareinc.com" -and $_.MatchOnlyPhoneUri -eq $True}
    
    Set-CsStaticRoutingConfiguration -Identity service:Registrar:atl-cs-001.litwareinc.com -Route @{Add=$x}

## ESEMPIO 2

Il comando riportato nell'esempio 2 elimina una route da una raccolta di route statiche. A tale scopo, il primo comando dell'esempio si connette alla raccolta con identità (Identity) service:Registrar:atl-cs-001.litwareinc.com e restituisce un riferimento oggetto alla route con MatchUri litwareinc.com e MatchOnlyPhoneUri uguale a True. A tale scopo, il comando chiama il cmdlet **Get-CsStaticRoutingConfiguration** per restituire informazioni dalla raccolta service:Registrar:atl-cs-001.litwareinc.com. Questi dati vengono quindi inviati tramite pipe al cmdlet **Select-Object**, che utilizza il parametro ExpandProperty per espandere i valori della proprietà Route. I valori espansi (che rappresentano le singole route assegnate alla raccolta) vengono quindi inviati tramite pipe al cmdlet **Where-Object**, che seleziona solo le route in cui la proprietà MatchUri è uguale a litwareinc.com e la proprietà MatchOnlyPhoneUri è uguale a True. La route restituita viene archiviata in una variabile denominata $x.

Dopo che è stata recuperata, la route viene eliminata con il secondo comando dalla raccolta. A tale scopo, viene chiamato il cmdlet **Set-CsStaticRoutingConfiguration** insieme al parametro Route. Il valore di parametro @{Remove=$x} indica al cmdlet **Set-CsStaticRoutingConfiguration** di eliminare la route archiviata nella variabile $x.

    $x = Get-CsStaticRoutingConfiguration -Identity service:Registrar:atl-cs-001.litwareinc.com | Select-Object -ExpandProperty Route | Where-Object {$_.MatchUri -eq "litwareinc.com" -and $_.MatchOnlyPhoneUri -eq $True}
    
    Set-CsStaticRoutingConfiguration -Identity service:Registrar:atl-cs-001.litwareinc.com -Route @{Remove=$x}

## ESEMPIO 3

L'Esempio 3 mostra come rimuovere tutte route assegnate ad una raccolta di configurazioni di route statiche. Per ottenere questo risultato, includere il parametro Route ed impostare il suo valore su null. Al termine del comando, la raccolta esiste ancora ma nessuna route è rimasta assegnata a questa raccolta.

    Set-CsStaticRoutingConfiguration -Identity service:Registrar:atl-cs-001.litwareinc.com -Route $Null

## Descrizione dettagliata

Quando si invia un messaggio SIP a qualcuno, quel messaggio potrebbe dover attraversare più subnet e reti prima di essere consegnato; il percorso effettuato dal messaggio viene spesso chiamato "route". Nelle reti esistono due tipi di route, dinamiche e statiche. Con le route dinamiche, i server utilizzano algoritmi per stabilire la prossima destinazione (prossimo hop) in cui inoltrare il messaggio. Con le route statiche, il percorso del messaggio viene stabilito a priori dagli amministratori di sistema. Quando un messaggio viene ricevuto da un server, questo controlla l'indirizzo del messaggio e lo inoltra al prossimo server che è stato preconfigurato da un amministratore. Se configurate correttamente le route statiche aiutano ad assicurare una tempestiva ed accurata consegna del messaggio senza sovraccarico sul server. Lo svantaggio delle route statiche è rappresentato dal fatto che i messaggi non vengono dinamicamente reinstradati nel caso di un errore di rete.

Quando si installa Lync Server, viene creata automaticamente una raccolta globale di route statiche. La raccolta viene creata, ma non le vengono assegnate route. Il software inoltre consente di creare raccolte aggiuntive applicate all'ambito del servizio. Queste nuove raccolte possono essere assegnate solo al servizio di registrazione. Il cmdlet **Set-CsStaticRoutingConfiguration** consente di modificare i valori delle proprietà di una raccolta di routing statico esistente. Ciò significa che è possibile utilizzare il cmdlet per aggiungere nuove route a una raccolta o per eliminare route esistenti da una raccolta.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsStaticRoutingConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsStaticRoutingConfiguration"}

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
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco della raccolta di configurazioni di route statiche da modificare. Per modificare la raccolta globale, utilizzare la seguente sintassi: -Identity global. Per modificare una raccolta applicata nell'ambito del servizio, utilizzare una sintassi simile alla seguente: -Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot;. Non è consentito utilizzare i caratteri jolly per specificare l'identità.</p>
<p>Se non viene incluso questo parametro, il cmdlet <strong>Set-CsStaticRoutingConfiguration</strong> modificherà automaticamente la raccolta globale.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto RoutingSettings</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Route</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Route statiche individuali gestite nella raccolta. Le route da aggiungere ad una raccolta possono essere copiate da un'altra raccolta o create utilizzando il cmdlet <strong>New-CsStaticRoute</strong> per eliminare una route da una raccolta si deve prima creare un oggetto di riferimento a quella route. Per informazioni dettagliate, vedere la sezione Esempi in questo argomento.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.RoutingSettings. Il cmdlet **Set-CsStaticRoutingConfiguration** accetta le istanze dell'oggetto impostazioni di routing statico inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CsStaticRoutingConfiguration** non restituisce alcun oggetto o valore. Configura invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.RoutingSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsStaticRoutingConfiguration](get-csstaticroutingconfiguration.md)  
[New-CsStaticRoute](new-csstaticroute.md)  
[New-CsStaticRoutingConfiguration](new-csstaticroutingconfiguration.md)  
[Remove-CsStaticRoutingConfiguration](remove-csstaticroutingconfiguration.md)

