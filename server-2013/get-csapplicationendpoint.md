---
title: Get-CsApplicationEndpoint
TOCTitle: Get-CsApplicationEndpoint
ms:assetid: 820d3bbd-0348-4272-bdb3-c3d612d0836a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398655(v=OCS.15)
ms:contentKeyID: 49301163
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsApplicationEndpoint

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera gli endpoint per il Servizio applicazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsApplicationEndpoint [-Identity <UserIdParameter>] [-ApplicationId <String>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-OU <OUIdParameter>] [-PoolFqdn <Fqdn>] [-ResultSize <Unlimited>]

## Esempi

## ESEMPIO 1

In questo esempio vengono recuperate le informazioni su tutti gli endpoint applicazione definiti nella distribuzione di Lync Server.

    Get-CsApplicationEndpoint

## ESEMPIO 2

Nell'esempio 2 vengono recuperati tutti gli endpoint applicazione contenenti la stringa "endpoint" in qualsiasi posizione all'interno del relativo nome visualizzato. A tale scopo, nel comando viene utilizzato il parametro Filter. Il valore del parametro applica un filtro per trovare gli oggetti endpoint che hanno un nome visualizzato (DisplayName) contenente (-like) la stringa endpoint (\*endpoint\*). I caratteri jolly indicano che la stringa endpoint può essere preceduta o seguita da qualsiasi carattere, ovvero l'endpoint può trovarsi in una posizione qualsiasi all'interno del nome visualizzato.

    Get-CsApplicationEndpoint -Filter {DisplayName -like "*endpoint*"}

## ESEMPIO 3

Nell'esempio 3 vengono restituiti tutti gli endpoint associati all'applicazione urn:application:tapp2. A tale scopo, viene passato l'ID tapp2 al parametro ApplicationId. Non è stato fornito un nome di dominio completo (FQDN) del pool. Se pertanto esiste un'applicazione con l'ID tapp2 in più di un pool, verranno recuperati gli endpoint per tutte le applicazioni. La parte successiva del comando invia tramite pipe l'oggetto o gli oggetti restituiti al cmdlet **Select-Object**, che visualizza solo le proprietà Identity, SipAddress, DisplayName e OwnerUrn di questi oggetti.

    Get-CsApplicationEndpoint -ApplicationId tapp2 | Select-Object Identity, SipAddress, DisplayName, OwnerUrn

## Descrizione dettagliata

Questo cmdlet consente di recuperare uno o più contatti dell'applicazione da Servizi di dominio Active Directory. Questi oggetti sono archiviati in Active Directory, nel contenitore Application Contacts del servizio RTC.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Get-CsApplicationEndpoint** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsApplicationEndpoint"}

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
<td><p>L'ID applicazione dell'endpoint applicazione da recuperare. L'ID dell'applicazione è il valore della proprietà OwnerUrn dell'endpoint. Ad esempio, se la proprietà OwnerUrn assume il valore urn:application:Caa, l'ID dell'applicazione è urn:application:Caa. Tuttavia, è possibile immettere solo il suffisso, in questo caso Caa, per recuperare l'endpoint. Ad esempio: -ApplicationId Caa</p></td>
</tr>
<tr class="even">
<td><p><em>Credential</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>Credenziali alternative con cui eseguire l'operazione Get. Per recuperare un oggetto PSCredential è possibile chiamare il cmdlet <strong>Get-Credential</strong> di Windows PowerShell.</p></td>
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
<td><p>Consente di limitare i dati restituiti applicando un filtro in base ad attributi specifici per Lync Server. Ad esempio, è possibile limitare i dati restituiti ai contatti i cui nomi visualizzati o indirizzi SIP corrispondono a un determinato modello di caratteri jolly.</p>
<p>Il parametro Filter utilizza la stessa sintassi di filtro Windows PowerShell impiegata dal cmdlet <strong>Where-Object</strong>. Ad esempio, un filtro che restituisce solamente i contatti abilitati per VoIP aziendale potrebbe essere simile al seguente: {EnterpriseVoiceEnabled -eq $True}, dove EnterpriseVoiceEnabled rappresenta l'attributo di Active Directory, -eq rappresenta l'operatore di confronto (uguale a) e $True (una variabile predefinita di Windows PowerShell) rappresenta il valore del filtro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>L'identità, l'indirizzo SIP o il nome visualizzato dell'endpoint applicazione da recuperare. L'identità è costituita dal nome distinto dell'endpoint. Tipicamente contiene un GUID come parte del CN, ad esempio: CN={8811fefe-e0bb-4fab-ae39-7aaeddd423dc},CN=Application Contacts,CN=RTC Service,CN=Services,CN=Configuration,DC=Vdomain,DC=com.</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>L'unità organizzativa in cui risiede l'endpoint.</p></td>
</tr>
<tr class="odd">
<td><p><em>PoolFqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Il nome di dominio completo del pool su cui risiede l'endpoint applicazione.</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>Il numero massimo di record endpoint da recuperare.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Stringa. Accetta un valore stringa da pipeline che rappresenta l'identità dell'endpoint applicazione.

## Tipi restituiti

Recupera un oggetto di tipo Microsoft.Rtc.Management.ADConnect.Schema.OCSADApplicationContact.

## Vedere anche

#### Ulteriori risorse

[Move-CsApplicationEndpoint](move-csapplicationendpoint.md)

