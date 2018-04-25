---
title: Remove-CsTrustedApplication
TOCTitle: Remove-CsTrustedApplication
ms:assetid: 0d441b74-324b-4dab-8bd6-7d0a7eb18d28
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398176(v=OCS.15)
ms:contentKeyID: 49299667
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsTrustedApplication

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un'applicazione attendibile dal servizio trusted associato. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsTrustedApplication -Identity <ExternalApplicationIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene rimossa dal servizio trusted associato l'applicazione attendibile con Identity TrustPool.litwareinc.com/tapp2.

    Remove-CsTrustedApplication -Identity TrustPool.litwareinc.com/tapp2

## ESEMPIO 2

Nell'esempio 2 vengono rimosse tutte le applicazioni attendibili le cui identità includono la stringa "trust". Il comando innanzitutto chiama il cmdlet **Get-CsTrustedApplication**, passando il valore di filtro \*trust\*. Questo comando recupererà tutte le applicazioni attendibili aventi la stringa "trust" in qualunque posizione all'interno dell'identità. La raccolta di applicazioni attendibili recuperata viene quindi inviata tramite pipe al cmdlet **Remove-CsTrustedApplication**, che rimuove ogni applicazione attendibile nella raccolta. Si noti che l'applicazione non viene in realtà eliminata. Ne viene solo rimossa l'associazione al pool di applicazioni attendibili e al servizio trusted.

    Get-CsTrustedApplication -Filter *trust* | Remove-CsTrustedApplication

## Descrizione dettagliata

Un'applicazione attendibile è un'applicazione sviluppata da terze parti alla quale è stato assegnato lo stato di attendibile per essere eseguita come parte di Lync Server, ma che non è parte integrante del prodotto. Questo cmdlet rimuove un'applicazione attendibile da un pool di applicazioni attendibili. Si noti che l'applicazione non viene in realtà eliminata, ne viene solo rimossa l'associazione con il pool di applicazioni attendibili e il servizio trusted.

Quando si utilizza questo cmdlet per rimuovere un'applicazione attendibile, è necessario specificare un valore per il parametro Identity. L'identità corrisponde al nome di dominio completo (FQDN) del pool in cui si trova l'applicazione seguito da una barra (/) seguita dall'ID dell'applicazione. Ad esempio, TrustPool.litwareinc.com/tapp2, dove TrustPool.litwareinc.com è l'FQDN del pool e tapp2 è l'ID dell'applicazione. Se si visualizza un'applicazione esistente chiamando il cmdlet **Get-CsTrustedApplication**, verrà visualizzato un ID molto più simile al seguente: TrustPool.litwareinc.com/urn:application:tapp2. Si noti il prefisso urn:application: prima del nome dell'applicazione(tapp2). Anche se questo prefisso fa parte dell'identità, non è necessario quando si specifica il valore per il parametro Identity.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Remove-CsTrustedApplication** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsTrustedApplication\\b"}

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
<td><p>Microsoft.Rtc.Management.Xds.ExternalApplicationIdentity</p></td>
<td><p>L'identificatore univoco dell'applicazione attendibile da rimuovere dal pool di applicazioni attendibili. I valori dell'identità devono essere immessi nel formato &lt;FQDN pool&gt;/&lt;ID applicazione&gt;, dove &quot;FQDN pool&quot; è il nome di dominio completo (FQDN) del pool in cui risiede l'applicazione e &quot;ID applicazione&quot; è il nome dell'applicazione.</p></td>
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
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
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

Oggetto Microsoft.Rtc.Management.Xds.DisplayTrustedApplication. Accetta input tramite pipeline da oggetti applicazione attendibile.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Rimuove un oggetto di tipo Microsoft.Rtc.Management.Xds.DisplayTrustedApplication.

## Vedere anche

#### Ulteriori risorse

[New-CsTrustedApplication](new-cstrustedapplication.md)  
[Set-CsTrustedApplication](set-cstrustedapplication.md)  
[Get-CsTrustedApplication](get-cstrustedapplication.md)

