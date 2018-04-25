---
title: New-CsAllowedDomain
TOCTitle: New-CsAllowedDomain
ms:assetid: 7e040cf8-8e6f-4293-b7c4-1be76053d43d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398628(v=OCS.15)
ms:contentKeyID: 49301112
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsAllowedDomain

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Aggiunge un dominio all'elenco dei domini approvati per la federazione. Dopo l'approvazione di un dominio per la federazione, ovvero l'aggiunta del dominio all'elenco dei domini consentiti, gli utenti possono scambiare messaggi istantanei e informazioni sulla presenza con persone che dispongono di account nel dominio federato. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsAllowedDomain -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    New-CsAllowedDomain -Domain <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Comment <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-MarkForMonitoring <$true | $false>] [-ProxyFqdn <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 il dominio fabrikam.com viene aggiunto all'elenco dei domini consentiti. A tale scopo, viene chiamato il cmdlet **New-CsAllowedDomain** con il parametro Identity. A tale parametro viene assegnato il nome del dominio da aggiungere all'elenco dei domini consentiti. Si noti che il comando avrà esito negativo se fabrikam.com è già presente nell'elenco dei domini consentiti o in quello dei domini bloccati

    New-CsAllowedDomain -Identity "fabrikam.com"

## ESEMPIO 2

L'Esempio 2 è una variazione del comando mostrato nell'Esempio 1. In questo caso però vengono inclusi due parametri aggiuntivi a Identity: ProxyFqdn viene utilizzato per specificare il nome completo del dominio del server proxy fabrikam.com e MarkForMonitoring viene utilizzato per aggiungere questa connessione federata all'elenco degli elementi monitorati da Monitoring Server.

    New-CsAllowedDomain -Identity "fabrikam.com" -ProxyFqdn "proxyserver.fabrikam.com" -MarkForMonitoring $True -Comment "Contact: Ken Myer (kenmyer@fabrikam.com)"

## ESEMPIO 3

Nell'esempio 3 viene illustrato come utilizzare il parametro InMemory per creare un nuovo dominio consentito che inizialmente esiste solo in memoria. Dopo aver modificato i valori delle proprietà di questo dominio solo in memoria, è possibile utilizzare il cmdlet **Set-CsAllowedDomain** per aggiungere il dominio all'elenco dei domini consentiti.

A tale scopo, il primo comando nell'esempio utilizza il cmdlet **New-CsAllowedDomain** e il parametro InMemory per creare un dominio consentito con identità (Identity) fabrikam.com. Questo dominio virtuale viene quindi archiviato nella variabile $x.

Le righe 2, 3, e 4 vengono utilizzate per modificare rispettivamente i valori delle proprietà ProxyFqdn, MarkForMonitoring e Comment. Dopo la modifica dei valori di tutte le proprietà, il comando finale utilizza il cmdlet **Set-CsAllowedDomain** per aggiungere il dominio virtuale all'elenco dei domini consentiti. Considerare che fino a quando non viene chiamato il cmdlet **Set-CsAllowedDomain**, fabrikam.com esiste solo in memoria: Se si esegue il cmdlet **Get-CsAllowedDomain** in qualunque momento prima dell'ultima riga nell'esempio, fabrikam.com non compare nell'elenco dei domini consentiti. Fabrikam.com non comparirà nell'elenco dei domini consentiti finché non verrà chiamato il cmdlet **Set-CsAllowedDomain**.

    $x = New-CsAllowedDomain -Identity "fabrikam.com" -InMemory
    $x.ProxyFqdn = "proxyserver.fabrikam.com" 
    $x.MarkForMonitoring = $True 
    $x.Comment = "Contact: Ken Myer (kenmyer@fabrikam.com)"
    Set-CsAllowedDomain -Instance $x

## Descrizione dettagliata

La federazione è un mezzo per stabilire una relazione di trust tra due organizzazioni per agevolare la comunicazione tra i due gruppi. Una volta stabilita una federazione, gli utenti delle due organizzazioni possono scambiare messaggi istantanei, sottoscrivere l'opzione di notifiche di presenza e comunicare comunque tra loro utilizzando le applicazioni SIP, ad esempio Lync. Lync Server supporta tre tipi di federazione: 1) federazione diretta tra due organizzazioni; 2) federazione tra un'organizzazione e un provider pubblico; e 3) federazione tra un'organizzazione e un provider di hosting di terze parti.

l'impostazione di una federazione diretta con altre organizzazioni richiede diverse attività. Per iniziare, è necessario configurare i server che eseguono il servizio Access Edge di Lync Server in modo da consentire la federazione. Inoltre, anche l'altra organizzazione deve abilitare la federazione; non è possibile stabilire una federazione, a meno che entrambe le parti non siano concordi nell'impostare una relazione.

Per stabilire una relazione federata potrebbe inoltre essere necessario gestire due elenchi relativi alla federazione, ovvero l'elenco dei domini consentiti e quello dei domini bloccati. L'elenco dei domini consentiti rappresenta le organizzazioni con le quali si è scelto di federarsi. Se un dominio è incluso in questo elenco, (in base alle impostazioni di configurazione) gli utenti saranno in grado di scambiare messaggi istantanei e informazioni sulla presenza con gli utenti che hanno gli account in tale dominio federato. Al contrario, l'elenco dei domini bloccati rappresenta i domini con i quali gli utenti non sono autorizzati a federarsi. Ad esempio, i messaggi inviati da un dominio bloccato verranno automaticamente rifiutati da Lync Server.

Se si desidera creare una nuova relazione di federazione, è possibile utilizzare il cmdlet **New-CsAllowedDomain** per aggiungere un dominio all'elenco dei domini consentiti.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **New-CsAllowedDomain** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsAllowedDomain"}

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
<td><p><em>Domain</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>FQDN (ad esempio, fabrikam.com) del dominio da aggiungere all'elenco dei domini consentiti. È possibile utilizzare i parametri Identity o Domain (ma non entrambi) per specificare il nome del dominio. Se si utilizza Identity, la proprietà Domain verrà impostata con lo stesso valore assegnato a Identity. Se si utilizza Domain, la proprietà Identity verrà impostata con lo stesso valore assegnato a Domain.</p>
<p>Si noti che Domains deve essere univoco: Se il dominio specificato esiste già nell'elenco dei domini bloccati o in quello dei domini consentiti, il comando avrà esito negativo.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nome di dominio completo (FQDN) del dominio da aggiungere all'elenco dei domini consentiti ad esempio, fabrikam.com. È anche possibile utilizzare il parametro Identity o Domain (ma non entrambi) per specificare il nome del dominio. Se si utilizza Identity, la proprietà Domain verrà impostata con lo stesso valore assegnato a Identity. Se si utilizza Domain, la proprietà Identity verrà impostata con lo stesso valore assegnato a Domain.</p>
<p>Si noti che l'identità deve essere univoca: Se il dominio specificato esiste già nell'elenco dei domini bloccati o in quello dei domini consentiti, il comando avrà esito negativo.</p></td>
</tr>
<tr class="odd">
<td><p><em>Comment</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Valore di stringa facoltativo che fornisce informazioni aggiuntive riguardo al dominio da aggiungere all'elenco dei domini consentiti. Ad esempio, potrebbe essere aggiunto un commento che fornisce le informazioni di contatto per il dominio federato.</p></td>
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
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>MarkForMonitoring</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se la connessione di federazione il proprio dominio ed il dominio remoto viene monitorata da Monitoring Server o non viene monitorata. Per impostazione predefinita, MarkForMonitoring è impostata su False, significa che la connessione non verrà monitorata.</p>
<p>Questa proprietà verrà ignorata se non è stato distribuito Monitoring Server.</p></td>
</tr>
<tr class="even">
<td><p><em>ProxyFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome completo di dominio (ad esempio, proxy-server.fabrikam.com) del server proxy SIP distribuito nel dominio che deve essere aggiunto all'elenco dei domini consentiti. Questa proprietà è facoltativa: se non viene specificato verranno utilizzate procedure di individuazione DNS SRV per determinare la località del server proxy SIP.</p></td>
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

Nessuno. Il cmdlet **New-CsAllowedDomain** non accetta input inviato tramite pipe.

## Tipi restituiti

Consente di creare istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.AllowedDomain.

## Vedere anche

#### Ulteriori risorse

[Get-CsAllowedDomain](get-csalloweddomain.md)  
[Remove-CsAllowedDomain](remove-csalloweddomain.md)  
[Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)  
[Set-CsAllowedDomain](set-csalloweddomain.md)

