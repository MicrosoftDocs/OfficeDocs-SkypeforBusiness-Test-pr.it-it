---
title: Invoke-CsStorageServiceFlush
TOCTitle: Invoke-CsStorageServiceFlush
ms:assetid: 3f88a70d-79b0-4614-8604-660bac35a86f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619175(v=OCS.15)
ms:contentKeyID: 49300313
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Invoke-CsStorageServiceFlush

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Scarica il database del servizio di archiviazione di Lync Server in ogni Front End Server di un pool. Lo scaricamento di un database implica la scrittura sul disco di tutti i dati in coda e quindi la cancellazione della coda del database. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    Invoke-CsStorageServiceFlush -FlushType <FullFlush | SteadyStateFlush> -PoolFqdn <Fqdn> [-Binding <String>] [-Force <SwitchParameter>] [-HostNameStorageService <String>] [-WaitTime <TimeSpan>]

## Esempi

## Esempio 1

Il comando riportato nell'esempio 1 esegue uno scaricamento "in stato stazionario" dei database del servizio di archiviazione presenti nel pool atl-cs-011.litwareinc.com. In uno scaricamento di questo tipo, i soli dati rimossi dalla coda (e scritti sul disco) sono quelli rimovibili senza influenzare il funzionamento del database.

    Invoke-CsStorageServiceFlush -PoolFqdn "atl-cs-001.litwareinc.com" -FlushType "SteadyState"

## Descrizione dettagliata

Il servizio di archiviazione di Lync Server offre un'interfaccia e un'infrastruttura comuni per la gestione dei dati di Lync Server, inclusi i dati di sessione, per la cronologia di monitoraggio, archiviazione e conversazione, oltre che per l'integrazione con il sistema di memorizzazione di Microsoft Exchange Server 2013. Come altri database, il servizio di archiviazione memorizza i dati in memoria e quindi, quando le risorse di sistema lo consentono, li scrive periodicamente sul disco.

Come regola generale, gli amministratori non devono interagire con questi dati in coda. Talvolta la coda può però diventare troppo grande, ad esempio a causa del failover del pool di registrazione associato al database. In questo caso è possibile chiamare il cmdlet **Invoke-CsStorageServiceFlush** per scrivere su disco tutti i dati in coda e quindi cancellare la cache del database.

Il cmdlet **Invoke-CsStorageServiceFlush** è utile anche quando è necessario arrestare contemporaneamente più Front End Server, ad esempio per eseguire un aggiornamento software. Di norma, i Front End Server di un pool devono essere arrestati e riavviati singolarmente per evitare la perdita di dati che può verificarsi a causa del ribilanciamento del gruppo di routing. In alcuni casi, tuttavia, potrebbe essere necessario arrestare più server contemporaneamente. Per evitare perdite di dati, è possibile eseguire il cmdlet **Invoke-CsStorageServiceFlush** prima di arrestare i computer. In questo modo verrà scaricata la coda per il pool e tutti questi dati verranno scritti su disco prima che i server vengano effettivamente arrestati.

Per restituire un elenco di tutti i ruoli di controllo di accesso basato sui ruoli (RBAC) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC creati personalmente), al prompt dell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Invoke-CsStorageServiceFlush"}

**Pannello di controllo di Lync Server:** le funzioni eseguite dal cmdlet **Invoke-CsStorageServiceFlush** non sono disponibili nel Pannello di controllo di Lync Server.

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
<td><p><em>FlushType</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Hadr.FlushType</p></td>
<td><p>Specifica il tipo di scaricamento di archiviazione da eseguire. I valori consentiti sono:</p>
<p>* SteadyState – i soli dati scaricati sono quelli che possono essere rimossi dalla coda senza influenzare il normale funzionamento del servizio di archiviazione. Questa operazione viene in genere eseguita per rimuovere dati precedenti dalla coda.</p>
<p>* FullFlush – consente di scaricare tutti i dati dalla coda. Questa operazione viene in genere utilizzata in caso di failover di un pool e quando non si prevede che la coda riceva nuovi dati.</p></td>
</tr>
<tr class="even">
<td><p><em>PoolFqdn</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo del pool contenente il servizio di archiviazione da scaricare.</p></td>
</tr>
<tr class="odd">
<td><p><em>Binding</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Binding WFC (Windows Communication Foundation). Un binding WCF determina i dettagli sul trasporto, la codifica e il protocollo necessari per la comunicazione tra client e servizi. I valori validi sono:</p>
<p>* NetNamedPipe</p>
<p>* NetTCP</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>HostNameStorageService</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio completo del server in cui è in esecuzione il servizio di archiviazione di Lync Server. Questo parametro è obbligatorio se il binding è impostato su NetTCP.</p></td>
</tr>
<tr class="even">
<td><p><em>WaitTime</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Specifica l'intervallo di tempo massimo che il cmdlet attende prima di stabilire che lo scaricamento è iniziato e andare al passaggio successivo del processo.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Invoke-CsStorageServiceFlush** non accetta dati da pipeline.

## Tipi restituiti

Valore stringa.

## Vedere anche

#### Ulteriori risorse

[Invoke-CsPoolFailOver](invoke-cspoolfailover.md)

