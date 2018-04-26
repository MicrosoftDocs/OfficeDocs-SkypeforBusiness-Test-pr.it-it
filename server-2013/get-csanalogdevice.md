---
title: Get-CsAnalogDevice
TOCTitle: Get-CsAnalogDevice
ms:assetid: 92f56039-f112-45bb-8340-109b0837f828
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398748(v=OCS.15)
ms:contentKeyID: 49301347
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsAnalogDevice

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui dispositivi analogici che possono essere gestiti con Lync Server. Un dispositivo analogico è un telefono o un altro dispositivo connesso alla rete PSTN (Public Switched Telephone Network). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsAnalogDevice [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-LdapFilter <String>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 viene restituita una raccolta di tutti i dispositivi analogici attualmente configurati per l'utilizzo nell'organizzazione. Per ottenere questo risultato viene chiamato il cmdlet **Get-CsAnalogDevice** senza alcun parametro.

    Get-CsAnalogDevice

## ESEMPIO 2

Con l'esempio 2 vengono restituiti solo due valori di proprietà, DisplayName e LineUri, per tutti i dispositivi analogici nell'organizzazione. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsAnalogDevice** senza parametri per restituire tutti i valori delle proprietà per tutti i dispositivi analogici dell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Select-Object**, che seleziona e visualizza solo i valori per le proprietà DisplayName e LineUri.

    Get-CsAnalogDevice | Select-Object DisplayName, LineUri

## ESEMPIO 3

Con l'esempio 3 vengono restituite informazioni sul dispositivo analogico con nome visualizzato di Active Directory "Building 14 Receptionist". A tal fine, il comando chiama **Get-CsAnalogDevice** e il parametro Filter; il valore del filtro {DisplayName -eq "Building 14 Receptionist"} limita gli oggetti restituiti ai dispositivi analogici la cui proprietà DisplayName è uguale a "Building 14 Receptionist".

    Get-CsAnalogDevice -Filter {DisplayName -eq "Building 14 Receptionist"}

## ESEMPIO 4

Nell'esempio 4 vengono restituiti tutti i dispositivi analogici configurati per il gateway 192.168.0.240. A tale scopo, viene chiamato il cmdlet **Get-CsAnalogDevice** con il parametro Filter. Il valore di filtro "192.168.0.240" restituisce solo i dispositivi analogici la cui proprietà Gateway è uguale a 192.168.0.240.

    Get-CsAnalogDevice -Filter {Gateway -eq "192.168.0.240"}

## ESEMPIO 5

Con il comando mostrato nell'esempio 5 vengono restituite informazioni su tutti i dispositivi fax analogici dell'organizzazione. A tale scopo, il comando chiama il cmdlet **Get-CsAnalogDevice** con il parametro Filter. Il valore di filtro {AnalogFax -eq $True} restituisce solo gli apparecchi fax analogici la cui proprietà AnalogFax è uguale a True.

    Get-CsAnalogDevice -Filter {AnalogFax -eq $True}

## ESEMPIO 6

Con l'esempio 6 viene restituito un singolo dispositivo analogico: il dispositivo il cui LineUri (numero di telefono) è uguale a tel:+14255556001.

    Get-CsAnalogDevice -Filter {LineUri -eq "tel:+14255556001"}

## ESEMPIO 7

Con l'esempio 7 vengono restituiti tutti i dispositivi analogici con indicativo di località 425 e prefisso telefonico 555. A tale scopo, viene utilizzato il cmdlet **Get-CsAnalogDevice** con il parametro Filter. Il valore di filtro {LineUri -like "tel:+1425555\*"} circoscrive i dati restituiti limitandoli ai dispositivi la cui proprietà LineUri inizia con i caratteri "tel:+1425555". Equivale a un numero di telefono che inizia con i caratteri 1425555, ad esempio 1-425-555-1298.

    Get-CsAnalogDevice -Filter {LineUri -like "tel:+1425555*"}

## ESEMPIO 8

Nell'esempio 8 viene restituita una raccolta di tutti i dispositivi analogici che dispongono di un oggetto contatto nell'unità organizzativa Telecommunications in Servizi di dominio Active Directory. A tale scopo, viene chiamato il cmdlet **Get-CsAnalogDevice** insieme al parametro OU. Il valore di parametro circoscrive gli oggetti restituiti limitandoli ai dispositivi analogici che dispongono di oggetti contatto nell'unità organizzativa con nome distinto ou=Telecommunications,dc=litwareinc,dc=com.

    Get-CsAnalogDevice -OU "ou=Telecommunications,dc=litwareinc,dc=com"

## ESEMPIO 9

Con il comando mostrato nell'esempio 9 viene illustrato come restituire una raccolta di dispositivi analogici e come assegnare un criterio vocale a ogni dispositivo della raccolta. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsAnalogDevice** senza alcun parametro per restituire una raccolta di tutti i dispositivi analogici configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Grant-CsVoicePolicy**, che assegna il criterio vocale AnalogVoicePolicy a ogni dispositivo della raccolta.

    Get-CsAnalogDevice | Grant-CsVoicePolicy -PolicyName "AnalogVoicePolicy"

## Descrizione dettagliata

I dispositivi analogici includono telefoni, apparecchi fax, modem e dispositivi TTY/TTD (Teletype/Telecommunication Devices for the Deaf) connessi alla rete PSTN (Public Switched Telephone Network). A differenza dei dispositivi che sfruttano VoIP aziendale (la soluzione VoIP offerta da Microsoft), i dispositivi analogici non trasmettono informazioni utilizzando pacchetti digitali; le informazioni vengono invece trasmesse utilizzando un segnale continuo. Questo segnale viene comunemente denominato segnale analogico; da qui l'espressione "dispositivi analogici".

Oltre ai telefoni analogici e ai telefoni che sfruttano VoIP aziendale, esiste un'altra classe di telefoni, ovvero i telefoni digitali non IP. Questi telefoni sono di proprietà del sistema PBX con cui vengono acquistati e non possono essere gestiti utilizzando i cmdlet di Lync Server.

Per consentire agli amministratori di gestire i dispositivi analogici per le organizzazioni, Lync Server consente di associare i dispositivi analogici agli oggetti contatto di Active Directory. Dopo aver associato un dispositivo a un oggetto contatto, è possibile gestire il dispositivo analogico ad esempio assegnando criteri e dial plan al contatto.

Il cmdlet **Get-CsAnalogDevice** consente di recuperare informazioni sui dispositivi analogici configurati per l'utilizzo nell'organizzazione. Se si chiama il cmdlet **Get-CsAnalogDevice** senza parametri, verranno restituite informazioni su tutti i dispositivi analogici. I parametri facoltativi consentono di filtrare le informazioni in diversi modi. È ad esempio possibile restituire tutti i dispositivi che dispongono di oggetti contatto in una specifica unità organizzativa o tutti i dispositivi analogici situati in un edificio specifico.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Get-CsAnalogDevice** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Le autorizzazioni per l'esecuzione di questo cmdlet in siti specifici o unità organizzative di Active Directory specifiche possono essere assegnate utilizzando il cmdlet **Grant-CsOUPermission**. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsAnalogDevice"}

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
<td><p>Consente di eseguire il cmdlet <strong>Get-CsAnalogDevice</strong> utilizzando credenziali alternative. Può essere necessario se l'account utilizzato per accedere a Windows non dispone dei privilegi necessari richiesti per lavorare con gli oggetti contatto.</p>
<p>Per utilizzare il parametro Credential, è necessario utilizzare innanzitutto il cmdlet <strong>Get-Credential</strong> per creare un oggetto PSCredential. Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet <strong>Get-Credential</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente la connessione al controller di dominio specificato per recuperare le informazioni di contatto. Per connettersi a un controller di dominio particolare, includere il parametro DomainController seguito dal nome di dominio completo del computer, ad esempio atl-cs-001.litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti applicando un filtro in base ad attributi specifici di Lync Server. Ad esempio, è possibile limitare i dati restituiti agli oggetti contatto dei dispositivi analogici a cui è stato assegnato uno specifico criterio vocale o ai contatti a cui non è assegnato un criterio vocale specifico.</p>
<p>Il parametro Filter utilizza la stessa sintassi di filtro Windows PowerShell impiegata dal cmdlet <strong>Where-Object</strong>. Ad esempio, un filtro che restituisce solo i dispositivi fax potrebbe essere simile al seguente, in cui AnalogFax rappresenta l'attributo di Active Directory, -eq rappresenta l'operatore di confronto (uguale a) e $True (una variabile predefinita di Windows PowerShell) rappresenta il valore del filtro:</p>
<p>-Filter {AnalogFax -eq $True}</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Identificatore univoco per il dispositivo analogico. I dispositivi analogici vengono identificati utilizzando il nome distinto di Active Directory dell'oggetto contatto associato. Per impostazione predefinita i dispositivi analogici utilizzano un GUID (identificatore univoco globale) come nome comune; significa che in genere i dispositivi utilizzano un'identità simile alla seguente: CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com.</p></td>
</tr>
<tr class="odd">
<td><p><em>LdapFilter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti applicando un filtro in base ad attributi generici di Active Directory (ovvero attributi non specifici di Lync Server). Ad esempio, è possibile limitare i dati restituiti agli oggetti contatto assegnati a un reparto specifico o che si trovano in un determinato edificio.</p>
<p>Il parametro LdapFilter utilizza il linguaggio di query LDAP per la creazione dei filtri. Ad esempio, un filtro che restituisce solamente gli oggetti contatto che rappresentano dispositivi analogici nella città di Redmond potrebbe essere simile al seguente:</p>
<p>-LdapFilter &quot;l=Redmond&quot;</p>
<p>Nel filtro precedente, &quot;l&quot; rappresenta l'attributo di Active Directory (località), &quot;=&quot; rappresenta l'operatore di confronto (uguale a) e &quot;Redmond&quot; rappresenta il valore del filtro.</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Consente di restituire gli oggetti contatto da una specifica unità organizzativa di Active Directory. Vengono restituiti i dati dell'unità organizzativa specificata e delle unità organizzative figlio. Ad esempio, se l'unità organizzativa Finance contiene due unità organizzative figlio, AccountsPayable e AccountsReceivable, saranno restituite le informazioni sui dispositivi analogici di tutte e tre le unità organizzative.</p>
<p>Per specificare un'unità organizzativa occorre utilizzare il nome distinto del contenitore, ad esempio: -OU &quot;OU=Finance,dc=litwareinc,dc=com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>Consente di limitare il numero di record restituiti da un comando. Ad esempio, per restituire sette dispositivi analogici (indipendentemente dal numero di dispositivi analogici nella foresta), includere il parametro ResultSize e impostarne il valore su 7. Non c'è modo di stabilire quali sette telefoni saranno restituiti. Se si imposta ResultSize su 7 ma la foresta contiene solo tre dispositivi analogici, il comando restituisce tali tre dispositivi e viene completato senza errori.</p>
<p>La dimensione del risultato può essere impostata su qualsiasi numero intero compreso tra 0 e 2147483647 (compresi). Se l'impostazione è 0 il comando viene eseguito ma non restituisce dati.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Stringa. Il cmdlet **Get-CsAnalogDevice** accetta l'input da pipeline di un valore stringa che rappresenta l'identità del dispositivo analogico.

## Tipi restituiti

Il cmdlet **Get-CsAnalogDevice** restituisce istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADAnalogDeviceContact.

## Vedere anche

#### Ulteriori risorse

[Move-CsAnalogDevice](move-csanalogdevice.md)  
[New-CsAnalogDevice](new-csanalogdevice.md)  
[Remove-CsAnalogDevice](remove-csanalogdevice.md)  
[Set-CsAnalogDevice](set-csanalogdevice.md)

