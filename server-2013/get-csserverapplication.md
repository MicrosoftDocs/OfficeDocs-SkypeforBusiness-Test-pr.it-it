---
title: Get-CsServerApplication
TOCTitle: Get-CsServerApplication
ms:assetid: 46769cc2-9e61-4437-b74a-24f3cf118f39
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425948(v=OCS.15)
ms:contentKeyID: 49300393
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsServerApplication

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle applicazioni server in uso nell'organizzazione. Le applicazioni server sono applicazioni ospitate da Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsServerApplication [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsServerApplication [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 restituisce informazioni su tutte le applicazioni server attualmente in uso nell'organizzazione. A tale scopo, viene chiamato il cmdlet **Get-CsServerApplication** senza alcun parametro.

    Get-CsServerApplication

## ESEMPIO 2

Con l'esempio 2 vengono restituite le informazioni per tutte le applicazioni server in esecuzione sul servizio EdgeServer:atl-edge-001.litwareinc.com.

    Get-CsServerApplication -Identity "service:EdgeServer:atl-edge-001.litwareinc.com"

## ESEMPIO 3

Con l'esempio 3 vengono restituite le informazioni per una singola applicazione server, l'applicazione con identità "Registrar:atl-cs-001.litwareinc.com/ExumRouting".

    Get-CsServerApplication -Identity "service:Registrar:atl-cs-001.litwareinc.com/ExumRouting"

## ESEMPIO 4

Nell'esempio 4 vengono restituite tutte le applicazioni server configurate per l'utilizzo nel pool atl-cs-001.litwareinc.com. Per ottenere questo risultato, viene utilizzato il parametro Filter con valore "service:\*:atl-cs-001.litwareinc.com\*". Il valore di filtro limita i dati restituiti alle applicazioni con identità (Identity) che inizia con i caratteri "service:" e che include i caratteri ":atl-cs-001.litwareinc.com".

    Get-CsServerApplication -Filter "service:*:atl-cs-001.litwareinc.com*"

## ESEMPIO 5

Nell'esempio 5 vengono restituite informazioni per tutte le applicazioni server attualmente disabilitate. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsServerApplication** per restituire una raccolta di tutte le applicazioni server configurate per l'utilizzo nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le applicazioni in cui la proprietà Enabled è uguale a False.

    Get-CsServerApplication | Where-Object {$_.Enabled -eq $False}

## ESEMPIO 6

L'esempio 6 è una variante del comando riportato nell'esempio 5. Nell'esempio 6 vengono restituite informazioni per tutte le applicazioni server contrassegnate come critiche e attualmente disabilitate. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsServerApplication** senza parametri per restituire una raccolta di tutte le applicazioni server configurate per l'utilizzo. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le applicazioni che soddisfano due criteri: la proprietà Critical deve essere uguale a True e la proprietà Enabled deve essere uguale a False. L'operatore -and garantisce la restituzione dei soli oggetti che soddisfano entrambi i criteri.

    Get-CsServerApplication | Where-Object {$_.Critical -eq $True -and $_.Enabled -eq $False}

## ESEMPIO 7

Nell'esempio 7 vengono restituite informazioni per tutte le applicazioni server che contengono il valore stringa "routing" nel relativo URI. A tale scopo, viene innanzitutto utilizzato il cmdlet **Get-CsServerApplication** per recuperare tutte le applicazioni server attualmente in uso. La raccolta risultante viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le applicazioni in cui la proprietà Uri contiene il valore stringa "routing".

    Get-CsServerApplication | Where-Object {$_.Uri -like "*routing*"}

## ESEMPIO 8

Nell'esempio 8 vengono restituite informazioni su tutte le applicazioni server a cui è stato assegnato uno script. A tale scopo, il comando recupera innanzitutto una raccolta di tutte le applicazioni server attualmente in uso. Tali informazioni vengono recuperate mediante una chiamata al cmdlet **Get-CsServerApplication** senza parametri. La raccolta completa delle applicazioni server viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le applicazioni in cui la proprietà ScriptName è diversa da un valore Null. Se la proprietà ScriptName è diversa da un valore Null, significa che è stato assegnato uno script a tale applicazione.

    Get-CsServerApplication | Where-Object {$_.ScriptName -ne $Null}

## Descrizione dettagliata

Le applicazioni server fanno riferimento a singoli programmi che vengono eseguiti in Lync Server. Il cmdlet **Get-CsServerApplication** consente agli amministratori di restituire informazioni su una o su tutte le applicazioni in esecuzione come parte di Lync Server.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Get-CsServerApplication** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsServerApplication"}

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
<td><p>Consente di utilizzare i caratteri jolly durante la restituzione di un'applicazione server o di un set di applicazioni server. Ad esempio, per restituire tutte le applicazioni server che contengono il valore stringa &quot;IIMFilter&quot; in Identity, utilizzare questa sintassi: -Filter &quot;*IIMFilter*&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Un identificatore univoco per l'applicazione server da recuperare. Le identità delle applicazioni server sono composte dal servizio in cui è ospitata l'applicazione seguito dal nome dell'applicazione. Ad esempio, il server applicazioni denominato QoEAgent può avere un'identità analoga alla seguente: service: Registrar:atl-cs-001.litwareinc.com/QoEAgent.</p>
<p>Per recuperare una raccolta di tutte le applicazioni in esecuzione su un determinato servizio è sufficiente tralasciare il nome dell'applicazione:</p>
<p>-Identity &quot;Registrar:atl-cs-001.litwareinc.com &quot;</p>
<p>Se questo parametro viene omesso, la chiamata al cmdlet <strong>Get-CsServerApplication</strong> restituisce tutte le applicazioni server.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati delle applicazioni server dalla replica locale del archivio di gestione centrale anziché dal archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsServerApplication** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Get-CsServerApplication** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.ServerApplication.Application.

## Vedere anche

#### Ulteriori risorse

[New-CsServerApplication](new-csserverapplication.md)  
[Remove-CsServerApplication](remove-csserverapplication.md)  
[Set-CsServerApplication](set-csserverapplication.md)

