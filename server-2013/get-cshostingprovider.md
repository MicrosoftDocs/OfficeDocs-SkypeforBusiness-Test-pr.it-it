---
title: Get-CsHostingProvider
TOCTitle: Get-CsHostingProvider
ms:assetid: fd493022-eb53-4084-aa81-213cb5e959fc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413078(v=OCS.15)
ms:contentKeyID: 49302578
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsHostingProvider

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui provider di hosting configurati per l'utilizzo nella propria organizzazione. Un provider di hosting è un'organizzazione di terze parti che fornisce servizi di messaggistica istantanea, informazioni sulla presenza e altri servizi correlati a un dominio con il quale si desidera attuare una federazione. I provider di hosting come Microsoft Lync Online 2010 si differenziano dai provider pubblici, ad esempio Yahoo\!, MSN e AOL, in quanto non offrono servizi al pubblico. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsHostingProvider [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsHostingProvider [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene restituita una raccolta di tutti i provider di hosting configurati per essere utilizzati nell'organizzazione. Se si chiama il cmdlet **Get-CsHostingProvider** senza parametri aggiuntivi, viene restituita la raccolta completa dei provider di hosting.

    Get-CsHostingProvider

## ESEMPIO 2

Nell'esempio 2 viene restituito il provider di hosting con identità Fabrikam.com. Poiché le identità devono essere univoche tra i provider di hosting, il comando non restituirà mai più di un elemento.

    Get-CsHostingProvider -Identity Fabrikam.com

## ESEMPIO 3

Con il comando mostrato nell'esempio 3 viene restituita una raccolta di tutti i provider di hosting che hanno un'identità che termina con il valore stringa ".org", ad esempio, fabrikam.org e contoso.org.

    Get-CsHostingProvider -Filter *.org

## ESEMPIO 4

Nell'esempio 4 vengono restituiti tutti i provider di hosting che sono attualmente abilitati per l'uso. A tal scopo, viene innanzitutto chiamato il cmdlet **Get-CsHostingProvider** per restituire una raccolta di tutti i provider di hosting attualmente configurati nell'organizzazione. La raccolta così ottenuta viene quindi inviata tramite pipe al cmdlet **Where-Object** che seleziona solo quei provider in cui la proprietà Enabled è uguale a True.

    Get-CsHostingProvider | Where-Object {$_.Enabled -eq $True}

## ESEMPIO 5

Nell'esempio 5 vengono restituiti tutti i provider di hosting che dispongono di uno spazio degli indirizzi condiviso e che ospitano utenti di Lync Server. Di conseguenza, vengono restituiti tutti i provider di hosting che fanno parte di una configurazione con dominio diviso (per dominio diviso si intende che alcuni account di Lync Server vengono gestiti in locale mentre altri account vengono gestiti da un provider di hosting). A tal scopo, viene innanzitutto utilizzato il cmdlet **Get-CsHostingProvider** per restituire una raccolta di tutti i provider di hosting attualmente configurati. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object** che seleziona solo i provider che soddisfano due criteri: 1) la proprietà Enabled è uguale a True e 2) la proprietà EnabledSharedAddressSpace è uguale a True.

    Get-CsHostingProvider | Where-Object {$_.Enabled -eq $True -and $_.EnabledSharedAddressSpace -eq $True}

## ESEMPIO 6

Il comando riportato nell'esempio 6 consente di visualizzare tutti i valori delle proprietà per i provider di hosting configurati per l'utilizzo nell'organizzazione. Per impostazione predefinita, i valori delle proprietà per EnabledSharedAddressSpace e HostsOCSUsers non vengono visualizzati quando si esegue il cmdlet **Get-CsHostingProvider**. Per visualizzare i valori per queste proprietà. le informazioni restituite dal cmdlet **Get-CsHostingProvider** vengono inviate tramite pipe al cmdlet **Select-Object**, mentre il carattere jolly (\*) indica al cmdlet **Select-Object** di visualizzare tutte le proprietà e i valori delle proprietà per gli elementi restituiti.

    Get-CsHostingProvider | Select-Object *

## Descrizione dettagliata

La federazione è un mezzo per stabilire una relazione di trust tra due organizzazioni per agevolare la comunicazione tra i due gruppi. Quando è stata stabilita una federazione, gli utenti delle due organizzazioni possono inviarsi messaggi istantanei, sottoscrivere l'opzione di notifiche di presenza e comunicare in altri modi tra loro utilizzando le applicazioni SIP come Lync. Lync Server supporta tre tipi di federazione: 1) federazione diretta tra due organizzazioni; 2) federazione tra un'organizzazione e un provider pubblico; e 3) federazione tra un'organizzazione e un provider di hosting di terze parti.

Un provider di hosting è un'organizzazione che fornisce servizi di comunicazione SIP ad altre organizzazioni; ad esempio, Fabrikam, Inc. potrebbe ospitare utenti di Contoso, Northwind Traders e Wingtip Toys. Quando si stabilisce una relazione di federazione con un provider di hosting, si definisce in realtà una federazione con tutte le organizzazioni ospitate da quel provider. Ad esempio, se un'organizzazione si associa tramite federazione a Fabrikam, gli utenti dell'organizzazione potranno scambiare messaggi istantanei e informazioni sulla presenza con gli utenti di Contoso, Northwind Traders e Wingtip Toys.

I provider di hosting vengono utilizzati anche nello scenario dei domini combinati. In uno scenario di dominio diviso, alcuni utenti di Lync Server dispongono di account ospitati in locale, ovvero ospitati nell'implementazione locale di Lync Server. Altri utenti dispongono invece di account gestiti in remoto da provider di hosting di terze parti. La federazione con il provider di hosting consente agli utenti in locale e in remoto di comunicare tra loro.

Il cmdlet **Get-CsHostingProvider** consente di restituire informazioni su tutti i provider di hosting che sono stati configurati per essere utilizzati nell'organizzazione.

Non è possibile attuare la federazione con un provider di hosting se gli server perimetrali sono configurati per utilizzare il routing predefinito anziché il routing del server DNS (Domain Name System).

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Get-CsHostingProvider** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsHostingProvider"}

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
<td><p>Consente di utilizzare valori con caratteri jolly per restituire uno o più provider di hosting. Ad esempio, per restituire tutti i provider di hosting che hanno un'identità che termina con il valore stringa &quot;.com&quot;, utilizzare la sintassi seguente: -Filter &quot;*.com&quot;. Per restituire tutti i provider di hosting che hanno un'identità che inizia con la stringa &quot;Fabri&quot;, utilizzare la sintassi seguente: -Filter &quot;Fabri*&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Identificatore univoco per il provider di hosting da restituire. L'identità può essere il nome di dominio completo per provider di hosting (ad esempio fabrikam.com) o il nome dell'azienda che fornisce i servizi (Fabrikam, Inc.).</p>
<p>Se questo parametro non viene specificato, il cmdlet <strong>Get-CsHostingProvider</strong> restituirà una raccolta di tutti i provider di hosting configurati per essere utilizzati nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati del provider di hosting dalla replica locale del archivio di gestione centrale anziché dallo stesso archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsHostingProvider** non accetta input inviato tramite pipe.

## Tipi restituiti

Restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayHostingProvider.

## Vedere anche

#### Ulteriori risorse

[Disable-CsHostingProvider](disable-cshostingprovider.md)  
[Enable-CsHostingProvider](enable-cshostingprovider.md)  
[New-CsHostingProvider](new-cshostingprovider.md)  
[Remove-CsHostingProvider](remove-cshostingprovider.md)  
[Set-CsHostingProvider](set-cshostingprovider.md)

