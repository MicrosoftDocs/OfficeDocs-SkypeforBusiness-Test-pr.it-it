---
title: Update-CsAdminRole
TOCTitle: Update-CsAdminRole
ms:assetid: 42cc9cc2-c408-4d0c-814a-6c6367cba834
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204851(v=OCS.15)
ms:contentKeyID: 49300344
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Update-CsAdminRole

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Aggiorna le definizioni del controllo di accesso basato sui ruoli (RBAC) archiviate nel database di gestione centrale senza modificare altre tabelle del database. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Update-CsAdminRole [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 aggiorna le definizioni RBAC archiviate nel database di gestione centrale.

    Update-CsAdminRole

## Descrizione dettagliata

Il cmdlet **Update-CsAdminRole** consente di aggiornare le definizioni dei ruoli RBAC archiviate nel database di gestione centrale. Questo cmdlet viene utilizzato in genere in scenari di coesistenza/migrazione in cui il database di gestione centrale si trova in un pool di Microsoft Lync Server 2010.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Update-CsAdminRole"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Update-CsAdminRole** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p>Richiede la conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Evita la visualizzazione di eventuali messaggi di errore non grave che potrebbero essere generati nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando, senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Update-CsAdminRole** non accetta input da pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Update-CsAdminRole** non restituisce oggetti o dati.

