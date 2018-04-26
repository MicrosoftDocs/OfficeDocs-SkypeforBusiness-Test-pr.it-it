---
title: Remove-CsManagementConnection
TOCTitle: Remove-CsManagementConnection
ms:assetid: 2fe69a3d-0154-418f-b6ee-99a88e5a9c7d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425803(v=OCS.15)
ms:contentKeyID: 49300080
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsManagementConnection

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Reimposta la connessione di gestione del punto di controllo del servizio Active Directory per l'archivio di gestione centrale. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsManagementConnection [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 rimuove le informazioni sulla connessione di gestione esistente e le sostituisce con le informazioni sulla connessione predefinita memorizzate in Active Directory.

    Remove-CsManagementConnection

## Descrizione dettagliata

I dati di configurazione di Lync Server sono archiviati nell'archivio di gestione centrale. È fondamentale che sia Windows PowerShell che i servizi di replica di gestione siano in grado di individuare questo database. Quando si installa Lync Server, in Servizi di dominio Active Directory viene creato un punto di controllo del servizio che fornisce informazioni sul percorso di questo database. I computer in genere utilizzano il punto di controllo del servizio per connettersi all'archivio di gestione centrale. Per visualizzare i dettagli di questa connessione, ovvero conoscere il computer in cui è in esecuzione l'archivio di gestione centrale e ottenere informazioni sulla connessione SQL Server all'archivio di gestione centrale, è possibile eseguire il cmdlet **Get-CsManagementConnection**.

Di norma, non è necessario cambiare la connessione di gestione. Può tuttavia accadere di dover temporaneamente utilizzare una nuova connessione di gestione. Quando si è pronti a ritornare alla connessione predefinita, è sufficiente eseguire il cmdlet **Remove-CsManagementConnection**. Questo cmdlet infatti elimina le informazioni di connessione correnti e le sostituisce con quelle archiviate nel punto di controllo del servizio Active Directory. Ciò significa che non è necessario ricreare le informazioni sulla connessione originale perché questa operazione viene eseguita direttamente dal cmdlet **Remove-CsManagementConnection**.

Si noti che non si verificherà alcun problema se si esegue questo cmdlet mentre si utilizza la connessione predefinita. In questo caso, si continua semplicemente a utilizzare la connessione predefinita memorizzata in Active Directory. Si noti, altresì, che questo cmdlet agisce esclusivamente sulle informazione della connessione di gestione relative alla sessione Windows PowerShell corrente: tutte le modifiche apportate alla connessione di gestione valgono solo per il computer locale e per l'istanza locale di Windows PowerShell.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Remove-CsManagementConnection** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsManagementConnection"}

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
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Remove-CsManagementConnection** non accetta input da pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsManagementConnection** invece elimina le istanze dell'oggetto Microsoft.Rtc.Management.Xds.ManagementConnection.

## Vedere anche

#### Ulteriori risorse

[Get-CsManagementConnection](get-csmanagementconnection.md)  
[Remove-CsConfigurationStoreLocation](remove-csconfigurationstorelocation.md)  
[Set-CsManagementConnection](set-csmanagementconnection.md)

