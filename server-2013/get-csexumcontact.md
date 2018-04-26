---
title: Get-CsExUmContact
TOCTitle: Get-CsExUmContact
ms:assetid: 9c7b2afb-4d7f-4b5a-99dd-6f8978dd5728
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412725(v=OCS.15)
ms:contentKeyID: 49301452
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsExUmContact

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera uno o più oggetti contatto della Messaggistica unificata di Exchange ospitata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsExUmContact [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-LdapFilter <String>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>]

## Esempi

## ESEMPIO 1

In questo esempio vengono recuperati tutti i contatti di Messaggistica unificata di Exchange definiti in una distribuzione di Lync Server.

    Get-CsExUmContact

## ESEMPIO 2

Con questo esempio viene recuperato il contatto Messaggistica unificata di Exchange con indirizzo SIP sip:exum1@fabrikam.com

    Get-CsExUmContact -Identity sip:exum1@fabrikam.com

## ESEMPIO 3

In questo esempio viene utilizzato il parametro Filter per recuperare tutti i contatti di Messaggistica unificata di Exchange che non sono abilitati per Lync Server. A tale scopo, viene applicato un filtro alla proprietà Enabled per verificare se il relativo valore è uguale a (-eq) False ($False). I contatti restituiti da questo comando non saranno utilizzabili.

    Get-CsExUmContact -Filter {Enabled -eq $False}

## ESEMPIO 4

Con questo comando viene applicato un filtro basato sulla proprietà LineURI per recuperare tutti i contatti Messaggistica unificata di Exchange il cui LineURI inizia con tel:555. In altre parole, vengono recuperati tutti i contatti che iniziano con 555.

    Get-CsExUmContact -Filter {LineURI -like "tel:555*"}

## ESEMPIO 5

Con il comando in questo esempio viene utilizzato il parametro OU per recuperare tutti i contatti Messaggistica unificata di Exchange nell'unità organizzativa di Active Directory OU=ExUmContacts,DC=Vdomain,DC=com.

    Get-CsExUmContact -OU "OU=ExUmContacts,DC=Vdomain,DC=com"

## Descrizione dettagliata

Lync Server interagisce con la Messaggistica unificata di Exchange per offrire diverse funzionalità vocali, tra cui Operatore automatico e Accesso sottoscrittore. Quando la Messaggistica unificata di Exchange viene fornita come servizio ospitato (anziché locale), è necessario creare gli oggetti contatto utilizzando Windows PowerShell per applicare le funzionalità Operatore automatico e Accesso sottoscrittore. Questo cmdlet recupera uno o più di questi contatti.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsExUmContact** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsExUmContact"}

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
<td><p><em>Credential</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>Consente di eseguire il cmdlet utilizzando credenziali alternative. Può essere necessario se l'account utilizzato per accedere a Windows non dispone dei privilegi necessari richiesti per lavorare con gli oggetti contatto.</p>
<p>Per utilizzare il parametro Credential, è necessario innanzitutto creare un oggetto PSCredential utilizzando il cmdlet <strong>Get-Credential</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente di eseguire la connessione al controller di dominio specificato per recuperare le informazioni sul contatto. Per la connessione a uno specifico controller di dominio, includere il parametro DomainController seguito dal nome computer (ad esempio atl-mcs-001) o dal suo nome di dominio completo (ad esempio atl-mcs-001.litwareinc.com).</p>
<p>Tipo di dati completi: Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti applicando un filtro in base ad attributi specifici di Lync Server. Ad esempio, è possibile limitare i dati restituiti ai contatti i cui URI di linea iniziano con &quot;tel:555&quot;.</p>
<p>Il parametro Filter utilizza un sottoinsieme della sintassi di filtro Windows PowerShell impiegata dal cmdlet <strong>Where-Object</strong>. Ad esempio, un filtro che restituisce solamente i contatti abilitati per VoIP aziendale potrebbe essere simile al seguente: {EnterpriseVoiceEnabled -eq $True}, dove EnterpriseVoiceEnabled rappresenta l'attributo di Active Directory, -eq rappresenta l'operatore di confronto (uguale a) e $True (una variabile predefinita di Windows PowerShell) rappresenta il valore del filtro.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>L'identificatore univoco dell'oggetto contatto che si desidera recuperare. Le identità dei contatti possono essere specificate con uno dei quattro formati riportati di seguito: 1) l'indirizzo SIP del contatto; 2) l'UPN (User Principal Name) del contatto; 3) il nome di dominio e il nome di accesso del contatto, nella forma dominio\accesso (ad esempio litwareinc\davidegarghentini); 4) il nome visualizzato in Active Directory per il contatto (ad esempio Team Auto Attendant).</p>
<p>Tipo di dati completi: Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
</tr>
<tr class="odd">
<td><p><em>LdapFilter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti applicando un filtro in base ad attributi generici di Active Directory (ovvero attributi non specifici di Lync Server).</p>
<p>Il parametro LdapFilter utilizza il linguaggio delle query LDAP per creare i filtri.</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Consente di limitare le informazioni recuperate in modo da includere esclusivamente quelle di una specifica unità organizzativa di Active Directory. Vengono restituiti dati dell'unità organizzativa specificata e delle unità organizzative figlio.</p>
<p>Per specificare un'unità organizzativa occorre utilizzare il nome distinto del contenitore, ad esempio OU=ExUmContacts,dc=litwareinc,dc=com.</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>Consente di limitare il numero di record restituiti da un comando. Ad esempio, per ottenere solo sette contatti (indipendentemente dal numero di contatti nella foresta), includere il parametro ResultSize e impostarlo su 7. Si noti che non è possibile stabilire a priori quali sette contatti verranno restituiti. Se si imposta ResultSize su 7 ma la foresta contiene solo tre contatti, il comando restituisce tali tre contatti e viene completato senza errori.</p>
<p>La dimensione del risultato può essere impostata su qualsiasi numero intero compreso tra 0 e 2147483647 (compresi). Se l'impostazione è 0 il comando viene eseguito ma non restituisce dati.</p>
<p>Tipo di dati completi: Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Stringa. Accetta una stringa inviata tramite pipeline che rappresenta l'identità dell'oggetto contatto Messaggistica unificata di Exchange.

## Tipi restituiti

Restituisce un oggetto di tipo Microsoft.Rtc.Management.ADConnect.Schema.OCSADExUmContact.

## Vedere anche

#### Ulteriori risorse

[New-CsExUmContact](new-csexumcontact.md)  
[Remove-CsExUmContact](remove-csexumcontact.md)  
[Set-CsExUmContact](set-csexumcontact.md)  
[Move-CsExUmContact](move-csexumcontact.md)

