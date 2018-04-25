---
title: Get-CsTenant
TOCTitle: Get-CsTenant
ms:assetid: 7b642117-5ca7-4a5b-bca7-16b0ae694ae2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994044(v=OCS.15)
ms:contentKeyID: 52062192
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTenant

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui tenant di Skype for Business online configurati per l'uso nell'organizzazione. I tenant rappresentano gruppi di utenti online. In molti casi potrebbe essere sufficiente un singolo tenant. Se gruppi di utenti diversi hanno esigente di gestione differenti, tuttavia, Skype for Business online supporta la configurazione di più tenant per una singola organizzazione.

Il cmdlet Get-CsTenant può essere usato solo con Skype for Business online.

## Sintassi

    Get-CsTenant [[-Identity] <OUIdParameter>] [-Filter <String>] [-ResultSize <Unlimited`1>] [-Verbose]

## Esempi

## Esempio 1

Il comando mostrato nell'esempio 1 restituisce informazioni su tutti i tenant configurati per l'uso nell'organizzazione.

    Get-CsTenant

## Esempio 2

Nell'esempio 2 vengono restituite informazioni per un singolo tenant, ovvero il tenant con Identity "bf19b7db-6960-41e5-a139-2aa373474354".

    Get-CsTenant -Identity "bf19b7db-6960-41e5-a139-2aa373474354"

## Esempio 3

Il comando precedente illustra un modo alternativo per restituire informazioni per un singolo tenant. In questo esempio si ottiene questo risultato includendo il parametro Filter e il valore di filtro {DisplayName –eq "Fabrikam"}. Tale sintassi restituisce solo le informazioni relative al tenant con nome visualizzato Fabrikam.

    Get-CsTenant -Filter {DisplayName -eq "Fabrikam"}

## Esempio 4

Il comando illustrato nell'esempio 4 restituisce informazioni per tutti i tenant con ServiceInstance uguale a "LitwareincCommunicationsOnline/San Antonio". A tale scopo, il comando include il parametro Filter e il valore di filtro {ServiceInstance -eq "LitwareincCommunicationsOnline/San Antonio"}. Tale valore di filtro limita i dati restituiti ai tenant con la proprietà ServiceInstance uguale a (-eq) "LitwareincCommunicationsOnline/San Antonio".

    Get-CsTenant -Filter {ServiceInstance -eq "LitwareincCommunicationsOnline/San Antonio"}

## Esempio 5

L'esempio 5 restituisce informazioni per tutti i tenant con nome visualizzato di paese o area geografica uguale a Australia. Questo risultato si ottiene usando il parametro Filter e il valore di filtro {CountryOrRegionDisplayName -eq "Australia"}.

    Get-CsTenant -Filter {CountryOrRegionDisplayName -eq "Australia"}

## Descrizione dettagliata

In Skype for Business online i tenant rappresentano gruppi di utenti con account ospitati nel servizio. Per molte organizzazioni sarà sufficiente un singolo tenant per ospitare tutti gli account utente. La gestione di Skype for Business online, tuttavia, viene spesso eseguita in base ai singoli tenant, in modo che tutti gli utenti nello stesso tenant usino gli stessi criteri vocali, le stesse impostazioni di configurazione della federazione e così via. Se occorre gestire diversamente alcuni utenti rispetto ad altri, è possibile prendere in considerazione l'uso di più tenant, ognuno con una raccolta specifica di criteri e impostazioni.

Indipendentemente dal numero di tenant definiti, è possibile restituire informazioni sui tenant tramite il cmdlet **Get-CsTenant**.

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
<td><p>Consente di restituire dati tramite gli attributi di Active Directory e senza dover specificare il nome distinto completo di Active Directory. Per recuperare un tenant in base al nome visualizzato, ad esempio, usare una sintassi simile alla seguente:</p>
<p>Get-CsTenant –Filter {DisplayName –eq &quot;FabrikamTenant&quot;}</p>
<p>Per restituire tutti i tenant che usano un dominio Fabrikam, usa la sintassi seguente:</p>
<p>Get-CsTenant –Filter {Domains –like &quot;*fabrikam*&quot;}</p>
<p>Il parametro Filter usa la stessa sintassi di filtro di Windows PowerShell impiegata dal cmdlet Where-Object.</p>
<p>Non è possibile utilizzare i parametri Identity e Filter nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Nome distinto di Active Directory del tenant. Ad esempio:</p>
<p>-Identity &quot;OU=bf19b7db-6960-41e5-a139-2aa373474354,OU=OCS Tenants,dc=litwareinc,dc=com&quot;</p>
<p>Se non si includono i parametri Identity o Filter, il cmdlet <strong>Get-CsTenant</strong> restituirà informazioni su tutti i tenant.</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited`1</p></td>
<td><p>Consente di limitare il numero di record restituiti dal cmdlet. Per restituire ad esempio sette tenant (indipendentemente dal numero di tenant presenti nella foresta), includere il parametro ResultSize e impostarne il valore su 7. Non è possibile stabilire quali dei sette utenti verranno restituiti.</p>
<p>La dimensione del risultato può essere impostata su qualsiasi numero intero compreso tra 0 e 2147483647 (compresi). Se l'impostazione è 0 il comando viene eseguito ma non restituisce dati. Se si imposta ResultSize su 7 ma nella foresta sono contenuti solo tre tenant, il comando restituirà i tre tenant e quindi verrà completato senza errori.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Il cmdlet **Get-CsTenant** accetta istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.TenantObject inviate tramite pipeline oltre a valori stringa che rappresentano l'identità di un tenant di Skype for Business online (ad esempio "OU=bf19b7db-6960-41e5-a139-2aa373474354,OU=OCS Tenants,dc=vdomain,dc=com").

## Tipi restituiti

Il cmdlet **Get-CsTenant** restituisce istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.TenantObject.

## Vedere anche

#### Ulteriori risorse

[Get-CsOnlineUser](get-csonlineuser.md)

