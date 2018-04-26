---
title: Get-CsAnnouncement
TOCTitle: Get-CsAnnouncement
ms:assetid: d692b377-8df2-4668-b9d3-06458dd4d96d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398937(v=OCS.15)
ms:contentKeyID: 49302129
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAnnouncement

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sugli annunci di Lync Server configurati per l'utilizzo nell'organizzazione. Gli annunci vengono riprodotti quando gli utenti compongono un numero di telefono valido, ma non assegnato. Un annuncio può corrispondere a un messaggio (ad esempio "Il numero è temporaneamente fuori servizio") o a un segnale di occupato. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsAnnouncement [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsAnnouncement [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono restituiti tutti gli annunci configurati per l'utilizzo nell'organizzazione. A tale scopo, viene chiamato il cmdlet **Get-CsAnnouncement** senza alcun parametro.

    Get-CsAnnouncement

## ESEMPIO 2

Il comando riportato nell'esempio 2 restituisce un singolo annuncio: l'annuncio con l'identità ApplicationServer:redmond.litwareinc.com/1951f734-c80f-4fb2-965d-51807c792b90. Per un metodo alternativo (e probabilmente più semplice) per recuperare un annuncio specifico, vedere l'esempio 5.

    Get-CsAnnouncement -Identity "ApplicationServer:redmond.litwareinc.com/1951f734-c80f-4fb2-965d-51807c792b90" 

## ESEMPIO 3

Il comando utilizzato nell'esempio 3 restituisce informazioni su tutti gli annunci configurati per l'utilizzo nel servizio ApplicationServer:redmond.litwareinc.com.

    Get-CsAnnouncement -Identity "ApplicationServer:redmond.litwareinc.com"

## ESEMPIO 4

Nell'esempio 4 vengono restituite informazioni per tutti gli annunci configurati per l'utilizzo nel sito Redmond (per tutti i domini). A tale scopo, è necessario includere il parametro Filter e il valore di filtro "\*ApplicationServer:Redmond\*" in modo da limitare i dati restituiti agli annunci il cui valore Identity contiene il valore stringa "ApplicationServer:Redmond". Per definizione, tali annunci sono quelli configurati per l'uso nel sito Redmond.

    Get-CsAnnouncement -Filter "*ApplicationServer:Redmond*"

## ESEMPIO 5

Nell'esempio 5 viene mostrato un metodo alternativo per restituire un annuncio specifico o un insieme di annunci, in questo caso tutti gli annunci denominati Welcome Announcement. A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsAnnouncement** senza alcun parametro per restituire una raccolta di tutti gli annunci in uso nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona gli annunci con nome uguale a (-eq) "Welcome Announcement".

    Get-CsAnnouncement | Where-Object {$_.Name -eq "Welcome Announcement"}

## ESEMPIO 6

In questo esempio, che è simile a quello precedente, viene mostrato un altro metodo per restituire un singolo annuncio. Viene di nuovo chiamato il cmdlet **Get-CsAnnouncement**, ma questa volta specificando il valore Identity ApplicationServer:redmond.litwareinc.com. In tal modo, verrà restituita una raccolta di tutti gli annunci associati al servizio. Come nell'esempio 5, questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona gli annunci con nome uguale a (-eq) "Welcome Announcement". Poiché in un Servizio applicazione i nomi degli annunci devono essere univoci, questo comando non restituirà mai più di un singolo elemento.

    Get-CsAnnouncement -Identity "ApplicationServer:redmond.litwareinc.com" | Where-Object {$_.Name -eq "Welcome Announcement"}

## ESEMPIO 7

Questo esempio è simile all'esempio 5, in quanto vengono recuperati tutti gli annunci e successivamente la relativa raccolta viene inviata tramite pipe al cmdlet **Where-Object**. Tuttavia, nell'esempio 5 è stato utilizzato l'operatore –eq nella clausola where per trovare una corrispondenza esatta per il nome. In questo esempio sono stati utilizzati l'operatore –like e un valore con carattere jolly per trovare tutti gli annunci che, in questo caso, iniziano con la stringa Welcome.

    Get-CsAnnouncement | Where-Object {$_.Name -like "Welcome*"}

## ESEMPIO 8

Nell'esempio 8 vengono restituite le informazioni relative a tutti gli annunci per i quali viene utilizzato un prompt di sintesi vocale (come annuncio principale o come fallback su un file audio), ma non l'inglese americano come lingua. Per eseguire questa attività, il comando chiama innanzitutto il cmdlet **Get-CsAnnouncement** per restituire una raccolta di tutti gli annunci attualmente configurati. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona tutti gli annunci in cui la proprietà TextToSpeechPrompt non è vuota (non è uguale a $Null) e in cui la proprietà Language non è uguale a (-ne) en-US.

    Get-CsAnnouncement | Where-Object {($_.TextToSpeechPrompt -ne $Null) -and ($_.Language -ne "en-US")}

## Descrizione dettagliata

Un'organizzazione può disporre di numeri telefonici non assegnati a utenti o telefoni, ma che sono comunque numeri validi per le chiamate. Per impostazione predefinita, quando un utente compone uno di questi numeri, riceve un segnale di occupato e la chiamata può generare un errore restituito al client SIP. Applicando le impostazioni di annuncio ai numeri non assegnati, gli amministratori possono decidere di riprodurre un messaggio, restituire un segnale di occupato o reindirizzare la chiamata. Questo cmdlet recupera una o più di queste impostazioni per annunci.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsAnnouncement** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAnnouncement"}

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Questo parametro consente di eseguire una ricerca mediante caratteri jolly nell'identità di tutti gli annunci configurati per l'organizzazione. Utilizzare il carattere jolly (*) per applicare un filtro per qualsiasi parte del valore Identity.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Un identificatore per l'annuncio che si desidera recuperare. Se si omettono questo parametro e il parametro Filter, verranno visualizzate tutte le istanze di annunci configurate per l'organizzazione. Il valore per il parametro Identity può essere fornito in uno dei seguenti modi:</p>
<p>- Immettere l'identità del Servizio applicazione per gli annunci che si desidera recuperare. In tal modo, verranno recuperati tutti gli annunci configurati che presentano l'identità del servizio fornita. Ad esempio, ApplicationServer:Redmond.litwareinc.com.</p>
<p>- Immettere l'identità completa del singolo annuncio che si desidera recuperare. Questo valore sarà sempre nel formato &lt;IDservizio&gt;/&lt;GUID&gt;, dove IDservizio è l'identità del server applicazioni nel quale è in esecuzione il Servizio annunci, mentre GUID è un identificatore univoco globale associato a questo annuncio. Ad esempio: ApplicationServer:Redmond.litwareinc.com/bef5fa3b-3c97-4af0-abe7-611deee7616c.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera le informazioni relative agli annunci dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Restituisce una o più istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.AnnouncementServiceSettings.Announcement.

## Vedere anche

#### Ulteriori risorse

[New-CsAnnouncement](new-csannouncement.md)  
[Remove-CsAnnouncement](remove-csannouncement.md)  
[Set-CsAnnouncement](set-csannouncement.md)  
[Import-CsAnnouncementFile](import-csannouncementfile.md)

