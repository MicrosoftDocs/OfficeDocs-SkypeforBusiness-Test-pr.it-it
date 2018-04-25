---
title: Import-CsDeviceUpdate
TOCTitle: Import-CsDeviceUpdate
ms:assetid: cc2e5fab-d978-4e7e-8fc6-d12a0172c07c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398861(v=OCS.15)
ms:contentKeyID: 49301989
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Import-CsDeviceUpdate

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Importa un insieme di regole di aggiornamento dei dispositivi scaricate dal sito Web Microsoft. Le regole di aggiornamento dei dispositivi associano gli aggiornamenti della versione del firmware ai dispositivi hardware che eseguono Lync Phone Edition. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Import-CsDeviceUpdate -FileName <String> -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 importa le regole di aggiornamento dei dispositivi dal file C:\\Updates\\UCUpdates.cab.

    Import-CsDeviceUpdate -Identity "service:WebServer:atl-cs-001.litwareinc.com" -FileName C:\Updates\UCUpdates.cab

## ESEMPIO 2

Il comando riportato nell'esempio 2 importa le regole di aggiornamento dei dispositivi dal percorso UNC \\\\atl-fs-001\\Updates\\UCUpdates.cab.

    Import-CsDeviceUpdate -Identity "service:WebServer:atl-cs-001.litwareinc.com" -FileName \\atl-fs-001\Updates\UCUpdates.cab

## ESEMPIO 3

Nell'esempio 3 viene mostrato come utilizzare un solo comando per importare le regole di aggiornamento dei dispositivi in tutti i server che eseguono i servizi Web. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsService** con il parametro WebServer per restituire una raccolta di tutti i server che eseguono il servizio servizi Web. La raccolta viene quindi inviata tramite pipe al cmdlet **ForEach-Object**, che esegue un ciclo in ogni server della raccolta e utilizza il cmdlet **Import-CsDeviceUpdate** per aggiornare le regole di aggiornamento dei dispositivi più recenti in tali server. Questo comando funzionerà solo se il file UCUpdates.cab è stato copiato nello stesso percorso (C:\\Updates) in tutti i server.

    Get-CsService -WebServer | ForEach-Object {Import-CsDeviceUpdate -Identity $_.Identity -FileName C:\Updates\UCUpdates.cab}

## Descrizione dettagliata

Periodicamente, Microsoft rende disponibile un nuovo set di regole di aggiornamento dei dispositivi per Lync Phone Edition. Queste regole rappresentano aggiornamenti del firmware per dispositivi che eseguono Lync Phone Edition. Una volta importate queste regole, gli amministratori possono testare gli aggiornamenti del firmware e successivamente renderli disponibili per tutti i dispositivi pertinenti in uso nell'organizzazione in caso di esito positivo del test.

L'unico modo per creare nuove regole di aggiornamento consiste nello scaricare pacchetti di aggiornamento dal sito Microsoft. Non è infatti possibile creare regole di aggiornamento dei dispositivi personalizzate. Per ottenere il set più recente di regole di aggiornamento dei dispositivi, aprire la pagina del supporto tecnico del sito Web Microsoft e cercare "Phone Edition". Scaricare il pacchetto di aggiornamento ed estrarre i file in una cartella nel computer dove devono essere caricati gli aggiornamenti. Dopo aver estratto i file, è possibile utilizzare il cmdlet **Import-CsDeviceUpdate** per importare le regole di aggiornamento dei dispositivi presenti nel file CAB estratto, che sarà denominato UCUpdates.cab.

Come già indicato precedentemente, gli aggiornamenti possono essere caricati solo localmente. Sarà necessario pertanto copiare il file UCUpdates.cab in tutti i computer che eseguono il servizio servizi Web che devono ospitare le regole di aggiornamento dei dispositivi. Considerare inoltre che le regole di aggiornamento dei dispositivi non vengono replicate da server a server. Se si desidera che tutte le regole di aggiornamento dei dispositivi dell'organizzazione siano sempre sincronizzate, sarà necessario eseguire la stessa operazione in ogni server che ospita tali regole. Se ad esempio si rimuove una regola da un server servizi Web, sarà necessario rimuovere la stessa regola dagli altri server servizi Web. In caso contrario, le regole di aggiornamento dei dispositivi non saranno più sincronizzate.

Le regole di aggiornamento possono essere importate solo nei servizi, poiché non sono applicabili all'ambito globale, all'ambito del sito o ad ambiti specifici per gli utenti. Si noti, tuttavia, che il cmdlet **Import-CsDeviceUpdate** non aggiunge automaticamente regole e aggiornamenti a ogni servizio di un sito, ma li carica solo nel servizio specificato. Se ad esempio in un sito esistono tre server che eseguono i servizi Web, sarà necessario eseguire il cmdlet **Import-CsDeviceUpdate** tre volte, una per ogni istanza dei servizi Web. In alternativa, è possibile utilizzare un comando come quello riportato nell'esempio 3, che recupera l'identità di tutti i server servizi Web e quindi esegue il cmdlet **Import-CsDeviceUpdate** in ciascuno di tali server.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Import-CsDeviceUpdate** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Import-CsDeviceUpdate"}

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
<td><p><em>FileName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Percorso del file di aggiornamento, ad esempio C:\Updates\UCUpdates.cab.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Indica l'istanza del servizio a cui verranno applicate le nuove regole di aggiornamento. Ad esempio: -Identity &quot;service:WebServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>Il valore di Identity deve essere il nome di dominio completo del pool Front End in cui è installato il server Web.</p></td>
</tr>
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
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Import-CsDeviceUpdate** non accetta input inviato tramite pipeline.

## Tipi restituiti

Il cmdlet **Import-CsDeviceUpdate** importa le istanze della classe Microsoft.Rtc.Management.WritableConfig.Settings.DeviceUpdate.Rule.

## Vedere anche

#### Ulteriori risorse

[Get-CsDeviceUpdateRule](get-csdeviceupdaterule.md)

