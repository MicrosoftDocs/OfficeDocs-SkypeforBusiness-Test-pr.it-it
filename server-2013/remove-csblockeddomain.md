---
title: Remove-CsBlockedDomain
TOCTitle: Remove-CsBlockedDomain
ms:assetid: 34485703-9e1d-47f9-9834-c2ba37249cd1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425832(v=OCS.15)
ms:contentKeyID: 49300125
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsBlockedDomain

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove un dominio dall'elenco dei domini bloccati per la federazione. Per definizione, agli utenti non è consentito utilizzare le applicazioni Lync Server per comunicare dal dominio bloccato. Non possono ad esempio utilizzare Lync per scambiare messaggi istantanei con chiunque disponga di un account SIP in un dominio presente in un elenco di domini bloccati. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsBlockedDomain -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 rimuove il dominio fabrikam.com dall'elenco di domini bloccati. A tale scopo, viene chiamato il cmdlet **Remove-CsBlockedDomain** e viene specificato il dominio con l'identità "fabrikam.com".

    Remove-CsBlockedDomain -Identity fabrikam.com

## ESEMPIO 2

Nell'esempio 2 tutti i domini la cui identità include il valore stringa "fabrikam" vengono rimossi dall'elenco di domini bloccati. A tale scopo, vengono utilizzati innanzitutto il cmdlet **Get-CsBlockedDomain** e il parametro Filter per restituire una raccolta di tutti i domini bloccati in cui la stringa "fabrikam" è inclusa in qualsiasi posizione all'interno del valore Identity, ad esempio fabrikam.com, fabrikam.org o us.fabrikam.net. La raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsBlockedDomain**, che elimina ogni elemento della raccolta dall'elenco dei domini bloccati.

    Get-CsBlockedDomain -Filter *fabrikam* | Remove-CsBlockedDomain 

## ESEMPIO 3

Il comando riportato nell'esempio 3 cancella del tutto l'elenco dei domini bloccati. A tale scopo, viene chiamato innanzitutto il cmdlet **Get-CsBlockedDomain** senza alcun parametro. Viene così restituita una raccolta di tutti i domini attualmente presenti nell'elenco dei domini bloccati. La raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsBlockedDomain**, che rimuove ogni elemento della raccolta dall'elenco dei domini bloccati. Come risultato l'elenco dei domini bloccati è vuoto.

    Get-CsBlockedDomain | Remove-CsBlockedDomain 

## Descrizione dettagliata

La federazione consente a due organizzazioni di instaurare una relazione di trust che facilita la comunicazione tra i due gruppi. Quando viene stabilita una federazione, gli utenti delle due organizzazioni possono inviarsi messaggi istantanei, sottoscrivere l'opzione di notifiche di presenza e comunicare in altri modi tra loro utilizzando applicazioni SIP come Lync. Lync Server supporta tre tipi di federazione: 1) federazione diretta tra la propria e un'altra organizzazione, 2) federazione tra la propria organizzazione e un provider pubblico e 3) federazione tra la propria organizzazione e un provider di hosting di terze parti.

L'impostazione di una federazione diretta con altre organizzazioni richiede diverse attività. Per iniziare, è necessario configurare i server che eseguono il servizio Access Edge di Lync Server in modo da consentire la federazione. Inoltre, anche l'altra organizzazione deve abilitare la federazione; non è possibile stabilire una federazione, a meno che entrambe le parti non siano concordi nell'impostare una relazione.

Per attuare una relazione federata, potrebbe inoltre essere necessario gestire due elenchi correlati alla federazione: l'elenco dei domini consentiti e l'elenco dei domini bloccati. L'elenco dei domini consentiti include le organizzazioni con le quali si è deciso di attuare la federazione. Se un dominio è presente nell'elenco dei domini consentiti, a seconda delle impostazioni di configurazione gli utenti dell'organizzazione possono scambiare messaggi istantanei e informazioni sulla presenza con gli utenti che dispongono di un account in tale dominio federato. Al contrario, l'elenco dei domini bloccati rappresenta i domini con i quali gli utenti non sono autorizzati ad attuare una federazione (ad esempio i messaggi inviati da un dominio bloccato verranno automaticamente rifiutati da Lync Server.

I messaggi ovviamente verranno rifiutati solo finché il dominio sarà contenuto nell'elenco dei domini bloccati. Se un dominio viene rimosso dall'elenco, sarà possibile stabilire con esso una relazione federata. Per abilitare la federazione con un dominio precedentemente non consentito, è necessario innanzitutto utilizzare il cmdlet **Remove-CsBlockedDomain** per rimuovere il dominio dall'elenco dei domini bloccati. Un dominio non può essere presente contemporaneamente in un elenco di domini consentiti e in un elenco di domini bloccati.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsBlockedDomain** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsBlockedDomain"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nome di dominio completo (FQDN) del dominio da rimuovere dall'elenco dei domini bloccati, ad esempio fabrikam.com. Non è possibile utilizzare i caratteri jolly per specificare il valore Identity di un dominio.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.BlockedDomain. Il cmdlet **Remove-CsBlockedDomain** accetta le istanze dell'oggetto dominio bloccato inviate tramite pipeline.

## Tipi restituiti

Elimina le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.BlockedDomain.

## Vedere anche

#### Ulteriori risorse

[Get-CsBlockedDomain](get-csblockeddomain.md)  
[New-CsBlockedDomain](new-csblockeddomain.md)  
[Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)  
[Set-CsBlockedDomain](set-csblockeddomain.md)

