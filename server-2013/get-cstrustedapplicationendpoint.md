---
title: Get-CsTrustedApplicationEndpoint
TOCTitle: Get-CsTrustedApplicationEndpoint
ms:assetid: f66ac464-31ef-4aa3-9b79-f9e67ebc1475
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413035(v=OCS.15)
ms:contentKeyID: 49302501
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsTrustedApplicationEndpoint

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera le informazioni su uno o più endpoint di applicazioni attendibili. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsTrustedApplicationEndpoint [-Identity <UserIdParameter>] [-ApplicationId <String>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>] [-TrustedApplicationPoolFqdn <Fqdn>]

## Esempi

## ESEMPIO 1

In questo esempio vengono recuperate le informazioni su tutti gli endpoint di applicazioni attendibili definiti all'interno della distribuzione di Lync Server.

    Get-CsTrustedApplicationEndpoint

## ESEMPIO 2

Nell'esempio 2 vengono recuperate le informazioni sul contatto endpoint applicazione con indirizzo SIP endpoint1@litwareinc.com. Il prefisso sip: è obbligatorio quando l'indirizzo SIP viene utilizzato come parametro Identity.

    Get-CsTrustedApplicationEndpoint -Identity "sip:endpoint1@litwareinc.com"

## ESEMPIO 3

Nell'esempio 3 vengono recuperati tutti gli endpoint di applicazioni attendibili che hanno la stringa "endpoint" in una posizione qualsiasi all'interno del nome visualizzato. A tale scopo, il comando utilizza il parametro Filter. Il valore del parametro applica un filtro per trovare oggetti endpoint che hanno un nome visualizzato (DisplayName) contenente (-like) la stringa endpoint (\*endpoint\* - i caratteri jolly indicano che la stringa endpoint può essere preceduta o seguita da qualsiasi carattere, ovvero l'endpoint può trovarsi in una posizione qualsiasi all'interno del nome visualizzato).

    Get-CsTrustedApplicationEndpoint -Filter {DisplayName -like "*endpoint*"}

## ESEMPIO 4

Nell'esempio 4 vengono restituiti tutti gli endpoint di applicazioni attendibili associati all'applicazione tapp2. A tale scopo, viene passato ID tapp2 al parametro ApplicationId. Non è stato fornito un nome di dominio completo (FQDN) del pool, pertanto se esiste un'applicazione con ID tapp2 in più di un pool, verranno recuperati gli endpoint per tutte le applicazioni. La parte successiva del comando invia tramite pipe l'oggetto o gli oggetti restituiti al cmdlet **Select-Object**, che visualizza solamente le proprietà SipAddress, DisplayName e OwnerUrn di tali oggetti.

    Get-CsTrustedApplicationEndpoint -ApplicationId tapp2 | Select-Object SipAddress, DisplayName, OwnerUrn

## Descrizione dettagliata

L'endpoint di applicazioni attendibili è un oggetto contatto di Active Directory che consente il routing delle chiamate verso un'applicazione attendibile. Questo cmdlet recupera uno o più oggetti contatto dell'endpoint esistenti in Servizi di dominio Active Directory.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Get-CsTrustedApplicationEndpoint** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsTrustedApplicationEndpoint"}

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
<td><p><em>ApplicationId</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>L'ID applicazione dell'applicazione attendibile per l'endpoint che si desidera recuperare.</p></td>
</tr>
<tr class="even">
<td><p><em>Credential</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>Le credenziali alternative da utilizzare per recuperare l'endpoint. Per recuperare un oggetto PSCredential è possibile chiamare il cmdlet <strong>Get-Credential</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente di specificare un controller di dominio. Se non è specificato alcun controller di dominio, verrà utilizzato il primo disponibile.</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti applicando un filtro in base ad attributi specifici per Lync Server. Ad esempio, è possibile limitare i dati restituiti ai contatti, i cui nomi visualizzati o indirizzi SIP corrispondono a un determinato modello di caratteri jolly.</p>
<p>Il parametro Filter utilizza la stessa sintassi di filtro Windows PowerShell impiegata dal cmdlet <strong>Where-Object</strong>. Ad esempio, un filtro che restituisce solamente i contatti abilitati per VoIP aziendale potrebbe essere simile al seguente: {EnterpriseVoiceEnabled -eq $True}, dove EnterpriseVoiceEnabled rappresenta l'attributo di Active Directory, -eq rappresenta l'operatore di confronto (uguale a) e $True (una variabile predefinita di Windows PowerShell) rappresenta il valore del filtro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>L'identità (nome distinto), l'indirizzo SIP o il nome visualizzato dell'endpoint applicazione da modificare.</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Il parametro OU in cui risiede l'endpoint.</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>Il numero massimo di record endpoint da recuperare.</p></td>
</tr>
<tr class="even">
<td><p><em>TrustedApplicationPoolFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Il nome di dominio completo (FQDN) del pool di applicazioni attendibili associato all'applicazione dell'endpoint che si desidera recuperare.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Stringa. Accetta un valore stringa inviato tramite pipe che rappresenta l'identità di un account utente.

## Tipi restituiti

Restituisce un oggetto di tipo Microsoft.Rtc.Management.ADConnect.Schema.OCSADApplicationContact.

## Vedere anche

#### Ulteriori risorse

[New-CsTrustedApplicationEndpoint](new-cstrustedapplicationendpoint.md)  
[Remove-CsTrustedApplicationEndpoint](remove-cstrustedapplicationendpoint.md)  
[Set-CsTrustedApplicationEndpoint](set-cstrustedapplicationendpoint.md)

