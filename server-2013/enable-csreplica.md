---
title: Enable-CsReplica
TOCTitle: Enable-CsReplica
ms:assetid: 4a745da5-5b09-4b5a-8ab6-8b8b03d7afc6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425965(v=OCS.15)
ms:contentKeyID: 49300436
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Enable-CsReplica

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Aggiunge il computer locale al percorso di replica di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Enable-CsReplica [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 aggiunge il computer locale al percorso di replica di Lync Server.

    Enable-CsReplica

## Descrizione dettagliata

Quando in un computer viene installato un ruolo del server o un servizio, è necessario aggiungere il computer al percorso di replica in modo che possa ricevere i file di configurazione e della topologia dall'archivio di gestione centrale. Il cmdlet **Enable-CsReplica** consente di aggiungere manualmente un computer al percorso di replica. Di norma, non è necessario aggiungere manualmente un computer al percorso di replica. Questa operazione infatti viene eseguita automaticamente quando si installa Lync Server in un computer.

Utenti autorizzati a utilizzare questo cmdlet: il cmdlet **Enable-CsReplica** può essere utilizzato localmente da un amministratore locale che sia membro del dominio.

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
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo (FQDN) del server di catalogo globale nel dominio. Questo parametro non è obbligatorio se si esegue il cmdlet <strong>Enable-CsReplica</strong> su un computer con un account nel dominio.</p></td>
</tr>
<tr class="even">
<td><p><em>GlobalSettingsDomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>FQDN del controller di dominio dove sono archiviate le impostazioni globali. Se le impostazioni globali vengono archiviate nel contenitore di sistema in Servizi di dominio Active Directory, questo parametro deve puntare al controller di dominio radice. Se le impostazioni globali sono archiviate nel contenitore di configurazione, è possibile utilizzare qualsiasi controller di dominio e omettere questo parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\EnableReplica.html&quot;</p></td>
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

Nessuno. Il cmdlet **Enable-CsReplica** non accetta input da pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Enable-CsReplica** non restituisce oggetti o valori.

## Vedere anche

#### Ulteriori risorse

[Get-CsManagementStoreReplicationStatus](get-csmanagementstorereplicationstatus.md)

