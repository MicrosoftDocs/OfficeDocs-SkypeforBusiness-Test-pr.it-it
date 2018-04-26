---
title: Remove-CsStaticRoutingConfiguration
TOCTitle: Remove-CsStaticRoutingConfiguration
ms:assetid: 844e849e-a2f6-42fd-a49c-1ab234a07a65
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398668(v=OCS.15)
ms:contentKeyID: 49301182
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsStaticRoutingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove la raccolta specificata di impostazioni di configurazione del routing statico. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsStaticRoutingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con il comando nell'esempio 1 viene rimossa la raccolta di configurazioni del routing statico con identità service:Registrar:atl-cs-001.litwareinc.com.

    Remove-CsStaticRoutingConfiguration -Identity "service:Registrar:atl-cs-001.litwareinc.com"

## ESEMPIO 2

Con l'esempio 2 vengono rimosse tutte le raccolte di configurazioni del routing statico applicate nell'ambito del servizio. A tale scopo, il comando utilizza inizialmente il cmdlet **Get-CsStaticRoutingConfiguration** con il parametro Filter. Il valore di filtro "service:\*" circoscrive i dati restituiti limitandoli alle raccolte in cui l'identità (Identity) inizia con il valore stringa "service:". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsStaticRoutingConfiguration**, che elimina ogni elemento presente nella raccolta.

    Get-CsStaticRoutingConfiguration -Filter "service:*" | Remove-CsStaticRoutingConfiguration

## ESEMPIO 3

Con l'esempio 3 viene mostrato come eliminare tutte le raccolte di configurazioni del routing statico a cui non sono state assegnate route effettive. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsStaticRoutingConfiguration** per restituire le informazioni su tutte le raccolte di routing statico in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che recupera solo le raccolte in cui il numero di route (Route.Count) è uguale a 0. Le informazioni filtrate vengono quindi inviate tramite pipe al cmdlet **Remove-CsStaticRoutingConfiguration**, che elimina ogni raccolta a cui non è stata assegnata almeno una route.

    Get-CsStaticRoutingConfiguration | Where-Object {$_.Route.Count -eq 0} | Remove-CsStaticRoutingConfiguration

## Descrizione dettagliata

Quando si invia un messaggio SIP, il messaggio potrebbe dover attraversare molteplici subnet e reti prima di essere recapitato; il percorso seguito dal messaggio è spesso definito route. Nelle reti esistono due tipi di route: dinamiche e statiche. Con il routing dinamico, i server utilizzano algoritmi per determinare la posizione successiva (vale a dire l'hop successivo) a cui dovrebbe essere inoltrato un messaggio. Con il routing statico, i percorsi seguiti dai messaggi sono determinati anticipatamente dagli amministratori di sistema. Quando riceve un messaggio, il server controlla l'indirizzo del messaggio e inoltra il messaggio stesso al server dell'hop successivo configurato anticipatamente da un amministratore. Se la configurazione è corretta, le route statiche aiutano a garantire un recapito tempestivo e accurato dei messaggi, applicando un sovraccarico minimo sui server. Lo svantaggio delle route statiche è dovuto al fatto che i messaggi non vengono reinstradati in modo dinamico se si verifica un errore di rete.

Quando si installa Lync Server, viene automaticamente creata una raccolta globale di route statiche. Le route non vengono tuttavia assegnate alla raccolta creata. Il software inoltre consente di creare raccolte aggiuntive applicate all'ambito del servizio. Queste nuove raccolte possono essere assegnate esclusivamente al servizio di registrazione. Se in seguito si cambia idea, è possibile utilizzare il cmdlet **Remove-CsStaticRoutingConfiguration** per eliminare le raccolte applicate all'ambito del servizio.

Il cmdlet **Remove-CsStaticRoutingConfiguration** può anche essere eseguito per la raccolta globale. In questo caso però la raccolta globale non viene rimossa, perché Lync Server non consente di rimuovere le raccolte globali. Tutte le proprietà della raccolta globale vengono invece reimpostate sui valori predefiniti. In questo modo tutte le route assegnate alla raccolta globale verranno eliminate.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Remove-CsStaticRoutingConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsStaticRoutingConfiguration"}

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
<td><p>Identificatore univoco della raccolta di configurazioni del routing statico da rimuovere. Per rimuovere una raccolta configurata nell'ambito del servizio, utilizzare una sintassi simile a quella riportata di seguito: -Identity &quot;service:Registrar:atl-cs-001.litwareinc.com&quot;.</p>
<p>Il cmdlet <strong>Remove-CsStaticRoutingConfiguration</strong> può essere eseguito anche per la raccolta globale. A tale scopo, utilizzare la sintassi riportata di seguito: -Identity global. Considerare tuttavia che la raccolta globale non verrà effettivamente eliminata. In realtà verranno ripristinati i valori predefiniti delle proprietà nella raccolta. Tutti gli elementi nella proprietà Route pertanto verranno eliminati.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.RoutingSettings. Il cmdlet **Remove-CsStaticRoutingConfiguration** accetta istanze dell'oggetto impostazioni di routing statico inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Remove-CsStaticRoutingConfiguration** non restituisce alcun oggetto o valore. Il cmdlet invece elimina le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SipProxy.RoutingSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsStaticRoutingConfiguration](get-csstaticroutingconfiguration.md)  
[New-CsStaticRoutingConfiguration](new-csstaticroutingconfiguration.md)  
[Set-CsStaticRoutingConfiguration](set-csstaticroutingconfiguration.md)

