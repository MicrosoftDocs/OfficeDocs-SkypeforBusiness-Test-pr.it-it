---
title: Start-CsWindowsService
TOCTitle: Start-CsWindowsService
ms:assetid: 7491b91f-d342-4f9a-878b-d20b35294a9c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398561(v=OCS.15)
ms:contentKeyID: 49300989
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Start-CsWindowsService

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Il cmdlet **Start-CsWindowsService** consente di avviare un servizio di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Start-CsWindowsService [-ComputerName <String>] [-Name <String>] <COMMON PARAMETERS>

    Start-CsWindowsService [-InputObject <NTService>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-NoWait <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 vengono avviati tutti i servizi di Lync Server nel computer locale. A tale scopo, viene chiamato il cmdlet **Start-CsWindowsService** senza alcun parametro. Non viene visualizzato alcun errore se si tenta di avviare un servizio che è già stato avviato.

    Start-CsWindowsService

## ESEMPIO 2

Nell'esempio 2 viene avviato il servizio applicazione Response Group nel computer locale. A tale scopo, il comando utilizza il parametro Name seguito dal nome del servizio: RTCRGS.

    Start-CsWindowsService -Name "RTCRGS"

## ESEMPIO 3

Anche con il comando mostrato nell'esempio 3 viene avviato il servizio applicazione Response Group; in questo caso, però, il servizio viene avviato sul computer remoto atl-cs-001.litwareinc.com. Per avviare un servizio su un computer remoto, è sufficiente includere il parametro ComputerName seguito dal nome di dominio completo del computer remoto.

    Start-CsWindowsService -Name "RTCRGS" -ComputerName atl-cs-001.litwareinc.com

## ESEMPIO 4

Con l'esempio 4 il comando ricerca nel computer locale tutti i servizi di Lync Server che attualmente non sono in esecuzione, quindi avvia ogni servizio inattivo. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsWindowsService** per restituire una raccolta di tutti i servizi di Lync Server. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i servizi in cui la proprietà Status non equivale a Running. Tale raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Start-CsWindowsService**, che avvia ogni servizio della raccolta.

    Get-CsWindowsService | Where-Object {$_.Status -ne "Running"} | Start-CsWindowsService

## Descrizione dettagliata

Molti componenti di Lync Server vengono eseguiti come servizi standard di Windows, ad esempio l'applicazione Operatore Conferenza è in realtà un servizio denominato RTCCAA. Se uno dei servizi di Lync Server attualmente è arrestato, è possibile riavviarlo con il cmdlet **Start-CsWindowsService**.

Si noti tuttavia che il cmdlet **Start-CsWindowsService** può avviare solo i servizi di Lync Server. Si verificherà un errore se con questo cmdlet si tenta di avviare un servizio non appartenente a Lync Server, ad esempio lo spooler di stampa.

A livello funzionale, il cmdlet **Start-CsWindowsService** è molto simile al cmdlet generico Windows PowerShell**Start-Service**. Se lo si desidera, è possibile utilizzare il cmdlet **Start-Service** per avviare un servizio di Lync Server. Il cmdlet **Start-CsWindowsService** tuttavia include un parametro ComputerName che facilita l'avvio di un servizio in un computer remoto: è sufficiente includere il parametro ComputerName seguito dal nome di dominio completo (FQDN) del computer remoto. Il cmdlet **Start-Service** non dispone di un parametro di questo tipo. Inoltre, il parametro Report del cmdlet consente di mantenere un log degli errori che possono verificarsi durante la chiamata a **Start-CsWindowsService**.

Come altri servizi Windows, alcuni servizi di Lync Server dipendono da altri servizi. Ad esempio, il servizio Operatore Conferenza di Lync Server non può essere eseguito se il Servizio applicazione non è già in esecuzione. Se si tenta di avviare un servizio che dipende da un altro servizio, il cmdlet **Start-CsWindowsService** avvierà entrambi i servizi. Se ad esempio si tenta di avviare il servizio Operatore Conferenza, il cmdlet avvierà innanzitutto il Servizio applicazione e quindi il servizio Operatore Conferenza. Tuttavia, il cmdlet **Start-CsWindowsService** non avvierà automaticamente eventuali servizi dipendenti di un servizio. Se si avvia il Servizio applicazione, il comando non avvierà automaticamente anche il servizio Operatore Conferenza.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Start-CsWindows** in locale: RTCUniversalServerAdmins. Inoltre, per eseguire questo cmdlet è necessario disporre dei diritti di amministratore locale sul computer di destinazione. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Start-CsWindowsService"}

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
<td><p>Nome del computer remoto che ospita il servizio da avviare. Se questo parametro non è incluso, il cmdlet <strong>Start-CsWindowsService</strong> avvierà nel computer locale il servizio o i servizi specificati. Per fare riferimento al computer remoto, utilizzare il relativo nome di dominio completo, ad esempio, atl-cs-001.litwareinc.com.</p></td>
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
<td><p>Consente di ignorare la visualizzazione di messaggi di errore non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InputObject</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.Core.NTService</p></td>
<td><p>Consente di avviare un servizio utilizzando un riferimento oggetto anziché un nome di servizio. Se ad esempio si utilizza il cmdlet <strong>Get-CsWindowsService</strong> per restituire informazioni su un servizio e si archivia l'oggetto restituito in una variabile denominata $x, è possibile avviare il servizio utilizzando il comando seguente:</p>
<p>$x = Get-CsWindowsService -Name &quot;RTCCPS&quot;</p>
<p>Start-CsWindowsService -InputObject $x.Name</p></td>
</tr>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome del servizio Lync Server da avviare. Si noti che si deve utilizzare il nome del servizio (ad esempio RTCCAA) e non il nome visualizzato del servizio. È possibile passare un singolo nome di servizio al parametro Name e non è consentito l'uso di caratteri jolly nel nome del servizio. I nomi dei servizi possono essere recuperati mediante il cmdlet <strong>Get-CsWindowsService</strong>.</p>
<p>Considerare che il cmdlet <strong>Start-CsWindowsService</strong> può avviare solo i servizi di Lync Server. Non può essere utilizzato per avviare altri servizi Windows. Per questi servizi è possibile utilizzare il cmdlet <strong>Start-Service</strong> di Windows PowerShell.</p></td>
</tr>
<tr class="even">
<td><p><em>NoWait</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presente, fa sì che il comando venga eseguito e restituisca immediatamente il controllo al prompt di Windows PowerShell. Se non è presente, il controllo non viene restituito fin quando il comando non è stato completato e sullo schermo non è stata scritta una relazione sullo stato.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Percorso di un file HTML in cui è possibile archiviare le informazioni sugli errori. Se viene incluso questo parametro, qualunque errore durante l'esecuzione di questo cmdlet verrà registrato nel file specificato (ad esempio, C:\Logs\Service_report.html).</p></td>
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

Oggetto Microsoft.Rtc.Management.Deployment.Core.NTService. Il cmdlet **Start-CsWindowsService** accetta istanze dell'oggetto servizio Windows inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Start-CsWindowsService** consente invece di avviare le istanze dell'oggetto Microsoft.Rtc.Management.Deployment.Core.NTService.

## Vedere anche

#### Ulteriori risorse

[Get-CsWindowsService](get-cswindowsservice.md)  
[Stop-CsWindowsService](stop-cswindowsservice.md)

