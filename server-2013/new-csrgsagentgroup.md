---
title: New-CsRgsAgentGroup
TOCTitle: New-CsRgsAgentGroup
ms:assetid: faaf46f9-1063-4d64-a36f-872e657cd869
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413065(v=OCS.15)
ms:contentKeyID: 49302548
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRgsAgentGroup

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo gruppo di agenti di Response Group. Un gruppo di agenti è una raccolta di agenti assegnati alla coda di Response Group. Gli agenti sono gli utenti designati per rispondere alle chiamate indirizzate a una coda specifica. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsRgsAgentGroup -Name <String> -Parent <RgsIdentity> [-AgentAlertTime <Int16>] [-AgentsByUri <Collection>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-DistributionGroupAddress <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-ParticipationPolicy <Informal | Formal>] [-RoutingMethod <LongestIdle | Serial | Parallel | RoundRobin | Attendant>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 crea un nuovo gruppo di agenti di Response Group denominato Help Desk Group, situato nel servizio ApplicationServer:atl-cs-001.litwareinc.com. Per creare il gruppo, il comando chiama **New-CsRgsAgentGroup** con i parametri Parent e Name. In questo esempio, non vengono specificati altri parametri del gruppo, il che significa che il gruppo utilizzerà tutti i valori della proprietà predefiniti. Poiché a questo gruppo non è stato assegnato alcun agente, le chiamate instradate al nuovo gruppo di agenti verranno disconnesse automaticamente.

    New-CsRgsAgentGroup -Parent service:ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk Group"

## ESEMPIO 2

Nell'esempio 2 viene creato un nuovo gruppo di agenti di Response Group e, allo stesso tempo, a tale gruppo viene assegnata una coppia di agenti. A tale scopo, il comando chiama **New-CsRgsAgentGroup** con i parametri Parent e Name. Nell'esempio è inoltre incluso il parametro AgentsByUri accompagnato dal valore "sip:kenmyer@litwareinc.com","sip:pilarackerman@litwareinc.com". Tale valore è un elenco di indirizzi SIP delimitati da virgole da aggiungere al gruppo di agenti.

    New-CsRgsAgentGroup -Parent service: ApplicationServer:atl-cs-001.litwareinc.com -Name "Help Desk Group" -AgentsByUri "sip:kenmyer@litwareinc.com","sip:pilarackerman@litwareinc.com"

## Descrizione dettagliata

Quando viene chiamato un numero di telefono associato all'applicazione Response Group, quest'ultima innanzitutto determina quale flusso di lavoro corrisponde al numero chiamato. A seconda della configurazione del flusso di lavoro, la chiamata può essere instradata a un insieme di domande del sistema IVR (Interactive Voice Response), in cui al chiamante vengono poste una o più domande, ad esempio "La domanda riguarda il supporto hardware o software?"). In alternativa, la chiamata può essere messa in una coda di Response Group; qui il chiamante viene lasciato in attesa finché una persona designata non sia disponibile per rispondere alla chiamata. Le persone designate a rispondere alle chiamate sono dette agenti, e un gruppo di agenti viene chiamato gruppo di agenti di Response Group. I gruppi di agenti sono associati alle code e definiti in base a responsabilità lavorative simili: il personale del supporto tecnico può essere raggruppato nel gruppo di agenti Help Desk, mentre gli agenti del servizio clienti possono essere raggruppati nel gruppo di agenti Customer Support.

Se a una coda sono assegnati più gruppi, l'applicazione Response Group inizierà a chiamare tutti gli agenti disponibili del primo gruppo assegnato alla coda. Se nessuno di questi agenti risponde, l'applicazione inizierà quindi a chiamare tutti gli agenti disponibili del successivo gruppo assegnato alla coda.

È possibile creare nuovi gruppi di agenti utilizzando il cmdlet **New-CsRgsAgentGroup**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsRgsAgentGroup** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

    Get-CsAdminRole | Where-Object  {$_.Cmdlets -match "New-CsRgsAgentGroup"}

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
<td><p><em>Name</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome univoco da assegnare al gruppo di agenti. La combinazione della proprietà Parent e della proprietà Name consente di identificare in modo univoco i gruppi di agenti senza dover fare riferimento al relativo identificatore univoco globale (GUID).</p></td>
</tr>
<tr class="even">
<td><p><em>Parent</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.RgsIdentity</p></td>
<td><p>Servizio in cui verrà ospitato il nuovo gruppo di agenti. Ad esempio: -Parent &quot;service:ApplicationServer:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>AgentAlertTime</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int16</p></td>
<td><p>Rappresenta la quantità di tempo (in secondi) in cui una chiamata può restare senza risposta prima di essere instradata automaticamente all'agente successivo. Il parametro AgentAlertTime può essere impostato su un qualsiasi valore intero compreso tra 10 e 600 secondi (10 minuti) inclusi. Il valore predefinito è 20 secondi. <strong>Nota:</strong> il valore di questo parametro non può essere maggiore di 180 secondi. In caso contrario, l'applicazione client rifiuterà la chiamata per il raggiungimento del valore massimo di attesa da parte del timer delle transazioni SIP. Per evitare che si verifichi questo problema, impostare il parametro AgentAlertTime su un valore inferiore a 180 secondi.</p></td>
</tr>
<tr class="even">
<td><p><em>AgentsByUri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Collections.ObjectModel.Collection</p></td>
<td><p>Consente di aggiungere singoli agenti a un gruppo di agenti. Nuovi agenti vengono identificati utilizzando i relativi indirizzi SIP.</p>
<p>Si noti che è possibile selezionare solo utenti abilitati per VoIP aziendale.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente agli amministratori di fornire informazioni aggiuntive ed esplicative sul gruppo di agenti. Ad esempio, la Descrizione può contenere informazioni su chi contattare se il gruppo non riceve le chiamate telefoniche attese.</p></td>
</tr>
<tr class="odd">
<td><p><em>DistributionGroupAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di aggiungere tutti i membri di un gruppo di distribuzione a un gruppo di agenti.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>ParticipationPolicy</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.ParticipationPolicy</p></td>
<td><p>Indica se sono necessari o meno degli agenti per accedere formalmente al sistema e ricevere chiamate intese per il gruppo. Se ParticipationPolicy è impostato su Informal (il valore predefinito), l'account di accesso non è necessario. Se ParticipationPolicy è impostato su Formal, l'account di accesso è necessario.</p></td>
</tr>
<tr class="odd">
<td><p><em>RoutingMethod</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Rgs.Management.WritableSettings.RoutingMethod</p></td>
<td><p>Specifica il metodo utilizzato per indirizzare nuove chiamate agli agenti. RoutingMethod deve essere impostato su uno dei seguenti valori:</p>
<p>LongestIdle - Le chiamate vengono instradate all'agente rimasto più a lungo inattivo, ovvero non impegnato in un'attività di Lync.</p>
<p>RoundRobin - Le chiamate vengono indirizzate all'agente successivo nell'elenco.</p>
<p>Serial - Le chiamate vengono sempre instradate al primo agente dell'elenco e instradate ad altri agenti solo se tale persona non è disponibile o non risponde entro l'intervallo di tempo previsto.</p>
<p>Parallel - Le chiamate vengono instradate a tutti gli agenti contemporaneamente, tranne a quelli il cui stato di presenza indica che sono impegnati o comunque non disponibili.</p>
<p>Attendant - Le chiamate vengono instradate a tutti gli agenti contemporaneamente, anche se il relativo stato di presenza indica che sono impegnati o comunque non disponibili. L'unica eccezione si verifica quando un agente imposta la propria presenza su Non disturbare.</p>
<p>Il metodo di routing predefinito è Parallel.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. **New-CsRgsAgentGroup** non accetta l'input da pipeline.

## Tipi restituiti

**New-CsRgsAgentGroup** crea nuove istanze dell'oggetto Microsoft.Rtc.Rgs.Management.WritableSettings.AgentGroup.

## Vedere anche

#### Ulteriori risorse

[Get-CsRgsAgentGroup](get-csrgsagentgroup.md)  
[Remove-CsRgsAgentGroup](remove-csrgsagentgroup.md)  
[Set-CsRgsAgentGroup](set-csrgsagentgroup.md)

