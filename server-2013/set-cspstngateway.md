---
title: Set-CsPstnGateway
TOCTitle: Set-CsPstnGateway
ms:assetid: 5d61e7e5-dacb-4dd3-bdd5-b757d98181d3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398408(v=OCS.15)
ms:contentKeyID: 49300701
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPstnGateway

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica le proprietà di un gateway PSTN (Public Switched Telephone Network). I gateway PSTN consentono di eseguire il routing delle chiamate tra i dispositivi sulla rete PSTN esterna e i dispositivi sulla rete interna di VoIP aziendale. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsPstnGateway [-Identity <XdsGlobalRelativeIdentity>] [-AlternateByPassId <String>] [-Confirm [<SwitchParameter>]] [-Default <$true | $false>] [-Force <SwitchParameter>] [-GatewaySipClientTcpPort <UInt16>] [-GatewaySipClientTlsPort <UInt16>] [-MediationServer <String>] [-RepresentativeMediaIP <String>] [-Routable <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando illustrato nell'Esempio 1 consente di configurare il gateway PstnGateway:192.168.0.240 in modo che sia il gateway predefinito. Ciò significa che PstnGateway:192.168.0.240 può essere utilizzato per gestire le chiamate originate da Office Communications Server 2007 R2.

    Set-CsPstnGateway -Identity "PstnGateway:192.168.0.240" -Default $True

## ESEMPIO 2

Nell'esempio 2 vengono configurati tutti i gateway PSTN dell'organizzazione, in modo che ogni gateway possa essere utilizzato nel routing in uscita. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsService** e il parametro PstnGateway per restituire una raccolta di tutti i gateway PSTN attualmente in uso. Questa raccolta viene quindi inviata tramite pipe al cmdlet **ForEach-Object**. Il cmdlet **ForEach-Object** esegue il cmdlet **Set-CsPstnGateway** per ogni gateway della raccolta e per ognuno imposta la proprietà Routable su True.

    Get-CsService -PstnGateway | ForEach-Object {Set-CsPstnGateway -Identity $_.Identity -Routable $True}

## Descrizione dettagliata

I gateway PSTN consentono agli utenti di VoIP aziendale di effettuare e ricevere chiamate telefoniche da utenti che non si trovano sulla rete PSTN. Questi gateway fungono da collegamento tra Mediation Server e la rete PSTN.

Generalmente, è necessario utilizzare i gateway PSTN nei sistemi telefonici PBX (Private Branch Exchange) di tipo TDM (Time Division Multiplex); in questo caso, di norma è necessario utilizzare un PSTN e un Mediation Server per instradare le chiamate di VoIP aziendale alla rete PSTN. Al contrario, se si utilizza un sistema IP-PBX, è possibile creare una connessione SIP diretta tra il sistema PBX e Mediation Server, eliminando così la necessità di un gateway PSTN.

Dopo aver installato e configurato i gateway PSTN, è possibile gestirli utilizzando il cmdlet **Set-CsPstnGateway**.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsPstnGateway** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPstnGateway"}

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
<td><p><em>AlternateByPassId</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Identificatore univoco globale (GUID) che rappresenta l'ID bypass alternativo. Questo ID viene generato automaticamente da Lync Server e consente di eliminare le chiamate &quot;hairpin&quot;. A seconda della configurazione del sistema, questo parametro consente alle chiamate &quot;hairpin&quot; di ignorare automaticamente il Mediation Server senza che sia necessario definire e associare singole subnet a tutti i siti e a tutte le aree.</p>
<p>Per ottenere questo risultato, è necessario abilitare a livello globale la funzionalità di bypass in modo da utilizzare aree e siti di configurazione di rete e quindi abilitare la funzionalità di bypass sulla configurazione trunk del gateway PSTN.</p>
<p>Si parla di chiamata &quot;hairpin&quot; quando una chiamata in arrivo dalla rete PSTN viene reinstradata alla rete PSTN mediante la funzione di inoltro chiamata o di squillo simultaneo.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Default</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, questo gateway gestisce le chiamate da Office Communications Server 2007 R2. Nella raccolta di gateway gestiti da un unico Mediation Server, può essere presente un solo gateway predefinito.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di prompt di conferma o messaggi di errore non irreversibile che possono verificarsi quando si esegue il cmdlet.</p></td>
</tr>
<tr class="odd">
<td><p><em>GatewaySipClientTcpPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta di attesa utilizzata per comunicare con i server Mediation Server tramite protocollo TCP (Transmission Control Protocol). Il valore predefinito è 5066.</p></td>
</tr>
<tr class="even">
<td><p><em>GatewaySipClientTlsPort</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Porta di attesa utilizzata per comunicare con i server Mediation Server tramite protocollo TLS (Transport Layer Security). Il valore predefinito è 5067.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identità del servizio del gateway PSTN da modificare. Ad esempio: -Identity &quot;PstnGateway:192.168.0.240&quot;.</p>
<p>Si noti che è possibile non utilizzare il prefisso &quot;PstnGatewayServer:&quot; quando si specifica un gateway PSTN. Ad esempio: -Identity &quot;atl-cs-001.litwareinc.com&quot;.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>MediationServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Identità del servizio di Mediation Server da associare al gateway PSTN. Ad esempio: -MediationServer &quot;MediationServer:atl-cs-001.litwareinc.com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>RepresentativeMediaIP</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Indirizzo IP del processore multimediale associato al gateway, se l'ubicazione del processore è diversa dall'indirizzo di segnalazione. Entrambe le funzionalità di bypass multimediale e controllo di ammissione di chiamata (CAC) si basano sull'ubicazione del processore multimediale del gateway; per impostazione predefinita, questa ubicazione corrisponde all'indirizzo di segnalazione. Se le due ubicazioni sono diverse (ad esempio, il processore multimediale si trova presso un sito remoto e quello di segnalazione presso il sito centrale), è necessario configurare la proprietà RepresentativeMediaIP con l'indirizzo IP del processore multimediale.</p>
<p>Se presso un unico sito sono stati distribuiti più processori multimediali ciascuno con un proprio indirizzo IP, è possibile utilizzare uno qualsiasi di questi indirizzi IP per configurare la proprietà RepresentativeMediaIP.</p></td>
</tr>
<tr class="even">
<td><p><em>Routable</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, il gateway può essere utilizzato per il routing in uscita.</p></td>
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

Nessuno. Il cmdlet **Get-CsPstnGateway** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Set-CsPstnGateway** non restituisce alcun oggetto o valore. Modifica invece le istanze esistenti dell'oggetto Microsoft.Rtc.Management.Xds.DisplayPstnGateway.

## Vedere anche

#### Ulteriori risorse

[Get-CsService](get-csservice.md)

