---
title: Set-CsUser
TOCTitle: Set-CsUser
ms:assetid: 6c452df7-75c9-4d94-86bc-4990d718ffe9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398510(v=OCS.15)
ms:contentKeyID: 49300891
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUser

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica le proprietà di Lync Server per un account utente esistente. Le proprietà possono essere modificate solo per gli account abilitati per l'utilizzo con Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsUser -Identity <UserIdParameter> [-AcpInfo <MultiValuedProperty>] [-AudioVideoDisabled <$true | $false>] [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Enabled <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-HostedVoiceMail <$true | $false>] [-LineServerURI <String>] [-LineURI <String>] [-PassThru <SwitchParameter>] [-PrivateLine <String>] [-RemoteCallControlTelephonyEnabled <$true | $false>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene utilizzato il cmdlet **Set-CsUser** per modificare l'account utente con identità (Identity) Pilar Ackerman. In questo caso, l'account viene modificato per abilitare VoIP aziendale, l'implementazione Microsoft di VoIP. A tale scopo, si aggiunge il parametro EnterpriseVoiceEnabled e si imposta il valore del parametro su $True.

    Set-CsUser -Identity "Pilar Ackerman" -EnterpriseVoiceEnabled $True

## ESEMPIO 2

Nell'esempio 2 gli account di tutti gli utenti del reparto Finance vengono abilitati per VoIP aziendale. In questo comando viene utilizzato innanzitutto il cmdlet **Get-CsUser** insieme al parametro LdapFilter per restituire una raccolta di tutti gli utenti che lavorano nel reparto Finance. Tali informazioni vengono quindi inviate tramite pipe al cmdlet **Set-CsUser**, che abilita VoIP aziendale per ogni account della raccolta.

    Get-CsUser -LdapFilter "Department=Finance" | Set-CsUser -EnterpriseVoiceEnabled $True

## Descrizione dettagliata

Il cmdlet **Set-CsUser** consente di modificare gli attributi degli account utente relativi a Lync Server archiviati in Servizi di dominio Active Directory. È ad esempio possibile disabilitare o riabilitare un utente per Lync Server, abilitare o disabilitare un utente per le comunicazioni audio/video (A/V) o modificare i numeri della linea privata e dell'URI di linea dell'utente. Il cmdlet **Set-CsUser** può essere utilizzato solo per gli utenti che sono stati abilitati per Lync Server.

I soli attributi che possono essere modificati utilizzando il cmdlet **Set-CsUser** sono gli attributi relativi a Lync Server. Gli altri attributi dell'account utente, come la qualifica o il reparto dell'utente, non possono essere modificati utilizzando questo cmdlet. Tenere presente, tuttavia, che gli attributi di Lync Server devono essere modificati solo tramite il cmdlet Set-CsUser o il Pannello di controllo di Lync Server. Non provare a configurarli manualmente.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsUser** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsUser\\b"}

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
<td><p>UserIdParameter</p></td>
<td><p>Indica l'identità dell'account utente da modificare. Le identità dell'utente possono essere specificate utilizzando uno dei seguenti quattro formati: 1) l'indirizzo SIP dell'utente; 2) il nome dell'entità utente (UPN); 3) il nome del dominio e il nome di accesso dell'utente nella forma dominio\accesso (ad esempio, litwareinc\kenmyer); 4) il nome visualizzato Active Directory dell'utente (ad esempio, Ken Myer). Alle identità utente è anche possibile fare riferimento utilizzando il nome distinto Active Directory dell'utente.</p>
<p>È possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il nome visualizzato come identità utente. Ad esempio, il parametro Identity &quot;* Smith&quot; restituirà tutti gli utenti con un nome visualizzato che termina con &quot; Smith&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>AcpInfo</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>MultiValuedProperty</p></td>
<td><p>Consente di assegnare a un utente uno o più provider di servizi di audioconferenza di terze parti. Tuttavia, si raccomanda di utilizzare il cmdlet <strong>Set-UserAcp</strong> per assegnare provider di audioconferenza.</p></td>
</tr>
<tr class="odd">
<td><p><em>AudioVideoDisabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se all'utente è consentito effettuare chiamate audio/video (A/V) utilizzando Lync. Se si imposta il parametro su True, all'utente verranno applicate restrizioni significative nell'invio e nella ricezione di messaggi istantanei.</p>
<p>Non è possibile disabilitare le comunicazioni A/V se un utente è attualmente abilitato al controllo delle chiamate remote, VoIP aziendale e/o il soft routing IP-PBX (Internet Protocol private branch exchange).</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Fqdn</p></td>
<td><p>Consente di specificare un controller di dominio a cui effettuare la connessione per modificare un account utente. Se questo parametro non viene specificato, il cmdlet utilizzerà il primo controller di dominio disponibile.</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se l'utente è stato abilitato per Lync Server. Se questo valore viene impostato su False, l'utente non potrà più accedere a Lync Server; se il valore viene impostato su True vengono riabilitati i privilegi di accesso dell'utente.</p>
<p>Se si disabilita un account utilizzando il parametro Enabled, le informazioni associate a tale account, inclusi i criteri assegnati e l'eventuale abilitazione dell'utente per VoIP aziendale e/o il controllo delle chiamate remote, vengono mantenute. Se in seguito si riabilita l'account utilizzando il parametro Enabled, le informazioni sull'account associate vengono ripristinate. Questo comportamento è diverso dall'utilizzo del cmdlet <strong>Disable-CsUser</strong> per disabilitare un account utente. Quando si esegue il cmdlet <strong>Disable-CsUser</strong>, tutti i dati di Lync Server associati a tale account vengono eliminati.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se l'utente è stato abilitato per VoIP aziendale, l'implementazione Microsoft di VoIP (Voice over Internet Protocol). Con VoIP aziendale gli utenti possono effettuare telefonate via Internet senza utilizzare la rete telefonica standard.</p></td>
</tr>
<tr class="even">
<td><p><em>ExchangeArchivingPolicy</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>ExchangeArchivingPolicyOptionsEnum</p></td>
<td><p>Indica la posizione in cui vengono archiviate le sessioni di messaggistica istantanea dell'utente. I valori consentiti sono:</p>
<p>* Uninitialized</p>
<p>* UseLyncArchivingPolicy</p>
<p>* ArchivingToExchange</p>
<p>* NoArchiving</p></td>
</tr>
<tr class="odd">
<td><p><em>HostedVoiceMail</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Se si imposta questo parametro su True, viene abilitato il routing della segreteria telefonica di un utente a una versione ospitata di Microsoft Exchange Server. Inoltre, impostando questa opzione su True, si consente agli utenti di Lync di effettuare una chiamata direttamente alla segreteria telefonica di un altro utente.</p></td>
</tr>
<tr class="even">
<td><p><em>LineServerURI</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'URI del gateway telefonico di controllo delle chiamate remote assegnato all'utente. LineServerUri è l'URI gateway, preceduto da &quot;sip:&quot;. Ad esempio: sip:rccgateway@litwareinc.com</p></td>
</tr>
<tr class="odd">
<td><p><em>LineURI</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Numero telefonico assegnato all'utente. L'URI (Uniform Resource Identifier) di linea deve essere specificato utilizzando il formato E.164 e il prefisso &quot;TEL:&quot;. Ad esempio: TEL:+14255551297. Qualsiasi numero di interno deve essere aggiunto alla fine dell'URI di linea, ad esempio: TEL:+14255551297;ext=51297.</p>
<p>È importante notare che in Lync Server TEL:+14255551297 e TEL:+14255551297;int=51297 vengono trattati come due numeri diversi. Se si assegna a Ken Myer l'URI di linea TEL:+14255551297 e successivamente si tenta di assegnare a Pilar Ackerman l'URI di linea TEL:+14255551297;ext=51297, tale assegnazione avrà esito positivo. Il numero assegnato a Pilar Ackerman non verrà contrassegnato come numero duplicato. Ciò è dovuto al fatto che, a seconda della configurazione, i due numeri potrebbero effettivamente essere diversi. In alcune organizzazioni ad esempio se si compone 1-425-555-1297, la chiamata viene inoltrata all'Operatore automatico di Exchange. Al contrario, se si compone solo il numero di interno (51297) o se si utilizza Lync per comporre il numero 1-425-555-1297 interno 51297, la chiamata viene inoltrata direttamente all'utente.</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Consente di specificare attraverso la pipeline un oggetto utente che rappresenta l'utente di cui si sta modificando l'account. Per impostazione predefinita, il cmdlet <strong>Set-CsUser</strong> non fornisce alcun oggetto attraverso la pipeline.</p></td>
</tr>
<tr class="odd">
<td><p><em>PrivateLine</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Il numero di telefono della linea telefonica privata dell'utente. Una linea privata è un numero di telefono che non è pubblicato in Servizi di dominio Active Directory e che quindi non è immediatamente disponibile alle altre persone. Inoltre, questa linea privata ignora la maggior parte delle regole di routing per le chiamate in entrata; ad esempio, una chiamata a una linea privata non viene inoltrata ai delegati di una persona. Le linee private sono spesso utilizzate per le telefonate personali o per le chiamate di affari che non riguardano gli altri membri del team.</p>
<p>La linea privata deve essere specificata utilizzando il formato E.164 e il prefisso &quot;TEL:&quot;. Ad esempio: TEL:+14255551297.</p></td>
</tr>
<tr class="even">
<td><p><em>RemoteCallControlTelephonyEnabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se l'utente è stato abilitato alla telefonia con controllo delle chiamate remote. Se è abilitato per il controllo delle chiamate remote, un utente può utilizzare Lync Server per rispondere alle chiamate effettuate al telefono da tavolo. È inoltre possibile effettuare le telefonate utilizzando Lync. Queste chiamate si basano sulla rete telefonica standard, denominata anche PSTN (Public Switched Telephone Network). Per effettuare e ricevere telefonate su Internet, l'utente deve essere abilitato per VoIP aziendale. Per informazioni dettagliate, vedere il parametro EnterpriseVoiceEnabled.</p>
<p>Per essere abilitato al controllo delle chiamate remote, un utente deve disporre sia di LineUri che di LineServerUri.</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Identificatore univoco (simile a un indirizzo di posta elettronica) che consente all'utente di comunicare utilizzando dispositivi SIP come Lync. L'indirizzo SIP deve utilizzare il prefisso sip: e un dominio SIP valido, ad esempio: -SipAddress sip:kenmyer@litwareinc.com.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Stringa oppure oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Il cmdlet **Set-CsUser** accetta gli input tramite pipeline dei valori stringa che rappresentano l'identità di un account utente abilitato per Lync Server. Il cmdlet accetta anche istanze di oggetti utente di Active Directory inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CsUser** non restituisce alcun oggetto.

## Vedere anche

#### Ulteriori risorse

[Disable-CsUser](disable-csuser.md)  
[Enable-CsUser](enable-csuser.md)  
[Get-CsUser](get-csuser.md)  
[Move-CsUser](move-csuser.md)

