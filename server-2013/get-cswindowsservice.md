---
title: Get-CsWindowsService
TOCTitle: Get-CsWindowsService
ms:assetid: 9b119dac-c3e6-4031-8ae4-972fca1ef728
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398803(v=OCS.15)
ms:contentKeyID: 49301433
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsWindowsService

 

_**Ultima modifica dell'argomento:** 2015-03-09_

**Get-CsWindowsService** restituisce informazioni dettagliate sui componenti di Lync Server che vengono eseguiti come servizi di Windows. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsWindowsService [-ComputerName <String>] [-ExcludeActivityLevel <SwitchParameter>] [-Name <String>] [-Report <String>]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 restituisce informazioni relative a tutti i servizi di Lync Server installati nel computer locale. A tale scopo, viene utilizzato il cmdlet **Get-CsWindowsService** senza alcun parametro.

    Get-CsWindowsService

## ESEMPIO 2

Nell'esempio 2 vengono restituite informazioni relative a servizi di Lync Server presenti nel computer locale, tuttavia in questo caso i dati vengono visualizzati in formato elenco. In questo modo è possibile visualizzare i valori di tutte le proprietà di ogni servizio. Nella visualizzazione predefinita tabulare viene visualizzato solo un subset di valori delle proprietà. A tale scopo, viene chiamato innanzitutto il cmdlet **Get-CsWindowsService** e quindi le informazioni risultanti vengono inviate tramite pipe al cmdlet **Format-List**.

    Get-CsWindowsService | Format-List

## ESEMPIO 3

Con l'esempio 3 vengono restituite le informazioni per un singolo servizio di Lync Server: il servizio denominato RTCSrv.

    Get-CsWindowsService -Name "RTCSrv"

## ESEMPIO 4

Nell'esempio 4 vengono visualizzate informazioni dettagliate per tutti i ruoli di servizio gestiti dal servizio RTCSrv. A tale scopo, viene utilizzato innanzitutto il cmdlet **Get-CsWindowsService** per recuperare informazioni relative al servizio RTCSrv. Queste informazioni vengono quindi inviate tramite pipe al cmdlet **Select-Object**, che utilizza il parametro ExpandProperty per visualizzare tutti i ruoli gestiti dal servizio RTCSrv. Si noti che questo comando restituisce un messaggio di errore se un servizio non dispone di un nome di ruolo.

    Get-CsWindowsService -Name "RTCSrv" | Select-Object -ExpandProperty RoleName

## ESEMPIO 5

Il comando riportato nell'Esempio 5 restituisce informazioni relative ai servizi di Lync Server sul computer remoto atl-cs-001.litwareinc.com. Per ottenere questo risultato, viene incluso il parametro -ComputerName seguito dal nome completo di dominio (FQDN) del computer remoto.

    Get-CsWindowsService -Computer atl-cs-001.litwareinc.com

## ESEMPIO 6

Nell'esempio 6 vengono restituite informazioni relative a tutti i servizi di Lync Server installati nel computer locale. Viene inoltre incluso il parametro Report per salvare le informazioni sugli errori in un file denominato C:\\Logs\\Services.html. Se il cmdlet **Get-CsWindowsService** rileva un problema qualsiasi durante il recupero dei dati sui servizi, le informazioni relative al problema verranno registrate nel file Services.html.

    Get-CsWindowsService -Report C:\Logs\Services.html

## ESEMPIO 7

Nell'esempio 7 le informazioni vengono restituite solo per i servizi di Lync Server attualmente in esecuzione nel computer locale. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsWindowsService** per restituire una raccolta di tutti i servizi di Lync Server, indipendentemente dal fatto che siano o meno in esecuzione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà Status è uguale a Running.

    Get-CsWindowsService | Where-Object {$_.Status -eq "Running"}

## ESEMPIO 8

Nell'esempio 8 viene illustrato come recuperare informazioni relative a un particolare servizio, anche se non si conosce il nome effettivo del servizio (in questo caso RTCASMCU). A tale scopo, viene chiamato innanzitutto il cmdlet **Get-CsWindowsService** senza alcun parametro in modo da restituire una raccolta di tutti i servizi di Lync Server presenti nel computer locale. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo il servizio in cui la proprietà DisplayName include (-like) il valore stringa "Application Sharing". Come risultato finale vengono visualizzate le informazioni per il servizio conferenze di Condivisione applicazioni di Lync Server.

    Get-CsWindowsService | Where-Object {$_.DisplayName -like "*Application Sharing*"}

## ESEMPIO 9

Nell'esempio 9 vengono restituite informazioni relative ai servizi che ospitano il ruolo ApplicationServer. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsWindowsService** per restituire una raccolta di tutti i servizi di Lync Server presenti nel computer locale. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona i servizi in cui la proprietà RoleName include (-contains) il ruolo ApplicationServer.

    Get-CsWindowsService | Where-Object {$_.RoleName -contains "ApplicationServer"}

## Descrizione dettagliata

Molti componenti di Lync Server vengono eseguiti come servizi di Windows standard, ad esempio l'applicazione Operatore Conferenza di Lync Server è in realtà un servizio denominato RTCCAA. Il cmdlet **Get-CsWindowsService** consente di recuperare informazioni dettagliate esclusivamente su questi servizi di Lync Server. Questo perché il cmdlet è stato progettato per ignorare qualsiasi servizio che non faccia parte di Lync Server.

Il fatto che il cmdlet **Get-CsWindowsService** escluda automaticamente i servizi non Lync Server è un vantaggio che questo cmdlet offre rispetto al generico cmdlet **Get-Service** distribuito come parte di Windows PowerShell. Esiste inoltre un'altra importante ragione per utilizzare il cmdlet **Get-CsWindowsService** quando è necessario recuperare informazioni sui servizi di Lync Server: il cmdlet **Get-CsWindowsService** restituisce dati utili che non vengono restituiti dal cmdlet **Get-Service**. Ad esempio, nelle informazioni relative al servizio Operatore Conferenza di Lync Server, il cmdlet **Get-CsWindowsService** riporta il numero di chiamate simultanee gestite dal servizio (il livello di attività del servizio), contrariamente al cmdlet **Get-Service**.

Per impostazione predefinita, il cmdlet **Get-CsWindowsService** viene eseguito per il computer locale. Includendo il parametro ComputerName è possibile tuttavia ottenere informazioni relative ai servizi di Lync Server in esecuzione in un computer remoto.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsWindowsService** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Inoltre, per eseguire questo cmdlet è necessario essere membri del gruppo Performance Monitor Users sul computer di destinazione. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsWindowsService"}

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
<td><p><em>ComputerName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome del computer remoto dal quale recuperare le informazioni relative ai servizi. Se questo parametro non viene incluso, il cmdlet <strong>Get-CsWindowsService</strong> restituirà informazioni relative ai servizi di Lync Server in esecuzione nel computer locale. Per fare riferimento al computer remoto, è necessario utilizzare il relativo nome completo di dominio (FQDN), ad esempio atl-mcs-001.litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p><em>ExcludeActivityLevel</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se viene incluso questo parametro, il cmdlet <strong>Get-CsWindowsService</strong> restituisce solo lo stato del servizio e non il livello di attività del servizio.</p></td>
</tr>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome del servizio del quale si cercano informazioni. Si noti che è necessario utilizzare il nome del servizio (ad esempio, RTCCAA) e non il nome visualizzato del servizio. Al parametro Name è possibile fornire un solo nome di servizio, inoltre nel nome del servizio non sono ammessi caratteri jolly.</p>
<p>Si noti inoltre che il cmdlet <strong>Get-CsWindowsService</strong> può restituire informazioni solo per i servizi di Lync Server. Non è possibile utilizzare questo cmdlet per ottenere informazioni su altri servizi Windows. Per tali servizi, è necessario utilizzare il cmdlet <strong>Get-Service</strong> di Windows PowerShell.</p>
<p>Se non si include questo parametro, il cmdlet <strong>Get-CsWindowsService</strong> restituirà informazioni su tutti i servizi di Lync Server.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Percorso per un file HTML dove possono essere memorizzate le informazioni relative agli errori. Se viene incluso questo parametro, qualunque errore durante l'esecuzione di questo cmdlet verrà registrato nel file specificato (ad esempio, C:\Logs\Service_report.html).</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsWindowsService** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsWindowsService** restituisce istanze dell'oggetto Microsoft.Rtc.Management.Deployment.Core.NTService.

## Vedere anche

#### Ulteriori risorse

[Start-CsWindowsService](start-cswindowsservice.md)  
[Stop-CsWindowsService](stop-cswindowsservice.md)

