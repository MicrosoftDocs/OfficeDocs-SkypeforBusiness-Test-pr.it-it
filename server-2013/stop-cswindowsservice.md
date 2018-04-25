---
title: Stop-CsWindowsService
TOCTitle: Stop-CsWindowsService
ms:assetid: 60318b9f-2291-4b99-a271-d206e4074b70
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398426(v=OCS.15)
ms:contentKeyID: 49300720
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Stop-CsWindowsService

 

_**Ultima modifica dell'argomento:** 2015-03-09_

**Stop-CsWindowsService** consente di arrestare un servizio di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Stop-CsWindowsService [-ComputerName <String>] [-Name <String>] <COMMON PARAMETERS>

    Stop-CsWindowsService [-InputObject <NTService>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Graceful <SwitchParameter>] [-LeaveClsAgentRunning <SwitchParameter>] [-LeaveWebServerRunning <SwitchParameter>] [-NoWait <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 viene arrestato il servizio applicazione Response Group sul computer locale. Il servizio applicazione Response Group viene identificato includendo il parametro Name e il nome del servizio, RTCRGS.

    Stop-CsWindowsService -Name "RTCRGS"

## ESEMPIO 2

Anche con l'esempio 2 viene arrestato il servizio applicazione Response Group; in questo esempio, però, il servizio si trova sul computer remoto atl-cs-001.litwareinc.com. Per arrestare un servizio su un computer remoto, è sufficiente includere il parametro ComputerName seguito dal nome di dominio completo del computer remoto.

    Stop-CsWindowsService -Name "RTCRGS" -ComputerName atl-cs-001.litwareinc.com

## ESEMPIO 3

Con l'esempio 3 viene dimostrato come arrestare un servizio anche se non se ne conosce il nome (in questo esempio RTCCPS). A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsWindowsService** senza alcun parametro per restituire una raccolta di tutti i servizi Lync Server nel computer locale. La raccolta completa viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i servizi la cui proprietà DisplayName include il valore stringa "Call Park". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Stop-CsWindowsService**, che arresta il servizio applicazione Parcheggio di chiamata.

    Get-CsWindowsService | Where-Object {$_.DisplayName -like "*Call Park*"} | Stop-CsWindowsService

## Descrizione dettagliata

Molti componenti di Lync Server vengono eseguiti come servizi standard di Windows, ad esempio il componente applicazione Operatore Conferenza è in realtà un servizio denominato RTCCAA. Per arrestare un servizio di Lync Server, è possibile utilizzare il cmdlet **Stop-CsWindowsService**.

Considerare che il cmdlet **Stop-CsWindowsService** può arrestare solo i servizi di Lync Server. Si verificherà un errore se si tenta di arrestare un servizio non appartenente a Lync Server, ad esempio lo spooler di stampa, utilizzando questo cmdlet.

A livello funzionale, il cmdlet **Stop-CsWindowsService** è molto simile al cmdlet generico di Windows PowerShell**Stop-Service**. Se lo si desidera, è possibile utilizzare il cmdlet **Stop-Service** per arrestare un servizio di Lync Server. Il cmdlet **Stop-CsWindowsService** tuttavia include un parametro ComputerName che facilita l'arresto di un servizio in un computer remoto. È sufficiente includere il parametro ComputerName seguito dal nome di dominio completo del computer remoto. Il cmdlet **Stop-Service** non dispone di un parametro di questo tipo. Inoltre, il cmdlet **Stop-CsWindowsService** dispone di un parametro Report che consente di mantenere un log degli errori che possono verificarsi durante la chiamata al cmdlet.

Il cmdlet **Stop-CsWindowsService** arresta qualsiasi servizio per cui viene richiesto l'arresto. Sono inclusi i servizi con servizi dipendenti, ovvero servizi che possono essere eseguiti solo se il servizio che si sta tentando di arrestare è in esecuzione. Per impostazione predefinita, se si tenta di arrestare un servizio con servizi dipendenti, il cmdlet **Stop-CsWindowsService** non arresta solo il servizio in questione, ma anche tutti i servizi dipendenti. Dal momento che potrebbero verificarsi conseguenze impreviste, è possibile includere il parametro Graceful nella chiamata al cmdlet **Stop-CsWindowsService**. Con l'inclusione del parametro Graceful, il cmdlet **Stop-CsWindowsService** impedirà al servizio di accettare nuove richieste. Tutte le richieste esistenti per il servizio restano invariate, mentre tutte le nuove richieste vengono rifiutate Al completamento delle richieste esistenti, queste non saranno sostituite. Alla fine, tutte le richieste esistenti saranno soddisfatte e il servizio verrà arrestato.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Stop-CsWindowsService** in locale: RTCUniversalServerAdmins. Inoltre, per eseguire questo cmdlet è necessario disporre dei diritti di amministratore locale sul computer di destinazione. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Stop-CsWindowsService"}

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
<td><p>Nome del computer remoto in cui è in esecuzione il servizio da arrestare. Se questo parametro non è incluso, il cmdlet <strong>Stop-CsWindowsService</strong> arresterà il servizio specificato nel computer locale. È necessario fare riferimento al computer remoto utilizzando il relativo nome di dominio completo, ad esempio atl-mcs-001.litwareinc.com.</p></td>
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
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Graceful</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Invece di arrestare immediatamente un servizio, consente di attendere che tutte le richieste esistenti del servizio siano soddisfatte. Le nuove richieste al servizio saranno invece rifiutate. Il servizio non viene completamente arrestato finché non sono state soddisfatte tutte le richieste esistenti.</p></td>
</tr>
<tr class="odd">
<td><p><em>InputObject</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deployment.Core.NTService</p></td>
<td><p>Consente di arrestare un servizio utilizzando un riferimento oggetto anziché un nome di servizio. Se ad esempio si utilizza il cmdlet <strong>Get-CsWindowsService</strong> per restituire informazioni su un servizio e si archivia l'oggetto restituito in una variabile denominata $x, è possibile arrestare il servizio utilizzando il comando seguente:</p>
<p>$x = Get-CsWindowsService –Name &quot;RTCCPS&quot;</p>
<p>Stop-CsWindowsService -InputObject $x.Name</p></td>
</tr>
<tr class="even">
<td><p><em>LeaveClsAgentRunning</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se specificato, arresta tutti i servizi Lync Server tranne il servizio Agente di registrazione centralizzato.</p></td>
</tr>
<tr class="odd">
<td><p><em>LeaveWebServerRunning</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se specificato, questo parametro arresta tutti i servizi nel computer specificato, eccetto il servizio Server Web.</p></td>
</tr>
<tr class="even">
<td><p><em>Name</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome del servizio Lync Server da arrestare. Si noti che si deve utilizzare il nome del servizio (ad esempio RTCCAA) e non il nome visualizzato del servizio. È possibile passare un singolo nome di servizio al parametro Name e non è consentito l'uso di caratteri jolly nel nome del servizio. È possibile utilizzare il cmdlet <strong>Get-CsWindowsService</strong> per recuperare i nomi dei servizi.</p>
<p>Considerare che il cmdlet <strong>Stop-CsWindowsService</strong> può arrestare solo i servizi di Lync Server. Non può essere utilizzato per arrestare altri servizi Windows. Per questi servizi è possibile utilizzare il cmdlet <strong>Stop-Service</strong> di Windows PowerShell.</p></td>
</tr>
<tr class="odd">
<td><p><em>NoWait</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Se presente, fa sì che il comando venga eseguito e restituisca immediatamente il controllo al prompt di Windows PowerShell. Se non è presente, il controllo non viene restituito fin quando il comando non è stato completato e sullo schermo non è stata scritta una relazione sullo stato.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Percorso di un file HTML in cui è possibile scrivere le informazioni sugli errori. Se viene incluso questo parametro, qualunque errore durante l'esecuzione di questo cmdlet verrà registrato nel file specificato (ad esempio, C:\Logs\Service_report.html).</p></td>
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

Oggetto Microsoft.Rtc.Management.Deployment.Core.NTService. Il cmdlet **Stop-CsWindowsService** accetta istanze dell'oggetto servizio Windows inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Stop-CsWindowsService** invece arresta le istanze dell'oggetto Microsoft.Rtc.Management.Deployment.Core.NTService.

## Vedere anche

#### Ulteriori risorse

[Get-CsWindowsService](get-cswindowsservice.md)  
[Start-CsWindowsService](start-cswindowsservice.md)

