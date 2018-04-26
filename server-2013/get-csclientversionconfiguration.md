---
title: Get-CsClientVersionConfiguration
TOCTitle: Get-CsClientVersionConfiguration
ms:assetid: ed39feda-ebcf-4ed6-a970-64543f150b16
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399072(v=OCS.15)
ms:contentKeyID: 49302373
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsClientVersionConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera informazioni sulla raccolta specificata delle impostazioni di configurazione della versione del client in uso nell'organizzazione. Le impostazioni di configurazione della versione del client determinano se Lync Server verifica il numero di versione di ogni applicazione client che accede al sistema. Se il filtro versione client è abilitato, la capacità dell'applicazione client di accedere al sistema dipenderà dalle impostazioni configurate nel criterio di versione client pertinente. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsClientVersionConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsClientVersionConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nel primo esempio viene chiamato il cmdlet **Get-CsClientVersionConfiguration** senza specificare ulteriori parametri. In questo modo, il cmdlet **Get-CsClientVersionConfiguration** restituirà una raccolta di tutte le impostazioni di configurazione della versione client attualmente in uso nell'organizzazione.

    Get-CsClientVersionConfiguration

## ESEMPIO 2

In questo esempio il cmdlet **Get-CsClientVersionConfiguration** restituisce tutte le impostazioni di configurazione della versione client con valore Identity site:Redmond. Poiché le identità devono essere univoche, il comando non restituirà mai più di un elemento.

    Get-CsClientVersionConfiguration -Identity site:Redmond

## ESEMPIO 3

Nell'esempio 3 vengono restituite tutte le impostazioni di configurazione della versione client applicate nell'ambito del sito. A tale scopo, vengono inclusi il parametro Filter e il valore di filtro "site:\*". Tale valore di filtro indica al cmdlet **Get-CsClientVersionConfiguration** di restituire solo le impostazioni il cui valore Identity inizia con il valore stringa "site:".

    Get-CsClientVersionConfiguration -Filter "site:*"

## ESEMPIO 4

Nell'esempio 4 vengono restituite tutte le impostazioni di configurazione della versione client attualmente disabilitate. Per eseguire questa attività, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsClientVersionConfiguration** per restituire una raccolta di tutte le impostazioni della versione client configurate per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object** che applica un filtro per limitare la raccolta alle impostazioni in cui la proprietà Enabled è uguale a False.

    Get-CsClientVersionConfiguration | Where-Object {$_.Enabled -eq $False}

## Descrizione dettagliata

Con Lync Server gli amministratori dispongono di uno spazio di manovra considerevole quando devono specificare il software client (e, ugualmente importante, il numero di versione del software) che gli utenti possono utilizzare per accedere al sistema. Ad esempio, non vi sono motivi tecnici che impongono agli utenti di accedere a Lync Server utilizzando Lync. Da un punto di vista tecnico, niente impedisce agli utenti di accedere utilizzando Microsoft Office Communicator 2007 R2.

Vi potrebbero essere invece motivi di carattere non tecnico per cui si preferisce che gli utenti non accedano tramite Office Communicator 2007 R2. Office Communicator 2007 R2 ad esempio non supporta tutte le caratteristiche e le funzionalità disponibili in Lync. Agli utenti che effettuano l'accesso mediante Office Communicator 2007 R2 verrà pertanto offerta un'esperienza diversa rispetto agli utenti che per l'accesso utilizzano Lync. Ciò può creare difficoltà per gli utenti; può inoltre creare difficoltà per il personale del supporto tecnico che deve fornire assistenza per varie applicazioni client diverse.

Se questo può costituire un problema per l'organizzazione, è possibile utilizzare il filtro versione client per specificare quali applicazioni client possono essere utilizzate per accedere a Lync Server. Quando si installa Lync Server, viene installato e abilitato un insieme globale di impostazioni di configurazione per la versione client. Tali impostazioni vengono utilizzate per determinare se il filtro versione client è abilitato o meno. Oltre alle impostazioni globali, anche le impostazioni di configurazione della versione client possono essere applicate nell'ambito del sito. In questo caso, le impostazioni del sito avranno la precedenza sulle impostazioni globali.

Il cmdlet **Get-CsClientVersionConfiguration** consente di recuperare le informazioni sulle impostazioni di configurazione della versione client attualmente in uso nell'organizzazione. Il cmdlet non restituisce informazioni su quali applicazioni client sono consentite e quali invece non lo sono. Per recuperare tali informazioni, utilizzare il cmdlet **Get-CsClientVersionPolicy**.

Anche tale configurazione della versione client non è una funzionalità di sicurezza. La tecnologia si basa su funzioni di auto-reporting da applicazioni client e non viene verificato se un'applicazione e il relativo numero di versione sono realmente quelli dichiarati.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsClientVersionConfiguration** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsClientVersionConfiguration"}

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
<td><p>Consente di utilizzare caratteri jolly per restituire una o più raccolte di impostazioni di configurazione della versione client. Per restituire una raccolta di tutte le impostazioni configurate nell'ambito del sito, utilizzare la sintassi seguente: -Filter site:*. Per restituire una raccolta di tutte le impostazioni con valore stringa &quot;EMEA&quot; in un punto qualsiasi del parametro Identity (l'unica proprietà in base alla quale è possibile applicare il filtro), utilizzare la seguente sintassi: -Filter *EMEA*.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Indica l'identificatore univoco della raccolta di impostazioni di configurazione client da restituire. Per fare riferimento alle impostazioni globali, utilizzare la seguente sintassi: -Identity global. Per far riferimento a una raccolta configurata nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Non è possibile utilizzare caratteri jolly per specificare il parametro Identity. Se è necessario utilizzare caratteri jolly, includere invece il parametro Filter.</p>
<p>Se tale parametro non è specificato, il cmdlet <strong>Get-CsClientVersionConfiguration</strong> restituirà una raccolta di tutte le impostazioni di configurazione della versione client attualmente in uso nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione della versione client dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsClientVersionConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsClientVersionConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsClientVersionConfiguration](new-csclientversionconfiguration.md)  
[Remove-CsClientVersionConfiguration](remove-csclientversionconfiguration.md)  
[Set-CsClientVersionConfiguration](set-csclientversionconfiguration.md)

