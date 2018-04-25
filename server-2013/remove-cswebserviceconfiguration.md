---
title: Remove-CsWebServiceConfiguration
TOCTitle: Remove-CsWebServiceConfiguration
ms:assetid: 1df2f881-6594-4de7-9762-8d64b2243355
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398266(v=OCS.15)
ms:contentKeyID: 49299871
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsWebServiceConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una o più raccolte di impostazioni di configurazione dei servizi Web. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsWebServiceConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono rimosse le impostazioni di configurazione dei servizi Web per il sito Redmond.

    Remove-CsWebServiceConfiguration -Identity site:Redmond

## ESEMPIO 2

Nell'esempio 2 vengono rimosse tutte le impostazioni di servizi Web configurate nell'ambito del sito. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsWebServiceConfiguration** e il parametro Filter. Il valore di filtro "service:\*" garantisce che vengano restituite solo le impostazioni che hanno un'identità che inizia con la stringa "service:". Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsWebServiceConfiguration**, che elimina ogni elemento della raccolta.

    Get-CsWebServiceConfiguration -Filter "site:*" | Remove-CsWebServiceConfiguration

## ESEMPIO 3

Il comando riportato nell'esempio 3 elimina tutte le impostazioni di configurazione di servizi Web in cui l'espansione dei gruppi è stata disabilitata. A tale scopo, il comando innanzitutto chiama il cmdlet **Get-CsWebServiceConfiguration** senza alcun parametro per restituire una raccolta di tutte le impostazioni di configurazione di servizi Web utilizzate nell'organizzazione. La raccolta così ottenuta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà EnableGroupExpansion è uguale a False. Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsWebServiceConfiguration**, che elimina ogni elemento della raccolta.

    Get-CsWebServiceConfiguration | Where-Object {$_.EnableGroupExpansion -eq $False} | Remove-CsWebServiceConfiguration

## Descrizione dettagliata

Molti componenti di Lync Server sono basati su Web: questi componenti utilizzano i servizi Web o le pagine Web per eseguire le attività. Gli utenti utilizzano ad esempio un servizio Web quando cercano i nuovi contatti nella Rubrica o quando utilizzano l'espansione gruppo per visualizzare i singoli membri di un gruppo di distribuzione. Analogamente, i componenti che includono le conferenze telefoniche con accesso esterno e il Pannello di controllo di Lync Server utilizzano le pagine Web come interfaccia tra Lync Server e gli utenti.

I cmdlet **CsWebServiceConfiguration** consentono agli amministratori di gestire le impostazioni di configurazione di servizi Web per tutta l'organizzazione. Ciò include anche la gestione dell'espansione dei gruppi, delle impostazioni dei certificati e dei metodi di autenticazione consentiti. Poiché è possibile configurare impostazioni diverse nell'ambito globale, del sito e del servizio (sebbene, in quest'ultimo caso, solo per i servizi Web), è altresì possibile personalizzare le funzionalità di servizi Web per utenti diversi in luoghi diversi.

Se si creano impostazioni di configurazione di servizi Web personalizzate nell'ambito del sito o del servizio, sarà possibile rimuoverle successivamente utilizzando il cmdlet **Remove-CsWebServiceConfiguration**. Si noti che è possibile eseguire il cmdlet **Remove-CsWebServiceConfiguration** anche per la raccolta globale di impostazioni di servizi Web. In questo caso, la raccolta globale tuttavia non verrà rimossa, in quanto Lync Server non consente di rimuovere le impostazioni globali. In realtà, per tutte le proprietà della raccolta globale verranno ripristinati i valori predefiniti. Ad esempio, si supponga di avere portato il valore della proprietà MaxGroupSizeToExpand a 500. Poiché il valore predefinito di questa proprietà è 100, la "rimozione" della raccolta globale determinerà il ripristino del valore 100 per la proprietà MaxGroupSizeToExpand.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Remove-CsWebServiceConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsWebServiceConfiguration"}

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
<td><p>Identificatore univoco delle impostazioni di configurazione di servizi Web da rimuovere. Per rimuovere le impostazioni configurate nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity &quot;site:Redmond&quot;. Per rimuovere le impostazioni configurate nell'ambito del servizio, utilizzare una sintassi simile alla seguente: -Identity &quot;service:WebServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>Il cmdlet <strong>Remove-CsWebServiceConfiguration</strong> può essere eseguito anche per la raccolta globale. In questo caso, la raccolta globale tuttavia non verrà rimossa. In realtà, tutte le proprietà di tale raccolta verranno reimpostate sui rispettivi valori predefiniti. Per reimpostare la raccolta globale, utilizzare la sintassi seguente: -Identity global.</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Web.WebServiceSettings. Il cmdlet **Remove-CsWebServiceConfiguration** accetta l'input da pipeline dell'oggetto impostazioni di servizi Web.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsWebServiceConfiguration** invece elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Web.WebServiceSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsWebServiceConfiguration](get-cswebserviceconfiguration.md)  
[New-CsWebServiceConfiguration](new-cswebserviceconfiguration.md)  
[Set-CsWebServiceConfiguration](set-cswebserviceconfiguration.md)

