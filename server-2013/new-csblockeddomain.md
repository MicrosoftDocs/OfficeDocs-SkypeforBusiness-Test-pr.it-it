---
title: New-CsBlockedDomain
TOCTitle: New-CsBlockedDomain
ms:assetid: c7b49baf-759b-485f-9391-58584b227fd5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398822(v=OCS.15)
ms:contentKeyID: 49301916
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsBlockedDomain

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Aggiunge un nuovo dominio all'elenco dei domini bloccati per la federazione. Per definizione, agli utenti non è consentito utilizzare le applicazioni Lync Server per comunicare dal dominio bloccato. Non possono ad esempio utilizzare Lync per scambiare messaggi istantanei con chiunque disponga di un account SIP in un dominio presente in un elenco di domini bloccati. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsBlockedDomain -Domain <String> <COMMON PARAMETERS>

    New-CsBlockedDomain -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Comment <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 il dominio fabrikam.com viene aggiunto all'elenco dei domini bloccati. A tale scopo, viene chiamato il cmdlet **New-CsBlockedDomain** insieme al parametro Identity, a cui viene assegnato il nome del dominio da bloccare. Viene incluso inoltre il parametro Comment per aggiungere un commento al dominio bloccato. Il comando avrà esito negativo se fabrikam.com compare già nell'elenco dei domini bloccati o nell'elenco dei domini consentiti.

    New-CsBlockedDomain -Identity "fabrikam.com" -Comment "Blocked per Ken Myer."

## ESEMPIO 2

Nell'esempio 2 viene illustrato come utilizzare il parametro InMemory per creare un nuovo dominio bloccato inizialmente esistente solo in memoria. Dopo aver modificato i valori di proprietà di questo dominio presente solo in memoria, è possibile chiamare il cmdlet **Set-CsBlockedDomain** per aggiungere il dominio all'elenco dei domini bloccati.

Per eseguire questa attività, nella prima riga del comando vengono utilizzati il cmdlet **New-CsBlockedDomain** e il parametro InMemory per creare un dominio bloccato con valore Identity fabrikam.com. Dopo la creazione, questo dominio virtuale viene archiviato nella variabile $x.

Nella seconda riga, viene modificata la proprietà Comment del dominio virtuale. Al termine, nella riga 3 viene utilizzato il cmdlet **Set-CsBlockedDomain** per aggiungere il dominio virtuale all'elenco dei domini bloccati. Senza la riga 3, il dominio virtuale esisterebbe solo in memoria e non verrebbe mai aggiunto all'elenco bloccato. Il dominio virtuale invece scomparirà non appena viene terminata la sessione di Windows PowerShell o viene eliminata la variabile $x.

    $x = New-CsBlockedDomain -Identity "fabrikam.com" -InMemory
    $x.Comment = "Blocked per Ken Myer."
    Set-CsBlockedDomain -Instance $x

## Descrizione dettagliata

La federazione è un mezzo per stabilire una relazione di trust tra due organizzazioni per agevolare la comunicazione tra i due gruppi. Una volta stabilita una federazione, gli utenti delle due organizzazioni possono scambiare messaggi istantanei, sottoscrivere l'opzione di notifiche di presenza e comunicare comunque tra loro utilizzando le applicazioni SIP, ad esempio Lync. Lync Server supporta tre tipi di federazione: 1) federazione diretta tra due organizzazioni; 2) federazione tra un'organizzazione e un provider pubblico; e 3) federazione tra un'organizzazione e un provider di hosting di terze parti.

L'impostazione di una federazione diretta con altre organizzazioni richiede diverse attività. Per iniziare, è necessario configurare i server che eseguono il servizio Access Edge di Lync Server in modo da consentire la federazione. Inoltre, anche l'altra organizzazione deve abilitare la federazione; non è possibile stabilire una federazione, a meno che entrambe le parti non siano concordi nell'impostare una relazione.

Per stabilire una relazione federata, potrebbe inoltre essere necessario gestire due elenchi correlati alla federazione: l'elenco consentito e l'elenco bloccato. L'elenco consentito contiene le organizzazioni con le quali si è deciso di stabilire la federazione; se un dominio è presente nell'elenco consentito, a seconda delle impostazioni di configurazione, gli utenti dell'organizzazione possono scambiare messaggi istantanei e informazioni sulla presenza con utenti che dispongono di un account in tale dominio federato. L'elenco dei domini bloccati invece rappresenta i domini con i quali è espressamente vietato agli utenti di stabilire una federazione. I messaggi provenienti da un dominio bloccato ad esempio verranno automaticamente rifiutati da Lync Server.

Il cmdlet **New-CsBlockedDomain** consente di aggiungere un dominio all'elenco dei domini bloccati.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsBlockedDomain** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsBlockedDomain"}

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
<td><p>FQDN (ad esempio fabrikam.com) del dominio da aggiungere all'elenco dei domini bloccati. Per specificare il nome di dominio, è possibile utilizzare il parametro Identity o Domain, ma non entrambi. Se si utilizza il parametro Identity, la proprietà Domain verrà impostata sullo stesso valore assegnato al parametro Identity. Se si utilizza il parametro Domain, la proprietà Identity verrà impostata sullo stesso valore assegnato al parametro Domain.</p>
<p>I domini devono essere univoci: se il dominio specificato esiste già nell'elenco dei domini bloccati o in quello dei domini consentiti, il comando avrà esito negativo.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nome di dominio completo (FQDN) del dominio da aggiungere all'elenco dei domini bloccati, ad esempio &quot;fabrikam.com&quot;. Per specificare il nome di dominio, è possibile utilizzare il parametro Identity o Domain, ma non entrambi. Se si utilizza il parametro Identity, la proprietà Domain verrà impostata sullo stesso valore assegnato al parametro Identity. Se si utilizza il parametro Domain, la proprietà Identity verrà impostata sullo stesso valore assegnato al parametro Domain.</p>
<p>Le identità devono essere univoche: se il dominio specificato esiste già nell'elenco dei domini bloccati o in quello dei domini consentiti, il comando avrà esito negativo.</p></td>
</tr>
<tr class="odd">
<td><p><em>Comment</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Valore stringa facoltativo che contiene informazioni aggiuntive sul dominio bloccato. Ad esempio, potrebbe essere opportuno aggiungere un Commento che spiega la ragione per cui il dominio è stato bloccato.</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsBlockedDomain** non accetta input inviato tramite pipeline.

## Tipi restituiti

Crea le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.BlockedDomain.

## Vedere anche

#### Ulteriori risorse

[Get-CsBlockedDomain](get-csblockeddomain.md)  
[Remove-CsBlockedDomain](remove-csblockeddomain.md)  
[Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)  
[Set-CsBlockedDomain](set-csblockeddomain.md)

