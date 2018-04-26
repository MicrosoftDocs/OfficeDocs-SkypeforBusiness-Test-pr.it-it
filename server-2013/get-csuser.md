---
title: Get-CsUser
TOCTitle: Get-CsUser
ms:assetid: 06f36c53-3a5e-4e79-b4f2-8c1aa7e6bf71
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398125(v=OCS.15)
ms:contentKeyID: 49299573
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsUser

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce le informazioni su tutti gli utenti dell'organizzazione abilitati per Lync Server o una versione precedente del software, ad esempio Microsoft Office Communications Server 2007 R2. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsUser [-Identity <UserIdParameter>] [-Credential <PSCredential>] [-DomainController <Fqdn>] [-Filter <String>] [-LdapFilter <String>] [-OnLyncServer <SwitchParameter>] [-OnOfficeCommunicationServer <SwitchParameter>] [-OU <OUIdParameter>] [-ResultSize <Unlimited>] [-UnassignedUser <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio precedente viene chiamato il cmdlet **Get-CsUser** senza parametri per restituire una raccolta di tutti gli utenti del dominio abilitati per Lync Server o Office Communications Server.

    Get-CsUser

## ESEMPIO 2

Nell'esempio 2 il cmdlet **Get-CsUser** restituisce una raccolta di tutti gli utenti del dominio abilitati per Lync Server o Office Communications Server. Per impostazione predefinita, il cmdlet **Get-CsUser** restituisce numerose proprietà e valori di proprietà, molti dei quali non saranno utili in una determinata situazione. In questo esempio i dati recuperati vengono pertanto inviati tramite pipe al cmdlet **Format-Table**. Il cmdlet **Format-Table** utilizza quindi il parametro Property per selezionare le proprietà DisplayName, SipAddress ed EnterpriseVoiceEnabled e visualizzarle insieme ai relativi valori in una tabella.

    Get-CsUser | Format-Table -Property DisplayName, SipAddress, EnterpriseVoiceEnabled -AutoSize

## ESEMPIO 3

Nell'Esempio 3, il parametro Identity viene utilizzato per ottenere solo l'account utente con l'identità (in questo caso, DisplayName) Pilar Ackerman.

    Get-CsUser -Identity "Pilar Ackerman"

## ESEMPIO 4

Nell'esempio 4 viene utilizzato il carattere jolly asterisco (\*) quando si specifica l'identità utente. In questo caso, il cmdlet **Get-CsUser** restituisce tutti gli utenti la cui identità inizia con il valore stringa "Pilar".

    Get-CsUser -Identity "Pilar*"

## ESEMPIO 5

Il comando riportato nell'esempio 5 restituisce una raccolta di utenti a cui non è assegnato un criterio vocale per utente. A tale scopo, il comando utilizza il parametro Filter seguito dal filtro VoicePolicy -eq "$Null. Quando si creano i filtri da utilizzare con il cmdlet **Get-CsUser**, è necessario specificare il nome della proprietà (VoicePolicy) seguito dall'operatore di confronto (in questo caso "eq", che indica "uguale a"). Subito dopo l'operatore di confronto deve comparire il valore per cui si esegue la verifica. In questo esempio quel valore è $Null, una variabile dell'interfaccia della riga di comando Windows PowerShell che rappresenta un valore Null.

Per restituire una raccolta di utenti ai quali è assegnato un criterio vocale, utilizzare questo comando:

Get-CsUser -Filter {VoicePolicy -ne $Null}

    Get-CsUser -Filter {VoicePolicy -eq $Null}

## ESEMPIO 6

Nell'esempio 6 viene utilizzato il parametro LdapFilter per ottenere solo i dati relativi agli utenti che lavorano nel reparto Finance. Questo risultato viene ottenuto utilizzando il filtro LDAP con valore "Department=Finance".

    Get-CsUser -LdapFilter "Department=Finance"

## ESEMPIO 7

Nell'esempio 7 viene illustrato l'utilizzo di una query AND insieme al parametro LdapFilter. Questa query (che utilizza il carattere "&" per indicare una query AND) indica due condizioni: "Department=Finance" e "Title=Manager". Per fare in modo che questa query restituisca un account utente, devono essere soddisfatte entrambe le condizioni: l'utente deve lavorare nel reparto Finance e deve possedere la qualifica Manager.

    Get-CsUser -LdapFilter "&(Department=Finance)(Title=Manager)"

## ESEMPIO 8

Nel comando riportato nell'esempio 8 viene utilizzata una query OR (indicata dalla barra verticale "|") con il parametro LdapFilter. Nella query AND riportata nell'esempio 7 devono essere soddisfatte entrambe le condizioni per restituire un account utente. Con una query OR deve essere soddisfatta solo una condizione per restituire l'account. In questo caso, l'account utente verrà restituito se l'utente possiede la qualifica Supervisor o Manager.

    Get-CsUser -LdapFilter "|(Title=Supervisor)(Title=Manager)"

## ESEMPIO 9

Nell'Esempio 9 vengono restituite le informazioni sull'account di tutti gli utenti nell'unità organizzativa Finance.

    Get-CsUser -OU "ou=Finance,ou=North America,dc=litwareinc,dc=com"

## ESEMPIO 10

Nell'esempio 10 viene restituita una raccolta di tutti gli utenti abilitati per Lync Server o Office Communications Server ma non attualmente assegnati a un pool di registrazione.

    Get-CsUser -UnassignedUser

## Descrizione dettagliata

Utilizzati insieme, i cmdlet **Get-CsAdUser** e **Get-CsUser** consentono di restituire informazioni dettagliate su tutti gli account utente di Active Directory. Il cmdlet **Get-CsAdUser** restituisce informazioni su tutti gli account utente, inclusi gli utenti abilitati per Lync Server o Office Communications Server e gli utenti non abilitati per Lync Server o Office Communications Server. Il cmdlet **Get-CsUser** invece restituisce informazioni solo sugli utenti i cui account sono stati abilitati per Lync Server o Office Communications Server.

Sebbene esista una certa sovrapposizione tra **Get-CsUser** e **Get-CsAdUser**, i due cmdlet differiscono nel tipo di informazioni restituite. Il cmdlet **Get-CsUser** di solito restituisce valori per gli attributi di Active Directory correlati specificamente a Lync Server. Ad esempio, il cmdlet **Get-CsUser** restituisce informazioni quali i criteri di Lync Server assegnati a un utente, l'URI (Uniform Resource Identifier) di linea assegnato a quell'utente e i dettagli relativi al fatto che l'utente sia stato abilitato o meno per VoIP aziendale. Questi attributi non faranno parte di un account utente se tale utente non è stato abilitato per Lync Server.

Al contrario, il cmdlet **Get-CsAdUser** restituisce valori generici per gli attributi di Active Directory, ovvero attributi che fanno parte dell'account utente di Active Directory di base e che sono presenti anche se l'utente non è stato abilitato per Lync Server. Ad esempio, il cmdlet **Get-CsAdUser** restituisce informazioni sull'utente quali il reparto e l'organizzazione per cui lavora, nonché la qualifica, il numero di telefono e l'indirizzo dell'ufficio.

Per visualizzare un elenco completo dei valori degli attributi restituiti dal cmdlet **Get-CsUser**, al prompt dei comandi di Windows PowerShell digitare il comando seguente:

Get-CsUser | Get-Member

Il cmdlet **Get-CsUser** consente di filtrare in diversi modi la raccolta di utenti restituita dal cmdlet. Se ad esempio non si desidera ottenere tutti gli account utente di Lync Server, è possibile applicare il parametro facoltativo Filter o LdapFilter. Questi parametri si escludono reciprocamente, pertanto se si utilizza Filter in un comando, non è possibile utilizzare LdapFilter nello stesso comando e viceversa. Il parametro Filter restituisce solo i dati relativi agli utenti che soddisfano i criteri di Lync Server specificati, ad esempio solo i dati degli utenti i cui account si trovano nel pool di registrazione specificato o solo i dati degli utenti abilitati per VoIP aziendale. Il parametro LdapFilter consente di ottenere solo i dati degli utenti che soddisfano altri criteri basati su Active Directory, ad esempio i dati degli utenti che lavorano in una provincia specifica, degli utenti che possiedono o meno un cercapersone oppure degli utenti con un determinato titolo professionale.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsUser** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins, RTCUniversalReadOnlyAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsUser\\b"}

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
<td><p>Consente di eseguire il cmdlet <strong>Get-CsUser</strong> utilizzando credenziali alternative. Può essere obbligatorio se l'account utilizzato per accedere a Windows non dispone dei privilegi necessari, richiesti per utilizzare gli oggetti utente.</p>
<p>Per utilizzare il parametro Credential, è necessario creare innanzitutto un oggetto PSCredential utilizzando il cmdlet <strong>Get-Credential</strong>. Per informazioni dettagliate, vedere nella Guida l'argomento relativo al cmdlet <strong>Get-Credential</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente di eseguire la connessione al controller di dominio specificato per recuperare le informazioni sull'utente. Per la connessione a un controller di dominio specifico, includere il parametro DomainController seguito dal nome di dominio completo (ad esempio, atl-cs-001.litwareinc.com).</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti applicando un filtro in base ad attributi specifici di Lync Server. Ad esempio, è possibile limitare i dati restituiti agli utenti a cui è stato assegnato un criterio vocale specifico o agli utenti a cui non è stato assegnato un criterio vocale specifico.</p>
<p>Il parametro Filter utilizza la stessa sintassi di filtro Windows PowerShell impiegata dal cmdlet <strong>Where-Object</strong>. Ad esempio, un filtro che restituisce solo utenti abilitati per VoIP aziendale sarà simile a quello seguente, dove EnterpriseVoiceEnabled indica l'attributo di Servizi di dominio Active Directory, -eq indica l'operatore di confronto (uguale a) e $True (una variabile incorporata di Windows PowerShell) indica il valore del filtro:</p>
<p>{EnterpriseVoiceEnabled -eq $True}</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Indica l'identità dell'account utente da recuperare. Le identità dell'utente possono essere specificate utilizzando uno dei seguenti quattro formati: 1) l'indirizzo SIP dell'utente; 2) il nome dell'entità utente (UPN); 3) il nome del dominio e il nome di accesso dell'utente nella forma dominio\accesso (ad esempio, litwareinc\kenmyer); 4) il nome visualizzato Active Directory dell'utente (ad esempio, Ken Myer). È anche possibile fare riferimento a un account utente utilizzando il nome distinto Active Directory dell'utente.</p>
<p>È possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il nome visualizzato come identità (Identity) utente. Ad esempio, il parametro Identity &quot;* Smith&quot; restituirà tutti gli utenti con un nome visualizzato che termina con &quot; Smith&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>LdapFilter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di limitare i dati restituiti applicando un filtro in base ad attributi generici di Active Directory (ovvero attributi non specifici di Lync Server). Ad esempio, è possibile limitare i dati restituiti agli utenti che lavorano in un reparto specifico o agli utenti che possiedono una qualifica specifica.</p>
<p>Il parametro LdapFilter utilizza il linguaggio di query LDAP per la creazione dei filtri. Ad esempio, un filtro che restituisce solo gli utenti che lavorano a Redmond sarà simile al seguente: &quot;l=Redmond&quot;, dove &quot;l&quot; (L minuscola) rappresenta l'attributo di Active Directory (località), &quot;=&quot; rappresenta l'operatore di confronto (uguale a) e &quot;Redmond&quot; rappresenta il valore di filtro.</p></td>
</tr>
<tr class="even">
<td><p><em>OnLyncServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce una raccolta di utenti ospitati in Lync Server. Gli utenti i cui account sono associati alle versioni precedenti del software non vengono restituiti quando si utilizza questo parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>OnOfficeCommunicationServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce una raccolta di utenti ospitata su una versione precedente di Lync Server (ad esempio, Office Communications Server 2007 R2). Gli utenti i cui account sono associati alla versione corrente del software non verranno restituiti quando si utilizza questo parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>Consente di ottenere solo gli account utente di una specifica unità organizzativa o di un contenitore. Il parametro OU restituisce i dati dell'unità organizzativa specificata e delle unità organizzative figlio. Ad esempio, se l'unità organizzativa Finance contiene due unità organizzative figlio, AccountsPayable e AccountsReceivable, saranno restituiti gli utenti di tutte e tre le unità organizzative.</p>
<p>Per specificare una OU occorre utilizzare il nome distinto (DN) del contenitore, ad esempio: -OU &quot;OU=Finance,dc=litwareinc,dc=com&quot;. Per restituire account utente da un contenitore Users, utilizzare la seguente sintassi: -OU &quot;cn=Users,dc=litwareinc,dc=com&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>ResultSize</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.ADConnect.Core.Unlimited</p></td>
<td><p>Consente di limitare il numero di record restituiti dal cmdlet. Ad esempio, per restituire sette utenti (indipendentemente dal numero di utenti nella foresta), includere il parametro -ResultSize e impostarne il valore su 7. Non c'è modo di stabilire quali sette utenti saranno restituiti.</p>
<p>ResultSize può essere impostato su qualsiasi numero intero compreso tra 0 e 2147483647. Se impostato su 0, il comando verrà eseguito ma i dati non verranno restituiti. Se si imposta ResultSize su 7, ma la foresta contiene solo tre utenti, il comando restituirà i tre utenti e verrà completato senza errori.</p></td>
</tr>
<tr class="even">
<td><p><em>UnassignedUser</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di ottenere una raccolta di tutti gli utenti abilitati per Lync Server ma non assegnati al momento ad un pool di registrazione. Agli utenti non è consentito accedere a Lync Server a meno che non vengano assegnati ad un pool di registrazione.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Stringa. Il cmdlet **Get-CsUser** accetta un valore stringa da pipeline che rappresenta l'identità di un account utente abilitato per Lync Server.

## Tipi restituiti

Il cmdlet **Get-CsUser** restituisce istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser.

## Vedere anche

#### Ulteriori risorse

[Disable-CsUser](disable-csuser.md)  
[Enable-CsUser](enable-csuser.md)  
[Get-CsAdUser](get-csaduser.md)  
[Move-CsUser](move-csuser.md)  
[Set-CsUser](set-csuser.md)

