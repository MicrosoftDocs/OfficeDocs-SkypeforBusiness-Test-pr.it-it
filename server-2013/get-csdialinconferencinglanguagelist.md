---
title: Get-CsDialInConferencingLanguageList
TOCTitle: Get-CsDialInConferencingLanguageList
ms:assetid: 39355144-c8de-4ad3-9568-6426d3b97ccb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425869(v=OCS.15)
ms:contentKeyID: 49300239
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsDialInConferencingLanguageList

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce un elenco di lingue, incluse lingue regionali e di minoranze, supportate per l'utilizzo nelle conferenze telefoniche con accesso esterno di Lync Server. Queste lingue vengono utilizzate per trasmettere messaggi e istruzioni audio agli utenti che partecipano a una conferenza tramite telefono. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsDialInConferencingLanguageList [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsDialInConferencingLanguageList [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene illustrato come interrogare il cmdlet **Get-CsDialInConferencingLanguageList** per verificare se nell'elenco delle lingue supportate sia presente una lingua specifica. In questo esempio viene chiamato il cmdlet **Get-CsDialInConferencingLanguageList** per restituire le informazioni su tutte le lingue supportate. Viene quindi utilizzato l'operatore -contains di Windows PowerShell per verificare se nell'elenco delle lingue supportate sia incluso il codice della lingua "en-US". In caso affermativo, il cmdlet **Get-CsDialInConferencingLanguageList** restituirà il valore "True". Se invece nell'elenco delle lingue supportate non è presente il codice "en-US", il cmdlet restituirà il valore "False".

    (Get-CsDialInConferencingLanguageList).Languages -contains "en-US"

## ESEMPIO 2

Il comando riportato nell'esempio 2 restituisce l'elenco completo delle lingue supportate. L'oggetto DialInConferencingLanguageList archivia queste informazioni nella proprietà Languages. Per visualizzare ogni lingua, il comando utilizza innanzitutto il cmdlet **Get-CsDialInConferencingLanguageList** per restituire una raccolta di tutti gli elenchi delle lingue e le relative proprietà. La chiamata al cmdlet **Get-CsDialInConferencingLanguageList** è racchiusa tra parentesi affinché Windows PowerShell esegua questa operazione prima delle altre. Dopo che sono state restituite queste informazioni, viene utilizzata la "notazione del punto" standard (nome dell'oggetto seguito da un punto, seguito a sua volta dal nome di una proprietà) per visualizzare tutti i valori archiviati nella proprietà Languages.

    (Get-CsDialInConferencingLanguageList).Languages

## Descrizione dettagliata

Lync Server consente agli utenti di partecipare alle conferenze tramite il telefono. Questi utenti con accesso esterno non possono visualizzare video o scambiare messaggi istantanei, ma possono comunque partecipare attivamente alla parte audio della riunione. Quando gli utenti si connettono a una conferenza tramite telefono, ascoltano innanzitutto un messaggio di benvenuto e quindi ricevono le istruzioni per partecipare alla riunione. In base alla configurazione della conferenza, è ad esempio possibile che venga richiesto di pronunciare il proprio nome e quindi di premere il tasto cancelletto (\#). È possibile che in momenti diversi Lync Server riproduca ulteriori messaggi o istruzioni. Se ad esempio un utente preme 1 sulla tastiera del telefono, il sistema riprodurrà un elenco di tutte le altre opzioni di tastiera disponibili.

Gli amministratori possono configurare la lingua o le lingue utilizzate in una conferenza telefonica con accesso esterno per trasmettere messaggi e istruzioni. Il cmdlet **Get-CsDialInConferencingLanguageList** restituisce un elenco delle lingue supportate. L'elenco viene restituito utilizzando codici lingua composti da 5 caratteri, ad esempio, ca-ES per il catalano.

L'elenco delle lingue supportate è un elenco di sola lettura. Non c'è modo di aggiungere nuove lingue all'elenco; per questa ragione non è possibile aggiungere nuove lingue supportate per la conferenza telefonica con accesso esterno. Questo elenco di lingue disponibili inoltre è configurato nell'ambito globale. Non è possibile pertanto assegnare elenchi diversi a siti diversi. È tuttavia possibile assegnare lingue differenti a numeri di accesso a conferenze telefoniche con accesso esterno diverse.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsDialInConferencingLanguageList** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsDialInConferencingLanguageList"}

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
<td><p>Consente di utilizzare caratteri jolly quando si specifica un elenco delle lingue per le conferenze telefoniche con accesso esterno. Dal momento che esiste un solo oggetto di questo tipo (globale), è possibile restituire l'elenco delle lingue senza utilizzare il parametro Filter o Identity.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Indica l'elenco delle lingue per le conferenze telefoniche con accesso esterno da restituire. In questo momento è presente solo un oggetto di questo tipo: globale. Per questo motivo non è necessario includere tale parametro quando si chiama il cmdlet <strong>Get-CsDialInConferencingLanguageList</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera l'elenco delle lingue dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsDialInConferencingLanguageList** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsDialInConferencingLanguageList** restituisce un'istanza dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.DialInConferencingSettings.DialInConferencingLanguageList.

## Vedere anche

#### Ulteriori risorse

[New-CsDialInConferencingAccessNumber](new-csdialinconferencingaccessnumber.md)  
[Set-CsDialInConferencingAccessNumber](set-csdialinconferencingaccessnumber.md)

