---
title: Get-CsDialInConferencingAccessNumber
TOCTitle: Get-CsDialInConferencingAccessNumber
ms:assetid: f2c78377-ad21-4a9f-bef9-e9ef97316c85
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413015(v=OCS.15)
ms:contentKeyID: 49302456
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsDialInConferencingAccessNumber

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce le informazioni relative a tutti i numeri di accesso alle conferenze telefoniche con accesso esterno configurati per l'utilizzo nell'organizzazione. Tali conferenze consentono agli utenti di utilizzare un "normale" telefono fisso o cellulare oppure un dispositivo sulla rete PSTN (Public Switched Telephone Network) per partecipare alla parte audio di una conferenza online. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsDialInConferencingAccessNumber [-Region <String>] <COMMON PARAMETERS>

    Get-CsDialInConferencingAccessNumber -EmptyRegion <SwitchParameter> <COMMON PARAMETERS>

    Get-CsDialInConferencingAccessNumber [-Identity <UserIdParameter>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 restituisce una raccolta di tutti numeri di accesso alle conferenze telefoniche con accesso esterno configurati per l'utilizzo nell'organizzazione. La chiamata al cmdlet **Get-CsDialInConferencingAccessNumber** senza ulteriori parametri restituirà sempre una raccolta di tutti i numeri di accesso alle conferenze telefoniche con accesso esterno disponibili.

    Get-CsDialInConferencingAccessNumber

## ESEMPIO 2

Nell'esempio 2 viene restituito il numero di accesso alle conferenze telefoniche con accesso esterno con il parametro Identity sip:RedmondDialIn@litwareinc.com. Poiché le identità devono essere univoche, il comando non restituirà mai più di un numero di accesso.

    Get-CsDialInConferencingAccessNumber -Identity sip:RedmondDialIn@litwareinc.com

## ESEMPIO 3

Nell'esempio 3 viene utilizzato il parametro Region per restituire tutti i numeri di accesso alle conferenze telefoniche con accesso esterno associati all'area Redmond. A tale scopo, viene chiamato il cmdlet **Get-CsDialInConferencingAccessNumber** con il parametro Region. Specificando "Redmond" come valore del parametro, il cmdlet **Get-CsDialInConferencingAccessNumber** restituirà tutti i numeri in cui "Redmond" risulta nell'elenco delle aree associate. Ad esempio, verrà restituito un numero di accesso per il quale nell'elenco risulta solo Redmond come area, così come un numero di accesso per il quale nell'elenco risulta sia Redmond che Portland.

    Get-CsDialInConferencingAccessNumber -Region "Redmond"

## ESEMPIO 4

Nell'esempio 4 vengono restituiti tutti i numeri di accesso alle conferenze telefoniche con accesso esterno non associati a un'area, ovvero la cui proprietà Regions è vuota.

    Get-CsDialInConferencingAccessNumber -Region $Null

## ESEMPIO 5

Il comando mostrato nell'esempio 5 restituisce tutti i numeri di accesso alle conferenze telefoniche con accesso esterno per l'area Redmond che hanno come ambito il sito USA, ovvero il sito con SiteId site:USA.

    Get-CsDialInConferencingAccessNumber -Region site:USA/Redmond

## ESEMPIO 6

Nell'esempio 6 viene utilizzato il parametro Filter per restituire una raccolta di tutti i numeri di accesso alle conferenze telefoniche con accesso esterno che includono il valore stringa "Seattle" in un punto qualsiasi del relativo parametro DisplayName. Il valore di filtro {DisplayName -like "\*Seattle\*"} limita i dati restituiti ai numeri di accesso in cui DisplayName include la parola "Seattle", ad esempio Numero di accesso di Seattle, Numero di accesso esterno per Seattle, Numero di accesso di Tacoma/Seattle e così via.

    Get-CsDialInConferencingAccessNumber -Filter {DisplayName -like "*Seattle*"}

## ESEMPIO 7

Nell'esempio 7 vengono restituiti tutti i numeri di accesso alle conferenze telefoniche con accesso esterno in cui l'Uri di linea inizia con tel:+1425. In questo modo vengono restituiti tutti i numeri di telefono degli Stati Uniti con indicativo di località 425. A tale scopo, viene chiamato il cmdlet **Get-CsDialInConferencingAccessNumber** con il parametro Filter. Il valore di filtro {LineUri -like "tel:+1425\*"} limita i dati restituiti agli Uri di linea che iniziano con il valore stringa "tel:+1425". Per restituire tutti i numeri di telefono per l'indicativo di località 425 o 206, utilizzare il seguente valore di filtro:

{LineUri -like "tel:+1425\*" -or LineUri -like "tel:+1206\*"}

    Get-CsDialInConferencingAccessNumber -Filter {LineUri -like "tel:+1425*"}

## ESEMPIO 8

Nell'esempio 8 viene restituita una raccolta di tutti i numeri di accesso alle conferenze telefoniche con accesso esterno in cui la lingua principale è impostata su Italiano. Per eseguire questa attività, viene innanzitutto chiamato il cmdlet **Get-CsDialInConferencingAccessNumber** per restituire una raccolta di tutti i numeri di accesso configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i numeri in cui la proprietà PrimaryLanguage è uguale all'italiano ("it-It").

    Get-CsDialInConferencingAccessNumber | Where-Object {$_.PrimaryLanguage -eq "it-IT"}

## ESEMPIO 9

Il comando mostrato nell'esempio 9 restituisce tutti i numeri di accesso alle conferenze telefoniche con accesso esterno in cui il francese è elencato come una delle lingue secondarie. Per eseguire questa attività, viene innanzitutto chiamato il cmdlet **Get-CsDialInConferencingAccessNumber** senza alcun parametro per restituire una raccolta completa dei numeri di accesso configurati per l'utilizzo nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i numeri in cui la proprietà SecondaryLanguages include una voce relativa al francese (fr-FR).

    Get-CsDialInConferencingAccessNumber  | Where-Object {$_.SecondaryLanguages -contains "fr-FR"}

## Descrizione dettagliata

Le conferenze telefoniche con accesso esterno consentono agli utenti di utilizzare qualsiasi tipo di telefono, ad esempio un apparecchio per linea terrestre standard, un telefono cellulare o un telefono VoIP (Voice over Internet Protocol), per partecipare alla parte audio di una conferenza online. In questo modo è possibile partecipare alla riunione anche non disponendo di un computer o di una connessione Internet. Gli utenti dispongono delle funzionalità audio complete: possono parlare con altri partecipanti e ascoltare tutto. Non saranno invece in grado di visualizzare diapositive condivise, trasmissioni video o altri elementi grafici.

Per offrire agli utenti le funzionalità di conferenza telefonica con accesso esterno, è necessario creare appositi numeri di accesso, ovvero i numeri di telefono che gli utenti possono comporre per la connessione a una riunione. I numeri di accesso alle conferenze telefoniche con accesso esterno vengono creati utilizzando il cmdlet **New-CsDialInConferencingAccessNumber**. Quando si crea un nuovo numero di accesso alle conferenze telefoniche con accesso esterno, si crea in realtà un nuovo oggetto contatto in Servizi di dominio Active Directory. L'oggetto contatto viene utilizzato per rappresentare il numero di accesso e tutte le relative proprietà. I numeri contatto possono essere recuperati mediante il cmdlet **Get-CsDialInConferencingAccessNumber**.

Se da Microsoft Office Communications Server 2007 sono stati importati numeri di accesso alle conferenze telefoniche con accesso esterno, sarà possibile recuperare anche tali numeri eseguendo il cmdlet **Get-CsDialInConferencingAccessNumber** e includendo il parametro Region. I numeri importati non verranno visualizzati se non si utilizza tale parametro. Verrà tuttavia visualizzato un messaggio di avviso insieme agli URI (Uniform Resource Identifier) dei numeri importati. Questa è semplicemente la modalità con cui vengono gestiti dal cmdlet i numeri di accesso alle conferenze telefoniche con accesso esterno importati.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsDialInConferencingAccessNumber** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsDialInConferencingAccessNumber"}

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
<td><p><em>EmptyRegion</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce informazioni sui dial plan associati a un'area non associata ad almeno un numero di accesso alle conferenze telefoniche con accesso esterno. Si supponga ad esempio che il dial plan Bellevue sia associato all'area Bellevue, ma che per tale area non sia stato configurato alcun numero di accesso. L'area Bellevue verrebbe pertanto considerata un'area vuota.</p>
<p>Questo parametro non può essere utilizzato con un altro parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>Credential</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSCredential</p></td>
<td><p>Consente di eseguire il cmdlet <strong>Get-CsDialInConferencingAccessNumber</strong> con credenziali alternative. Ciò potrebbe essere necessario se l'account utilizzato per accedere a Windows non dispone dei privilegi necessari per gestire gli oggetti contatto.</p>
<p>Per poter utilizzare il parametro Credential, è necessario innanzitutto creare un oggetto PSCredential mediante il cmdlet <strong>Get-Credential</strong>. Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet <strong>Get-Credential</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente la connessione al controller di dominio specificato per recuperare le informazioni di contatto. Per la connessione a un determinato controller di dominio, includere il parametro DomainController seguito dal nome computer (ad esempio, atl-mcs-001) o dal relativo nome di dominio completo (ad esempio, atl-mcs-001.litwareinc.com).</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti applicando un filtro in base ad attributi specifici per Lync Server. Ad esempio, è possibile limitare i dati restituiti ai numeri delle conferenze telefoniche con accesso esterno che presentano il valore stringa &quot;Redmond&quot; nel nome visualizzato o ai numeri verdi delle conferenze telefoniche con accesso esterno che utilizzano il prefisso 1-800.</p>
<p>Per il parametro Filter viene utilizzata la stessa sintassi di filtro di Windows PowerShell utilizzata dal cmdlet <strong>Where-Object</strong>. Ad esempio, un filtro che restituisce solo i numeri di accesso con prefisso 1-800 potrebbe risultare analogo al seguente: {LineUri -like &quot;tel:+1800*&quot;}, con LineUri che rappresenta l'attributo di Active Directory, -like che rappresenta l'operatore di confronto e &quot;tel:+1800*&quot; che rappresenta il valore di filtro.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>L'indirizzo SIP del numero di accesso alle conferenze telefoniche con accesso esterno (ovvero l'oggetto contatto che rappresenta tale numero) da recuperare. È necessario includere il prefisso &quot;sip:&quot; quando si specifica il valore Identity, ad esempio -Identity sip:RedmondDialIn@litwareinc.com.</p>
<p>Se questo parametro non è specificato, il cmdlet <strong>Get-CsDialInConferencingAccessNumber</strong> restituirà tutti i numeri di accesso alle conferenze telefoniche con accesso esterno configurati per l'utilizzo nell'organizzazione.</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Consente di restituire i numeri di accesso da una specifica unità organizzativa di Active Directory. Sono inclusi i dati dell'unità organizzativa specificata e delle relative unità organizzative figlio. Ad esempio, se l'unità organizzativa Finance dispone di due unità organizzative figlio, AccountsPayable e AccountsReceivable, verranno restituite le informazioni sui numeri di accesso di tutte e tre le unità organizzative.</p>
<p>Per specificare un'unità organizzativa occorre utilizzare il nome distinto del contenitore, ad esempio: -OU &quot;OU=Finance,dc=litwareinc,dc=com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>Region</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente la restituzione di tutti i numeri delle conferenze telefoniche con accesso esterno associati all'area dial plan specificata. Ad esempio, per restituire tutti i numeri di accesso per l'area nord-occidentale, utilizzare la sintassi seguente: -Region Northwest.</p>
<p>È inoltre possibile restituire i numeri di accesso che hanno come ambito un determinato sito oppure l'ambito globale includendo l'ambito nel valore del parametro. Ad esempio, per restituire i numeri di accesso per cui viene utilizzata l'area Northwest e che hanno come ambito il sito Redmond, utilizzare la seguente sintassi: -Region site:Redmond/Northwest. Si noti che, quando si fa riferimento all'ambito del sito, è necessario utilizzare la proprietà SiteId. È possibile recuperare i valori SiteId utilizzando il cmdlet <strong>Get-CsSite</strong>.</p>
<p>Per restituire un elenco dei numeri di accesso non associati a un dial plan, impostare su $Null il valore del parametro Region: -Region $Null.</p>
<p>Si noti che i numeri di accesso alle conferenze telefoniche con accesso esterno verranno restituiti in base all'ordine di priorità loro assegnato solo se viene specificato questo parametro. L'ordine di priorità corrisponde all'ordine in cui compaiono i numeri negli inviti alle riunioni e nella pagina Web per le conferenze telefoniche con accesso esterno. Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet <a href="set-csdialinconferencingaccessnumber.md">Set-CsDialInConferencingAccessNumber</a>.</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>Consente di limitare il numero di record restituiti da un comando. Ad esempio, per restituire solo sette numeri di accesso (indipendentemente da quanti sono i numeri di accesso disponibili nella foresta), è sufficiente includere il parametro ResultSize e impostare su 7 il relativo valore. Si noti che non è possibile stabilire a priori quali sette elementi verranno restituiti. Se si imposta ResultSize su 7 ma nella foresta sono presenti solo tre numeri di accesso, il comando restituirà i tre numeri e quindi verrà completato senza errori.</p>
<p>La dimensione del risultato può essere impostata su qualsiasi numero intero compreso tra 0 e 2147483647 (compresi). Se l'impostazione è 0 il comando viene eseguito ma non restituisce dati.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Stringa. Il cmdlet **Get-CsDialInConferencingAccessNumber** accetta un valore stringa che rappresenta l'identità del numero di accesso.

## Tipi restituiti

Il cmdlet **Get-CsDialInConferencingAccessNumber** restituisce istanze dell'oggetto Microsoft.Rtc.Management.Xds.AccessNumber.

## Vedere anche

#### Ulteriori risorse

[New-CsDialInConferencingAccessNumber](new-csdialinconferencingaccessnumber.md)  
[Remove-CsDialInConferencingAccessNumber](remove-csdialinconferencingaccessnumber.md)  
[Set-CsDialInConferencingAccessNumber](set-csdialinconferencingaccessnumber.md)

