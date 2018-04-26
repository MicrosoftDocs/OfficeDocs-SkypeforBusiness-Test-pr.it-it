---
title: Get-CsManagementConnection
TOCTitle: Get-CsManagementConnection
ms:assetid: b0e2377c-6aab-45d8-b71d-0d37c6f6dae3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412849(v=OCS.15)
ms:contentKeyID: 49301689
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsManagementConnection

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulla connessione di gestione all'archivio di gestione centrale. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsManagementConnection

## Esempi

## ESEMPIO 1

Il comando nell'esempio 1 restituisce informazioni sulla connessione alla gestione all'archivio di gestione centrale.

    Get-CsManagementConnection

## Descrizione dettagliata

I dati di configurazione di Lync Server sono archiviati nell'archivio di gestione centrale. È di fondamentale importanza che sia Windows PowerShell che i servizi di replica di gestione siano in grado di individuare questo database. Quando si installa Lync Server, in Servizi di dominio Active Directory viene creato un punto di controllo del servizio che fornisce informazioni sulla posizione di tale database. I computer in genere utilizzano questo punto di controllo del servizio per connettersi all'archivio di gestione centrale. Per visualizzare i dettagli di base della connessione, ad esempio il computer in cui è in esecuzione l'archivio di gestione centrale e le informazioni sulla connessione di SQL Server a tale archivio di gestione centrale, è possibile eseguire il cmdlet **Get-CsManagementConnection**.

Se è stato utilizzato il cmdlet **Set-CsManagementConnection** per configurare una connessione temporanea di gestione per l'istanza corrente di Windows PowerShell, ad esempio per poter utilizzare la replica locale, il cmdlet **Get-CsManagementConnection** restituirà le informazioni relative a tale connessione temporanea. Al contrario, il cmdlet **Get-CsConfigurationStoreLocation** restituisce sempre informazioni sul punto di controllo del servizio in Active Directory, indipendentemente dalla connessione di gestione locale utilizzata come riferimento.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsManagementConnection** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsManagementConnection"}

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
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Questo cmdlet fornisce unicamente parametri comuni di Windows PowerShell.</p></td>
<td> </td>
<td> </td>
<td> </td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsManagementConnection** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsManagementConnection** restituisce istanze dell'oggetto Microsoft.Rtc.Management.Xds.ManagementConnection.

## Vedere anche

#### Ulteriori risorse

[Remove-CsManagementConnection](remove-csmanagementconnection.md)  
[Set-CsManagementConnection](set-csmanagementconnection.md)

