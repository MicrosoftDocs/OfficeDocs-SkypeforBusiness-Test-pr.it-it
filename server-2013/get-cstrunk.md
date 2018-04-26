---
title: Get-CsTrunk
TOCTitle: Get-CsTrunk
ms:assetid: c49407f2-2e03-4b8b-b51b-75b12ef87fd1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205244(v=OCS.15)
ms:contentKeyID: 49301890
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTrunk

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui trunk SIP utilizzati dall'organizzazione. I trunk SIP connettono la rete telefonica Voice over IP di Lync Server 2013 alla rete PSTN (Public Switched Telephone Network). Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Get-CsTrunk [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsTrunk [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-PoolFqdn <String>]

## Esempi

## ESEMPIO 1

Tramite il comando illustrato nell'esempio 1 vengono restituite informazioni per tutti i trunk SIP configurati per l'utilizzo nell'organizzazione.

    Get-CsTrunk

## ESEMPIO 2

Nell'esempio 2 vengono restituite informazioni per un singolo trunk SIP, ovvero il trunk con Identity PstnGateway:192.168.0.240.

    Get-CsTrunk -Identity "PstnGateway:192.168.0.240"

## ESEMPIO 3

Tramite il comando illustrato nell'esempio 3 vengono restituite informazioni per tutti i trunk SIP trovati nel pool atl-cs-001.litwareinc.com.

    Get-CsTrunk -PoolFqdn "atl-cs-001.litwareinc.com"

## ESEMPIO 4

Nell'esempio 4 vengono restituite informazioni per tutti i trunk SIP instradabili. A tale scopo, il comando chiama prima di tutto il cmdlet **Get-CsTrunk** senza parametri per restituire una raccolta di tutti i trunk SIP disponibili. Questa raccolta viene poi inviata tramite pipeline al cmdlet **Where-Object** che sceglie solo i trunk per cui la proprietà Routable è uguale a (-eq) True ($True).

    Get-CsTrunk | Where-Object {$_.Routable -eq $True}

## Descrizione dettagliata

In Microsoft Lync Server 2010 i trunk vengono utilizzati per instradare le chiamate da un Mediation Server a un gateway PSTN. Ogni gateway può essere assegnato a un singolo trunk, limitando tra l'altro gli amministratori, che in questo modo non possono garantire la resilienza per le chiamate in uscita. Poiché tuttavia i trunk e i gateway PSTN sono praticamente identici, è possibile recuperare informazioni su tutti i trunk utilizzando il comando seguente:

Get-CsService -PstnGateway

In Lync Server 2013 è ora possibile assegnare più trunk a un singolo gateway PSTN. In questo modo i gateway e i trunk non sono più praticamente identici. In Lync Server 2013 pertanto non è possibile recuperare informazioni dettagliate sui singoli trunk utilizzando il cmdlet **Get-CsService**. A tale scopo è necessario invece utilizzare il nuovo cmdlet **Get-CsTrunk**.

Si noti che nell'interfaccia della riga di comando Windows PowerShell le informazioni sui trunk sono di sola lettura. Non è possibile creare, eliminare o modificare i trunk utilizzando PowerShell. Queste operazioni possono essere eseguite solo utilizzando Generatore di topologie di Lync Server.

Per restituire un elenco di tutti i ruoli di controllo dell'accesso basato su ruoli (RBAC) a cui è stato assegnato questo cmdlet, inclusi quelli creati dall'utente stesso, eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsTrunk"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Get-CsTrunk** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare i caratteri jolly allo scopo di restituire un trunk SIP (o una raccolta di trunk SIP). Ad esempio, per restituire una raccolta di tutti i trunk SIP configurati come parte del servizio gateway PSTN, utilizzare la sintassi seguente:</p>
<p>-Filter &quot;PstnGateway:*&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificatore univoco per il trunk SIP da restituire. Esempio:</p>
<p>–Identity &quot;PstnGateway:192.168.0.240&quot;</p>
<p>Si noti che non è possibile utilizzare i caratteri jolly per specificare un'identità. Se è necessario utilizzare i caratteri jolly, includere il parametro Filter.</p>
<p>Se questo parametro non viene specificato, il cmdlet <strong>Get-CsTrunk</strong> restituisce una raccolta di tutti i trunk SIP utilizzati nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>PoolFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo del trunk o del gateway PSTN definito nella topologia, ad esempio:</p>
<p>-PoolFqdn &quot;atl-trunk-001.litwareinc.com&quot;</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsTrunk** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsTrunk** restituisce istanze dell'oggetto Microsoft.Rtc.Management.Xds.DisplayPstnGateway\#Decorated.

## Vedere anche

#### Ulteriori risorse

[Get-CsTrunkConfiguration](get-cstrunkconfiguration.md)

