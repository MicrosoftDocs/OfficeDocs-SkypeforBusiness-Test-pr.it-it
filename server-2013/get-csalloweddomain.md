---
title: Get-CsAllowedDomain
TOCTitle: Get-CsAllowedDomain
ms:assetid: 0b693788-2270-4bf3-b899-f5cf4321351b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398164(v=OCS.15)
ms:contentKeyID: 49299643
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAllowedDomain

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui domini inclusi nell'elenco dei domini approvati per la federazione. Dopo l'approvazione di un dominio per la federazione, ovvero l'aggiunta del dominio nell'elenco dei domini consentiti, gli utenti possono scambiare messaggi istantanei e informazioni sulla presenza con persone che dispongono di account in quel dominio. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsAllowedDomain [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Get-CsAllowedDomain [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 restituisce una raccolta di tutti i domini inclusi nell'elenco dei domini approvati per la federazione. Chiamando il cmdlet **Get-CsAllowedDomain** senza ulteriori parametri, viene restituita sempre la raccolta di domini approvati completa.

    Get-CsAllowedDomain

## ESEMPIO 2

Nell'Esempio 2 vengono restituite le informazioni sul dominio consentito con Identity "fabrikam.com". Poiché le identità devono essere univoche, il comando non restituirà mai più di un elemento.

    Get-CsAllowedDomain -Identity fabrikam.com

## ESEMPIO 3

Il comando riportato nell'esempio 3 restituisce una raccolta di tutti i domini consentiti che contengono il valore stringa "fabrikam" in qualunque punto della relativa identità. A tale scopo, il comando utilizza il parametro Filter e il valore di filtro "\*fabrikam\*". Questo valore di filtro indica al cmdlet **Get-CsAllowedDomain** di restituire solo i domini in cui Identity (la sola proprietà in base alla quale è possibile filtrare i dati) include il valore stringa "fabrikam". Domini quali fabrikam.com, fabrikam.net e africa.fabrikam.org verranno tutti restituiti da questo comando.

    Get-CsAllowedDomain -Filter *fabrikam*

## ESEMPIO 4

Nell'esempio 4 vengono utilizzati i cmdlet **Get-CsAllowedDomain** e **Where-Object** per restituire una raccolta di tutti i domini per i quali non è stato immesso alcun valore per la proprietà ProxyFqdn. A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsAllowedDomain** senza parametri aggiuntivi per restituire una raccolta di tutti i domini consentiti. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i domini consentiti in cui la proprietà ProxyFqdn è uguale a un valore Null. Un valore Null significa che non è stato immesso alcun valore per ProxyFqdn. Per trovare invece tutti i domini per i quali è stato configurato un valore per la proprietà ProxyFqdn, utilizzare la sintassi seguente:

Where-Object {$\_.ProxyFqdn -ne $Null}

    Get-CsAllowedDomain | Where-Object {$_.ProxyFqdn -eq $Null}

## ESEMPIO 5

Nell'esempio 5 vengono restituiti tutti i domini consentiti il cui stato di integrità è stato verificato dal Monitoring Server. A tale scopo, viene utilizzato innanzitutto il cmdlet **Get-CsAllowedDomain** per restituire una raccolta di tutti i domini inclusi nell'elenco dei domini consentiti. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i domini in cui la proprietà MarkForMonitoring è uguale a True.

    Get-CsAllowedDomain | Where-Object {$_.MarkForMonitoring -eq $True}

## Descrizione dettagliata

La federazione consente a due organizzazioni di instaurare una relazione di trust che facilita la comunicazione tra i due gruppi. Quando viene stabilita una federazione, gli utenti delle due organizzazioni possono inviarsi messaggi istantanei, sottoscrivere l'opzione di notifiche di presenza e comunicare in altri modi tra loro utilizzando applicazioni SIP come Lync. Lync Server supporta tre tipi di federazione: 1) federazione diretta tra la propria e un'altra organizzazione, 2) federazione tra la propria organizzazione e un provider pubblico e 3) federazione tra la propria organizzazione e un provider di hosting di terze parti.

La configurazione di una federazione con un'altra organizzazione implica diverse attività. Per iniziare si deve abilitare il proprio Access Edge Server per consentire la federazione. Inoltre, l'altra organizzazione deve a sua volta abilitare il processo federativo; la federazione non può essere instaurata se entrambe le parti non sono d'accordo.

Per impostare una relazione federata potrebbe inoltre essere necessario gestire due elenchi relativi alla federazione: l'elenco dei domini consentiti e quello dei domini bloccati. L'elenco dei domini consentiti (necessario se è stato disabilitato EnablePartnerDiscovery) rappresenta le organizzazioni con cui si è scelto di attuare la federazione. Se un dominio è incluso nell'elenco dei domini consentiti (a seconda delle impostazioni di configurazione), gli utenti saranno in grado di scambiare messaggi istantanei e informazioni sulla presenza con utenti in possesso di un account nel dominio federato. Al contrario, l'elenco dei domini bloccati rappresenta i domini con i quali gli utenti non sono autorizzati ad attuare una federazione (ad esempio i messaggi inviati da un dominio bloccato verranno automaticamente rifiutati da Lync Server).

Il cmdlet **Get-CsAllowedDomain** consente di ottenere informazioni su tutti i domini inclusi nell'elenco dei domini consentiti.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsAllowedDomain** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAllowedDomain"}

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
<td><p>Consente di utilizzare i caratteri jolly per ottenere uno o più domini dall'elenco dei domini consentiti. Per ottenere tutti i domini che hanno un'identità che inizia con la lettera &quot;r&quot;, utilizzare la seguente sintassi: -Filter r*. Per ottenere tutti i domini con un'identità che termina con &quot;.net&quot;, utilizzare la seguente sintassi: -Filter &quot;*.net&quot;. Per ottenere tutti i domini che hanno un'identità che inizia con la lettera &quot;r&quot; o la lettera &quot;g&quot;, utilizzare la seguente sintassi: -Filter [rg]*.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Il nome del dominio da ottenere. Nell'elenco dei domini consentiti, i domini sono riportati con il loro nome completo (FQDN); pertanto, l'identità di un dominio potrebbe essere fabrikam.com o contoso.net e non è possibile utilizzare i caratteri jolly per specificarla. Per utilizzare i caratteri jolly per ottenere un determinato dominio o gruppo di domini è necessario utilizzare il parametro Filter.</p>
<p>Se questo parametro non viene specificato, verranno restituiti tutti i domini inclusi nell'elenco dei domini consentiti.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i domini consentiti dalla replica locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsAllowedDomain** non accetta input da pipeline.

## Tipi restituiti

Restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowedDomain.

## Vedere anche

#### Ulteriori risorse

[New-CsAllowedDomain](new-csalloweddomain.md)  
[Remove-CsAllowedDomain](remove-csalloweddomain.md)  
[Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)  
[Set-CsAllowedDomain](set-csalloweddomain.md)

