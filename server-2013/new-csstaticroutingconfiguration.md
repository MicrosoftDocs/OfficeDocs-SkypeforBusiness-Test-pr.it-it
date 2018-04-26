---
title: New-CsStaticRoutingConfiguration
TOCTitle: New-CsStaticRoutingConfiguration
ms:assetid: 30d1736f-990f-46e8-931f-9247cd988244
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425811(v=OCS.15)
ms:contentKeyID: 49300086
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsStaticRoutingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta di impostazioni di configurazione del routing statico. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsStaticRoutingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Route <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene creata una nuova raccolta di configurazioni di routing statico con identità (Identity) service:Registrar:atl-cs-001.litwareinc.com. Poiché nel comando non è incluso il parametro Route, alla nuova raccolta non verrà assegnata alcuna route statica.

    New-CsStaticRoutingConfiguration -Identity "service:Registrar:atl-cs-001.litwareinc.com" 

## ESEMPIO 2

I comandi riportati nell'esempio 2 creano una nuova route di proxy SIP che utilizza TCP come trasporto. Questa nuova route viene quindi aggiunta a una nuova raccolta di configurazione del routing statico. A tale scopo, il primo comando dell'esempio utilizza il cmdlet **New-CsStaticRoute** per creare una nuova route che punta al server dell'hop successivo con indirizzo IP 192.168.1.100. Questa nuova route (archiviata in una variabile nominata $x) utilizza inoltre la porta 8025 e il MatchUri "\*.litwareinc.com".

Viene quindi chiamato il cmdlet **New-CsStaticRoutingConfiguration** per creare una nuova raccolta (con identità service:Registrar:atl-cs-001.litwareinc.com), assegnando la route archiviata nella variabile $x alla proprietà Route della nuova raccolta.

    $x = New-CsStaticRoute -TCPRoute -Destination "192.168.0.100" -Port 8025 -MatchUri "*.litwareinc.com"
    
    New-CsStaticRoutingConfiguration -Identity "service:Registrar:atl-cs-001.litwareinc.com" -Route $x

## Descrizione dettagliata

Quando si invia un messaggio SIP a qualcuno, quel messaggio potrebbe dover attraversare più subnet e reti prima di essere consegnato; il percorso effettuato dal messaggio viene spesso chiamato "route". Nelle reti, esistono due tipi di route: dinamiche e statiche. Con le route dinamiche, i server utilizzano algoritmi per stabilire la prossima destinazione (prossimo hop) dove inoltrare il messaggio. Con le route statiche, il percorso del messaggio viene stabilito a priori dagli amministratori di sistema. Quando un messaggio viene ricevuto da un server, questo controlla l'indirizzo del messaggio e lo inoltra al prossimo server che è stato preconfigurato da un amministratore. Se configurate correttamente le route statiche aiutano ad assicurare una tempestiva ed accurata consegna del messaggio senza sovraccarico sul server. Lo svantaggio delle route statiche è rappresentato dal fatto che i messaggi non vengono dinamicamente reinstradati nel caso di un errore di rete.

Quando si installa Lync Server, viene automaticamente creata una raccolta globale di route statiche. È inoltre possibile utilizzare il cmdlet **New-CsStaticRoutingConfiguration** per creare raccolte aggiuntive nell'ambito del sito o del servizio (solo per il servizio di registrazione).

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **New-CsStaticRoutingConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsStaticRoutingConfiguration"}

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
<td><p>Identificatore univoco della nuova raccolta di route statiche da creare. Le nuove raccolte possono essere create solo nell'ambito di servizio e possono essere assegnate solo al servizio di registrazione. A causa di ciò, la Identity di una nuova raccolta sarà simile a questa: -Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot;.</p></td>
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
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>Route</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Route statiche individuali gestite nella raccolta. Le route che devono essere aggiunte a una raccolta possono essere o copiate da un'altra raccolta o create usando il cmdlet <strong>New-CsStaticRoute</strong>. Per informazioni dettagliate, vedere gli esempi in questo argomento.</p></td>
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

Nessuno. Il cmdlet **New-CsStaticRoutingConfiguration** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **New-CsStaticRoutingConfiguration** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.RoutingSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsStaticRoutingConfiguration](get-csstaticroutingconfiguration.md)  
[New-CsStaticRoute](new-csstaticroute.md)  
[Remove-CsStaticRoutingConfiguration](remove-csstaticroutingconfiguration.md)  
[Set-CsStaticRoutingConfiguration](set-csstaticroutingconfiguration.md)

