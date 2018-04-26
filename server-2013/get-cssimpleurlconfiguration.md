---
title: Get-CsSimpleUrlConfiguration
TOCTitle: Get-CsSimpleUrlConfiguration
ms:assetid: 59f5528b-d1f4-4da9-9dfe-102c96c6d7c2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398392(v=OCS.15)
ms:contentKeyID: 49300643
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsSimpleUrlConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sugli URL semplici configurati per l'utilizzo nell'organizzazione. Gli URL semplici agevolano la partecipazione degli utenti a riunioni e conferenze e l'accesso degli amministratori al Pannello di controllo di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsSimpleUrlConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsSimpleUrlConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Tenant <Guid>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono restituite informazioni su tutte le raccolte di configurazione degli URL semplici attualmente in uso nell'organizzazione. A tale scopo, viene chiamato il cmdlet **Get-CsSimpleUrlConfiguration** senza parametri aggiuntivi.

    Get-CsSimpleUrlConfiguration

## ESEMPIO 2

Nell'Esempio 2, vengono restituite informazioni inerenti una singola raccolta di configurazioni degli URL semplificati: la configurazione per Identity site:Redmond.

    Get-CsSimpleUrlConfiguration -Identity "site:Redmond"

## ESEMPIO 3

Nell'esempio 3 vengono restituite informazioni su tutte le raccolte di configurazione degli URL semplificati che sono state assegnate nell'ambito del sito. A tale scopo, viene chiamato il cmdlet **Get-CsSimpleUrlConfiguration** con il parametro Filter. Il valore di filtro "site:\*" restituisce solo i dati relativi alle raccolte la cui identità inizia con il valore stringa "site:".

    Get-CsSimpleUrlConfiguration -Filter "site:*"

## ESEMPIO 4

Nell'esempio 4 vengono visualizzate informazioni dettagliate su ogni URL semplice configurato per l'utilizzo nell'organizzazione. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsSimpleUrlConfiguration** per restituire una serie completa di informazioni sugli URL semplici. Questi dati vengono quindi inviati tramite pipe al cmdlet **Select-Object**, che utilizza il parametro ExpandProperty per "espandere" il valore della proprietà SimpleUrl. Espandendo il valore di una proprietà, è possibile visualizzare tutte le informazioni archiviate in quella proprietà in un formato di facile lettura.

    Get-CsSimpleUrlConfiguration | Select-Object -ExpandProperty SimpleUrl

## ESEMPIO 5

Il comando riportato nell'esempio 5 restituisce tutti gli URL semplici per la gestione delle riunioni attualmente in uso nell'organizzazione. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsSimpleUrlConfiguration** senza alcun parametro aggiuntivo. Viene così restituita una serie completa di informazioni sugli URL semplici. Questi dati vengono quindi inviati tramite pipe al cmdlet **Select-Object**, che utilizza il parametro ExpandProperty per espandere il valore della proprietà SimpleUrl. Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo gli URL semplici nei quali la proprietà Component è uguale a "Meet".

    Get-CsSimpleUrlConfiguration | Select-Object -ExpandProperty SimpleUrl | Where-Object {$_.Component -eq "Meet"}

## Descrizione dettagliata

In Microsoft Office Communications Server 2007 R2, per le riunioni si utilizzavano URL simili al seguente:

https://imdf.litwareinc.com/Join?uri=sip%3Akenmyer%40litwareinc.com%3Bgruu%3Bopaque%3Dapp%3Aconf%3Afocus%3Aid%3A125f95a0b0184dcea706f1a0191202a8\&key=EcznhLh5K5t

Tuttavia, URL di questo tipo non sono particolarmente intuitivi e facili da comunicare ad altri utenti. Gli URL semplificati introdotti in Lync Server 2010 risolvono questo tipo di problema mettendo a disposizione degli utenti degli URL simili al seguente:

https://meet.litwareinc.com/kenmyer/071200

Gli URL semplici rappresentano un miglioramento rispetto agli URL utilizzati in Office Communications Server. Tenere presente tuttavia che gli URL semplici non vengono creati automaticamente, ma devono essere configurati dall'utente. È inoltre necessario creare record DNS (Domain Name System) per ogni URL, configurare regole di proxy inversi per gli accessi esterni, aggiungere gli URL semplici ai certificati Front End Server e così via.

Lync Server consente di creare tre diversi tipi di URL semplici:

Meet: utilizzato per le riunioni. Occorre avere almeno un URL di tipo Meet per ciascuno dei propri domini SIP.

Admin - Utilizzati per consentire agli amministratori di accedere al Pannello di controllo di Lync Server.

Dialin: utilizzato per le pagine Web delle conferenze telefoniche con accesso esterno.

Gli URL semplici vengono archiviati nelle raccolte di configurazioni di URL semplici. Quando si installa Lync Server, viene creata automaticamente una raccolta globale. È inoltre possibile creare raccolte personalizzate nell'ambito del sito. In questo modo, è possibile utilizzare diversi URL semplici nei singoli siti.

Il cmdlet **Get-CsSimpleUrlConfiguration** consente di recuperare le informazioni su tutte le raccolte di configurazioni degli URL semplificati attualmente in uso nell'organizzazione.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsSimpleUrlConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsSimpleUrlConfiguration"}

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
<td><p>Consente di utilizzare i caratteri jolly per rendere più specifiche le raccolte di URL semplificati che si otterranno. Ad esempio, la seguente sintassi restituisce tutte le raccolte di URL semplificati configurate nell'ambito del sito: -Filter &quot;site:*&quot;.</p>
<p>Si noti che non è possibile utilizzare entrambi i parametri Filter e Identity nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco della raccolta di URL semplificati da ottenere. Per ottenere la raccolta globale, utilizzare la seguente sintassi: -Identity global. Per ottenere una raccolta nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity &quot;site:Redmond.&quot; Si noti che non è consentito utilizzare i caratteri jolly per specificare l'identità. Se si desidera utilizzare i caratteri jolly, utilizzare invece il parametro Filter.</p>
<p>Se si chiama il cmdlet <strong>Get-CsSimpleUrlConfiguration</strong> senza alcun parametro, vengono restituiti tutti gli URL semplici configurati per l'utilizzo nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati di configurazione degli URL semplificati dalla copia locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di Skype for Business online per cui è necessario recuperare le impostazioni di configurazione degli URL semplici. Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Il cmdlet **Get-CsSimpleUrlConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SimpleUrl.SimpleUrlConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsSimpleUrlConfiguration](new-cssimpleurlconfiguration.md)  
[Remove-CsSimpleUrlConfiguration](remove-cssimpleurlconfiguration.md)  
[Set-CsSimpleUrlConfiguration](set-cssimpleurlconfiguration.md)

