---
title: New-CsSimpleUrlConfiguration
TOCTitle: New-CsSimpleUrlConfiguration
ms:assetid: 3140f15a-e448-42fe-b494-bf9caba32b35
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425813(v=OCS.15)
ms:contentKeyID: 49300094
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsSimpleUrlConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta di configurazioni di URL semplici. Gli URL semplici agevolano la partecipazione degli utenti a riunioni e conferenze e l'accesso degli amministratori al Pannello di controllo di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsSimpleUrlConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-SimpleUrl <PSListModifier>] [-Tenant <Guid>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 consente di creare una nuova raccolta di URL semplici per il sito Redmond. Visto che nel comando non sono inclusi altri parametri oltre ad Identity, la nuova raccolta non conterrà alcun URL semplice. Questo comando avrà esito negativo se il sito Redmond ospita già una raccolta di URL semplici.

    New-CsSimpleUrlConfiguration -Identity "site:Redmond"

## ESEMPIO 2

Nell'esempio 2 viene illustrato come creare una nuova raccolta di URL semplici che include due URL semplici, uno per la gestione delle riunioni e uno per le conferenze telefoniche con accesso esterno. A tale scopo, il primo comando dell'esempio utilizza il cmdlet **New-CsSimpleUrlEntry** per creare una voce URL che punta al sito https://dialin.litwareinc.com. Questa voce URL è archiviata in una variabile denominata $urlEntry. Il secondo comando crea quindi un'altra voce URL che punta a https://meet.fabrikam.com.

A seguire, viene utilizzato il cmdlet **New-CsSimpleUrl** per creare un'istanza solo in memoria di un URL semplice. In questo esempio, il componente URL è impostato su dialin, il dominio è impostato su un asterisco (\*), ActiveUrl è impostato su https://dialin.fabrikam.com, mentre la proprietà SimpleUrl è impostata su $urlEntry, che rappresenta la voce URL creata nel primo comando. Un comando simile viene utilizzato per creare un URL semplice per meet.fabrikam.com.

Dopo aver creato gli URL (e dopo averli archiviati nei riferimenti a oggetto $simpleUrl e $simpleUrl2), l'ultimo comando nell'esempio crea una nuova raccolta di URL semplici per il sito Redmond e aggiunge i due nuovi URL solo in memoria a tale raccolta. I nuovi URL vengono aggiunto alla raccolta con il cmdlet **New-CsSimpleUrlConfiguration**, il parametro SimpleUrl e il valore di parametro @{Add=$simpleUrl, $simpleUrl2}. Questa sintassi indica semplicemente che gli URL memorizzati nei riferimenti oggetto $simpleUrl e $simpleUrl2 devono essere aggiunti alla proprietà SimpleUrl.

    $urlEntry = New-CsSimpleUrlEntry -Url "https://dialin.fabrikam.com"
    $simpleUrl = New-CsSimpleUrl -Component "dialin" -Domain "*" -SimpleUrlEntry $urlEntry -ActiveUrl "https://dialin.fabrikam.com"
    
    $urlEntry2 = New-CsSimpleUrlEntry -Url "https://meet.fabrikam.com"
    $simpleUrl2 = New-CsSimpleUrl -Component "meet" -Domain "fabrikam.com" -SimpleUrlEntry $urlEntry2 
    
    New-CsSimpleUrlConfiguration -Identity "site:Redmond" -SimpleUrl @{Add=$simpleUrl,$simpleUrl2}

## Descrizione dettagliata

In Microsoft Office Communications Server 2007 R2, le riunioni presentano URL simili al seguente:

https://imdf.litwareinc.com/Join?uri=sip%3Akenmyer%40litwareinc.com%3Bgruu%3Bopaque%3Dapp%3Aconf%3Afocus%3Aid%3A125f95a0b0184dcea706f1a0191202a8\&key=EcznhLh5K5t

Tuttavia, tali URL non sono particolarmente intuitivi e non risultano facili da comunicare a un altro utente. Gli URL semplici introdotti in Lync Server 2010 risolvono questo tipo di problemi mettendo a disposizione degli utenti degli URL simili al seguente:

https://meet.litwareinc.com/kenmyer/071200

Gli URL semplici rappresentano un miglioramento rispetto agli URL utilizzati in Office Communications Server. Tuttavia, gli URL semplici non vengono creati automaticamente, ma devono essere configurati dall'utente. Inoltre, è necessario eseguire operazioni quali la creazione di record DNS (Domain Name System) per ogni URL, la configurazione di regole proxy inverso per l'accesso esterno, l'aggiunta degli URL semplici ai certificati Front End Server e così via.

Lync Server consente di creare tre diversi tipi di URL semplici:

Meet - Usati per le riunioni. È necessario disporre di almeno un URL Meet per i singoli domini SIP in uso.

Admin - Utilizzati per consentire agli amministratori di accedere al Pannello di controllo di Lync Server.

Dialin - Utilizzati per la pagina Web delle conferenze telefoniche con accesso esterno.

Gli URL semplici vengono archiviati nelle raccolte di configurazioni di URL semplici. Quando si installa Lync Server, viene creata automaticamente una raccolta globale. È inoltre possibile creare raccolte personalizzate nell'ambito del sito. In questo modo, è possibile utilizzare diversi URL semplici nei singoli siti.

Le raccolte di configurazioni di URL semplici vengono create tramite il cmdlet **New-CsSimpleUrlConfiguration**. È quindi possibile utilizzare cmdlet aggiuntivi (come il cmdlet **New-CsSimpleUrl** e il cmdlet **Set-CsSimpleUrlConfiguration**) per popolare queste raccolte con URL semplici. Dopo aver aggiornato una raccolta di URL semplici, è necessario eseguire il cmdlet **Enable-CsComputer**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **New-CsSimpleUrlConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets -match "New-CsSimpleUrlConfiguration"}

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
<td><p>Identificatore univoco per la nuova raccolta di configurazioni di URL semplici. Poiché le nuove raccolte possono essere create solo nell'ambito del sito, l'identità deve utilizzare il prefisso &quot;site:&quot; seguito dal nome del sito. Ad esempio, questa sintassi consente di creare una nuova raccolta per il sito Redmond: -Identity &quot;site:Redmond&quot;.</p></td>
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
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>SimpleUrl</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Gli URL semplici configurati per questa raccolta. Questi URL devono essere creati tramite il cmdlet <strong>New-SimpleUrl</strong> e il cmdlet <strong>New-SimpleUrlEntry</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di Skype for Business online per cui vengono create nuove impostazioni di configurazione degli URL semplici. Ad esempio:</p>
<p>-Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID tenant per ciascun tenant eseguendo questo comando:</p>
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

Nessuno.

## Tipi restituiti

Il cmdlet **New-CsSimpleUrlConfiguration** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.SimpleUrl.SimpleUrlConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsSimpleUrlConfiguration](get-cssimpleurlconfiguration.md)  
[New-CsSimpleUrl](new-cssimpleurl.md)  
[New-CsSimpleUrlEntry](new-cssimpleurlentry.md)  
[Remove-CsSimpleUrlConfiguration](remove-cssimpleurlconfiguration.md)  
[Set-CsSimpleUrlConfiguration](set-cssimpleurlconfiguration.md)

