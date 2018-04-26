---
title: Test-CsTopology
TOCTitle: Test-CsTopology
ms:assetid: 06ffa245-f1c7-46b7-9be6-5b291deda5c1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398127(v=OCS.15)
ms:contentKeyID: 49299580
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsTopology

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica l'attivazione del servizio e le autorizzazioni di gruppo per l'installazione di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsTopology [-GlobalCatalog <Fqdn>] [-GlobalSettingsDomainController <Fqdn>] [-Report <String>] [-Service <String>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene convalidata l'intera topologia di Lync Server.

    Test-CsTopology

## ESEMPIO 2

Il comando riportato nell'Esempio 2 è molto simile al comando nell'Esempio 1. Tuttavia, in questo caso, viene incluso il parametro Report per specificare il percorso (C:\\Logs\\Topology.xml) in cui deve essere scritto il file di output.

    Test-CsTopology -Report "C:\Logs\Topology.html"

## ESEMPIO 3

Nell'esempio 3 viene utilizzato il cmdlet **Test-CsTopology** per convalidare un unico servizio, ovvero Registrar:atl-cs-001.litwareinc.com.

    Test-CsTopology -Service "Registrar:atl-cs-001.litwareinc.com"

## Descrizione dettagliata

Il cmdlet **Test-CsTopology** consente di verificare che Lync Server funzioni correttamente a livello globale. Per impostazione predefinita, il cmdlet controlla l'intera infrastruttura di Lync Server verificando che i servizi richiesti siano in esecuzione e che siano state configurate le autorizzazioni appropriate per tali servizi e per i gruppi di sicurezza universali creati durante l'installazione di Lync Server.

Oltre a verificare la validità di Lync Server nella sua globalità, il cmdlet **Test-CsTopology** consente anche di controllare la validità di un servizio specifico. Questo comando ad esempio verifica lo stato di A/V Conferencing Server nel pool atl-cs-001.litwareinc.com:

Test-CsTopology –Service "ConferencingServer:atl-cs-001.litwareinc.com".

Utenti autorizzati a utilizzare questo cmdlet: Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsTopology"}

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
<td><p><em>GlobalCatalog</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo (FQDN) del server di catalogo globale nel dominio. Questo parametro non è obbligatorio se si esegue il cmdlet <strong>Test-CsTopology</strong> su un computer con un account nel dominio.</p></td>
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
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\Topology.html&quot;</p></td>
</tr>
<tr class="even">
<td><p><em>Service</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Se presente, il cmdlet <strong>Test-CsTopology</strong> limita le verifiche di convalida al servizio specificato. Si noti che è possibile specificare un servizio alla volta quando si utilizza il parametro Service. I servizi devono essere specificati utilizzando l'ID appropriato. Ad esempio, la sintassi seguente fa riferimento al servizio di registrazione nel pool atl-cs-001.litwareinc.com: -Service &quot;Registrar:atl-cs-001.litwareinc.com&quot;.</p>
<p>Se questo parametro non è incluso, verrà convalidata l'intera topologia.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsTopology** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Test-CsTopology** restituisce un'istanza dell'oggetto Microsoft.Rtc.SyntheticTransactions.TaskOutput.

## Vedere anche

#### Ulteriori risorse

[Enable-CsTopology](enable-cstopology.md)  
[Get-CsTopology](get-cstopology.md)  
[Publish-CsTopology](publish-cstopology.md)

