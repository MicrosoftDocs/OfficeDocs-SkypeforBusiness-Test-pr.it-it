---
title: Set-CsBlockedDomain
TOCTitle: Set-CsBlockedDomain
ms:assetid: 03f9443c-4c99-4338-bbf0-7b2f40a30ea5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398090(v=OCS.15)
ms:contentKeyID: 49299528
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsBlockedDomain

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica la proprietà Comment per uno o più domini inclusi nell'elenco dei domini bloccati per la federazione. Per definizione, agli utenti non è consentito utilizzare le applicazioni di Lync Server per comunicare con utenti del dominio bloccato. Gli utenti non possono utilizzare ad esempio Lync per scambiare messaggi istantanei con altri utenti con account SIP in un dominio incluso nell'elenco dei domini bloccati. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsBlockedDomain [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsBlockedDomain [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Comment <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di modificare il commento (Comment) per il dominio bloccato con Identity "fabrikam.com". In questo esempio, viene incluso il parametro Comment con il valore "Block this domain pending legal review".

    Set-CsBlockedDomain -Identity fabrikam.com -Comment "Block this domain pending legal review."

## ESEMPIO 2

Nell'esempio 2 la proprietà Comment viene aggiornata per tutti i domini inclusi nell'elenco dei domini bloccati. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsBlockedDomain**, che restituisce una raccolta di tutti i domini attualmente inclusi nell'elenco dei domini bloccati. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsBlockedDomain**, che modifica la proprietà Comment di ogni dominio della raccolta.

    Get-CsBlockedDomain | Set-CsBlockedDomain -Comment "Block this domain pending legal review."

## ESEMPIO 3

Nell'esempio 3 un nuovo commento ("Block this domain pending legal review.") viene aggiunto a ogni dominio nell'elenco dei domini bloccati per il quale non è già stato configurato un valore per la proprietà Comment. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsBlockedDomain** per restituire una raccolta di tutti i domini attualmente inclusi nell'elenco dei domini bloccati. La raccolta così ottenuta viene quindi inviata tramite pipe al cmdlet **Where-Object** che seleziona solo i domini in cui la proprietà Comment è uguale a un valore Null. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsBlockedDomain**, che assegna lo stesso commento alla proprietà Comment di ogni dominio della raccolta filtrata.

    Get-CsBlockedDomain | Where-Object {$_.Comment -eq $Null} | Set-CsBlockedDomain -Comment "Block this domain pending legal review."

## Descrizione dettagliata

La federazione consente a due organizzazioni di instaurare una relazione di trust che facilita la comunicazione tra i due gruppi. Quando viene stabilita una federazione, gli utenti delle due organizzazioni possono inviarsi messaggi istantanei, sottoscrivere l'opzione di notifiche di presenza e comunicare in altri modi tra loro utilizzando applicazioni SIP come Lync Server. Lync Server supporta tre tipi di federazione: 1) federazione diretta tra la propria e un'altra organizzazione, 2) federazione tra la propria organizzazione e un provider pubblico e 3) federazione tra la propria organizzazione e un provider di hosting di terze parti.

La configurazione di una federazione con un'altra organizzazione implica diverse attività. Per iniziare si deve abilitare il proprio Access Edge Server per consentire la federazione. Inoltre, l'altra organizzazione deve a sua volta abilitare il processo federativo; la federazione non può essere instaurata se entrambe le parti non sono d'accordo.

Per impostare una relazione federata potrebbe inoltre essere necessario gestire due elenchi relativi alla federazione: l'elenco dei domini consentiti e quello dei domini bloccati. L'elenco dei domini consentiti rappresenta l'organizzazione con la quale si è scelto di attuare la federazione. Se un dominio è incluso in questo elenco, gli utenti, subordinatamente alle impostazioni di configurazione, saranno in grado di scambiare messaggi istantanei e informazioni sulla presenza con gli utenti il cui account è incluso nel dominio federato. Al contrario, l'elenco bloccato rappresenta i domini con i quali viene espressamente proibito agli utenti di attuare la federazione, ad esempio un messaggio inviato da un dominio bloccato viene automaticamente rifiutato da Lync Server.

La proprietà Comment, la sola proprietà di un dominio bloccato che è possibile modificare, viene utilizzata per archiviare ulteriori informazioni sul dominio in questione, ad esempio, il motivo per cui è stato bloccato, quando può essere eliminato dall'elenco dei domini bloccati, chi contattare per richiedere l'eliminazione del dominio dall'elenco dei domini bloccati e così via. Per modificare la proprietà Comment per uno qualsiasi dei domini bloccati, utilizzare il cmdlet **Set-CsBlockedDomain**.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsBlockedDomain** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsBlockedDomain"}

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
<td><p><em>Comment</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di fornire ulteriori informazioni sul dominio da modificare. Ad esempio, è possibile aggiungere un commento (Comment) che spiega perché il dominio è stato inserito nell'elenco dei domini bloccati.</p></td>
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
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Nome completo (FQDN) del dominio bloccato del quale viene modificata la proprietà Comment. Ad esempio: fabrikam.com</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto BlockedDomain</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.BlockedDomain. Il cmdlet **Set-CsBlockedDomain** accetta le istanze dell'oggetto dominio bloccato inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CsBlockedDomain** non restituisce alcun oggetto o valore. Il cmdlet invece configura le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Edge.BlockedDomain.

## Vedere anche

#### Ulteriori risorse

[Get-CsBlockedDomain](get-csblockeddomain.md)  
[New-CsBlockedDomain](new-csblockeddomain.md)  
[Remove-CsBlockedDomain](remove-csblockeddomain.md)  
[Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)

