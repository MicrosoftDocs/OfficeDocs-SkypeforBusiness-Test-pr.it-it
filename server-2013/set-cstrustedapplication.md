---
title: Set-CsTrustedApplication
TOCTitle: Set-CsTrustedApplication
ms:assetid: 35b2812b-43da-4a0a-88dc-960f3cab0dfc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425840(v=OCS.15)
ms:contentKeyID: 49300155
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTrustedApplication

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica le impostazioni di un'applicazione attendibile. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsTrustedApplication [-Identity <ExternalApplicationIdentity>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Port <Int32>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Questo esempio consente di modificare la porta per l'applicazione attendibile con valore Identity TrustPool.litwareinc.com/tapp2 nella porta 6200. Questo risultato viene ottenuto passando al cmdlet **Set-CsTrustedApplication** un parametro Identity TrustPool.litwareinc.com/tapp2. Questo parametro Identity è costituito dal nome del pool in cui si trova l'applicazione seguito dal nome (o ID) dell'applicazione. Viene quindi incluso il parametro Port, a cui viene assegnato il valore 6200, per modificare il valore esistente.

    Set-CsTrustedApplication -Identity TrustPool.litwareinc.com/tapp2 -Port 6200

## Descrizione dettagliata

Un'applicazione attendibile è un'applicazione sviluppata da terze parti alla quale è stato assegnato lo stato di attendibile per essere eseguita come parte di Lync Server, ma che non è parte integrante del prodotto. Questo cmdlet consente di modificare il numero della porta utilizzata dal servizio esterno che esegue l'applicazione.

Quando si utilizza questo cmdlet per modificare un'applicazione attendibile, è necessario specificare un valore per il parametro Identity. L'identità corrisponde al nome di dominio completo (FQDN) del pool in cui si trova l'applicazione seguito da una barra (/) seguita dall'ID dell'applicazione. Ad esempio, TrustPool.litwareinc.com/tapp2, dove TrustPool.litwareinc.com è l'FQDN del pool e tapp2 è l'ID dell'applicazione. Se si visualizza un'applicazione esistente chiamando il cmdlet **Get-CsTrustedApplication**, verrà visualizzato un ID molto più simile al seguente: TrustPool.litwareinc.com/urn:application:tapp2. Si noti il prefisso urn:application: prima del nome dell'applicazione (tapp2). Anche se questo prefisso fa parte dell'identità, non è necessario quando si specifica il valore per il parametro Identity.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsTrustedApplication** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –matches "Set-CsTrustedApplication\\b"}

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
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.ExternalApplicationIdentity</p></td>
<td><p>L'identificatore univoco dell'applicazione attendibile da modificare. I valori dell'identità devono essere immessi nel formato &lt;FQDN pool&gt;/&lt;ID applicazione&gt;, dove &quot;FQDN pool&quot; è il nome di dominio completo (FQDN) del pool in cui risiede l'applicazione e &quot;ID applicazione&quot; è il nome dell'applicazione.</p></td>
</tr>
<tr class="even">
<td><p><em>Port</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Il numero della porta sulla quale verrà eseguita l'applicazione.</p></td>
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

Oggetto Microsoft.Rtc.Management.Xds.DisplayTrustedApplication. Accetta input tramite pipeline da oggetti applicazione attendibile.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Consente di modificare un oggetto di tipo Microsoft.Rtc.Management.Xds.DisplayTrustedApplication.

## Vedere anche

#### Ulteriori risorse

[New-CsTrustedApplication](new-cstrustedapplication.md)  
[Remove-CsTrustedApplication](remove-cstrustedapplication.md)  
[Get-CsTrustedApplication](get-cstrustedapplication.md)

