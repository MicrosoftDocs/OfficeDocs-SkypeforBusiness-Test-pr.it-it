---
title: Remove-CsTrustedApplicationEndpoint
TOCTitle: Remove-CsTrustedApplicationEndpoint
ms:assetid: c9b96690-d8c2-47f7-bff3-706dbf68d75a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398837(v=OCS.15)
ms:contentKeyID: 49301945
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsTrustedApplicationEndpoint

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove l'endpoint di un'applicazione attendibile. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsTrustedApplicationEndpoint -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

L'esempio mostra la rimozione del contatto dell'endpoint con identità (in questo caso il nome visualizzato) Endpoint 1. Poiché le identità devono essere univoche, il comando rimuoverà al massimo un endpoint.

    Remove-CsTrustedApplicationEndpoint -Identity "Endpoint 1"

## ESEMPIO 2

In questo esempio vengono rimossi tutti gli endpoint delle applicazioni attendibili associati all'applicazione tapp2. È possibile eseguire questa operazione chiamando innanzitutto il cmdlet **Get-CsTrustedApplicationEndpoint** e passando l'ID tapp2 al parametro ApplicationId. Questa operazione restituirà una raccolta di endpoint associati all'applicazione attendibile tapp2. La raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsTrustedApplicationEndpoint**, che rimuove ogni endpoint della raccolta. Considerare che con questa chiamata al cmdlet **Get-CsTrustedApplicationEndpoint** è possibile che vengano recuperati gli endpoint con ID applicazione tapp2 da più pool, con la conseguente rimozione di endpoint delle applicazioni attendibili da più pool.

    Get-CsTrustedApplicationEndpoint -ApplicationId tapp2 | Remove-CsTrustedApplicationEndpoint

## Descrizione dettagliata

L'endpoint applicazione attendibile è un oggetto contatto di Active Directory che consente il routing delle chiamate verso un'applicazione attendibile. Questo cmdlet rimuove da Servizi di dominio Active Directory un oggetto contatto dell'endpoint esistente.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsTrustedApplicationEndpoint** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsTrustedApplicationEndpoint"}

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
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Identità (nome distinto del contatto), indirizzo SIP o nome visualizzato dell'endpoint applicazione da rimuovere.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
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

Oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADApplicationContact. Accetta l'input da pipeline di oggetti endpoint applicazione attendibile.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Rimuove un oggetto di tipo Microsoft.Rtc.Management.ADConnect.Schema.OCSADApplicationContact.

## Vedere anche

#### Ulteriori risorse

[New-CsTrustedApplicationEndpoint](new-cstrustedapplicationendpoint.md)  
[Set-CsTrustedApplicationEndpoint](set-cstrustedapplicationendpoint.md)  
[Get-CsTrustedApplicationEndpoint](get-cstrustedapplicationendpoint.md)

