---
title: Remove-CsSimpleUrlConfiguration
TOCTitle: Remove-CsSimpleUrlConfiguration
ms:assetid: 6cf483ed-7a53-47b0-b87a-6ef70493ba32
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398515(v=OCS.15)
ms:contentKeyID: 49300898
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsSimpleUrlConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una o più raccolte di configurazioni degli URL semplici attualmente in uso nell'organizzazione. Gli URL semplici agevolano la partecipazione degli utenti a riunioni e conferenze e l'accesso degli amministratori al Pannello di controllo di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsSimpleUrlConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di eliminare la raccolta di configurazioni degli URL semplificati applicata al sito Redmond. Questo comando consente di eliminare tutti gli URL semplificati assegnati al sito specificato.

    Remove-CsSimpleUrlConfiguration -Identity "site:Redmond"

## ESEMPIO 2

Nell'esempio 2 vengono eliminate tutte le raccolte di configurazioni degli URL semplici applicate nell'ambito del sito. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsSimpleUrlConfiguration** e il parametro Filter per restituire tutte le raccolte di URL semplici configurate nell'ambito del sito. Il valore di filtro "site:\*" restituisce solo i dati relativi alle raccolte la cui identità (Identity) inizia con il valore "site:". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsSimpleUrlConfiguration**, che elimina ogni elemento presente nella raccolta.

    Get-CsSimpleUrlConfiguration -Filter "site:*" | Remove-CsSimpleUrlConfiguration 

## Descrizione dettagliata

In Microsoft Office Communications Server 2007 R2, per le riunioni si utilizzavano URL simili al seguente:

https://imdf.litwareinc.com/Join?uri=sip%3Akenmyer%40litwareinc.com%3Bgruu%3Bopaque%3Dapp%3Aconf%3Afocus%3Aid%3A125f95a0b0184dcea706f1a0191202a8\&key=EcznhLh5K5t

Tuttavia, URL di questo tipo non sono particolarmente intuitivi e facili da comunicare ad altri utenti. Gli URL semplificati introdotti in Lync Server 2010 risolvono questo tipo di problema mettendo a disposizione degli utenti degli URL simili al seguente:

https://meet.litwareinc.com/kenmyer/071200

Gli URL semplificati rappresentano un miglioramento notevole rispetto agli URL utilizzati in Office Communications Server. Tenere presente che gli URL semplificati non vengono creati automaticamente, ma devono essere configurati dall'utente. Inoltre, è necessario creare i record DNS (Domain Name System) per ciascun URL, configurare regole proxy inverse per gli accessi esterni, aggiungere gli URL semplificati ai certificati Front End Server e così via.

Lync Server consente di creare tre diversi tipi di URL semplici:

Meet: utilizzato per le riunioni. Occorre avere almeno un URL di tipo Meet per ciascuno dei propri domini SIP.

Admin: utilizzato per consentire agli amministratori di accedere a Lync Server.

Dialin: utilizzato per le pagine Web delle conferenze telefoniche con accesso esterno.

Gli URL semplici vengono archiviati nelle raccolte di configurazioni di URL semplici. Quando si installa Lync Server, viene creata automaticamente una raccolta globale. È inoltre possibile creare raccolte personalizzate nell'ambito del sito. In questo modo, è possibile utilizzare diversi URL semplici nei singoli siti.

Le raccolte di configurazioni degli URL semplici vengono create utilizzando il cmdlet **New-CsSimpleUrlConfiguration**. È quindi possibile utilizzare altri cmdlet, ad esempio **New-CsSimpleUrlEntry** e **Set-CsSimpleUrlConfiguration**, per inserire in queste raccolte gli URL semplici. Se in un secondo momento si decide di eliminare una o più raccolte nell'ambito del sito, utilizzare il cmdlet **Remove-CsSimpleUrlConfiguration**.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Remove-CsSimpleUrlConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsSimpleUrlConfiguration"}

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
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco della raccolta di URL semplificati da rimuovere. Per rimuovere una raccolta nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity &quot;site:Redmond.&quot; Si noti che non è consentito utilizzare i caratteri jolly per specificare l'identità.</p>
<p>È possibile inoltre eseguire questo cmdlet sulla raccolta globale utilizzando la seguente sintassi: -Identity global. In questo caso, tuttavia, la raccolta globale non verrà rimossa. Verranno eliminati al contrario tutti gli URL semplificati presenti nella raccolta.</p></td>
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
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account del tenant di Skype for Business online per le impostazioni di configurazione degli URL semplici da eliminare, ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SimpleUrl.SimpleUrlConfiguration. Il cmdlet **Remove-CsSimpleUrlConfiguration** accetta istanze dell'oggetto di configurazione URL semplice inviate tramite pipeline.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Get-CsSimpleUrlConfiguration](get-cssimpleurlconfiguration.md)  
[New-CsSimpleUrlConfiguration](new-cssimpleurlconfiguration.md)  
[Set-CsSimpleUrlConfiguration](set-cssimpleurlconfiguration.md)

