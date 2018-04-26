---
title: Set-CsExUmContact
TOCTitle: Set-CsExUmContact
ms:assetid: c0fe0fdc-6fea-4334-8645-24ffd494db07
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412944(v=OCS.15)
ms:contentKeyID: 49301852
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsExUmContact

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un oggetto contatto Operatore automatico o Accesso sottoscrittore esistente per il servizio Messaggistica unificata di Exchange ospitato. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsExUmContact -Identity <UserIdParameter> [-AutoAttendant <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-DisplayNumber <String>] [-DomainController <Fqdn>] [-Enabled <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-PassThru <SwitchParameter>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Questo esempio imposta su True la proprietà AutoAttendant del contatto Messaggistica unificata di Exchange con l'indirizzo SIP exumsa4@fabrikam.com. Come prima cosa viene richiamato il cmdlet **Get-CsExUmContact** per recuperare l'oggetto contatto (si sarebbe potuto utilizzare anche il nome visualizzato in Servizi di dominio Active Directory del contatto, il nome principale del contatto utente o il nome di accesso del contatto). Questo comando recupera il contatto con il parametro Identity fornito. Il contatto viene quindi passato al cmdlet **Set-CsExUmContact**, dove il parametro AutoAttendant viene impostato su True.

    Get-CsExUmContact -Identity sip:exumsa4@fabrikam.com | Set-CsExUmContact -AutoAttendant $True

## ESEMPIO 2

Questo esempio è identico all'esempio 1, ma invece di recuperare il contatto chiamando il cmdlet **Get-CsExUmContact** e inviare tramite pipe l'oggetto al cmdlet **Set-CsExUmContact**, al cmdlet **Set-CsExUmContact** viene fornito il valore Identity del contatto che si desidera modificare. Si noti il formato del parametro Identity: in questo caso, è stato utilizzato il nome distinto completo dell'oggetto contatto che include un GUID generato automaticamente (al momento della creazione del contatto). Viene quindi impostato su True il parametro AutoAttendant del contatto.

    Set-CsExUmContact -Identity "CN={1bf6208d-2847-45d0-828f-636f14da858b},OU=ExUmContacts,DC=litwareinc,DC=com" -AutoAttendant $True

## Descrizione dettagliata

Lync Server collabora con Messaggistica unificata di Exchange per fornire diverse funzionalità vocali, tra cui Operatore automatico e Accesso sottoscrittore. Quando Messaggistica unificata di Exchange viene fornito come servizio ospitato (anziché locale), è necessario creare oggetti contatto mediante Windows PowerShell per applicare le funzionalità Operatore automatico e Accesso sottoscrittore. Questi oggetti sono creati tramite il cmdlet **New-CsExUmContact** e possono essere successivamente modificati utilizzando il cmdlet **Set-CsExUmContact**.

Il modo più semplice per utilizzare questo cmdlet consiste spesso nel chiamare per prima cosa il cmdlet **Get-CsExUmContact** per recuperare un'istanza dell'oggetto contatto che si desidera modificare. È sufficiente inviare tramite pipe l'output del cmdlet **Get-CsExUmContact** al cmdlet **Set-CsExUmContact** e assegnare i valori ai parametri delle proprietà che si intende modificare. Per informazioni dettagliate, vedere la sezione relativa agli esempi in questo argomento. In alternativa, è possibile chiamare il cmdlet **Set-CsExUmContact**, passando il parametro Identity dell'oggetto contatto che si desidera modificare.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsExUmContact** i membri dei seguenti gruppi: RTCUniversalUserAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsExUmContact"}

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
<td><p>L'identificatore univoco dell'oggetto contatto che si desidera modificare. Le identità dei contatti possono essere specificate utilizzando uno dei quattro formati seguenti: 1) L'indirizzo SIP del contatto; 2) il nome dell'entità utente (UPN) del contatto; 3) il nome del dominio del contatto e il nome di accesso nella forma dominio\accesso (ad esempio, litwareinc\exum1); infine, 4) il nome di visualizzazione Active Directory del contatto (ad esempio, Team Auto Attendant).</p>
<p>Tipo di dati completi: Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
</tr>
<tr class="even">
<td><p><em>AutoAttendant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Impostare il parametro su True se l'oggetto contatto è un Operatore automatico. Questo parametro è False per impostazione predefinita.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Una descrizione del contatto. La descrizione consente agli amministratori di identificare il tipo di contatto (Operatore automatico o Accesso sottoscrittore), l'ubicazione, il provider o qualsiasi altra informazione che identifichi lo scopo di ciascun contatto Messaggistica unificata di Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Il numero di telefono del contatto. I numeri visualizzati per ogni contatto devono essere univoci (ovvero due contatti di Messaggistica unificata di Exchange non possono avere lo stesso numero visualizzato). La modifica del valore non modifica il valore della proprietà LineURI.</p>
<p>Questo valore può iniziare con un segno più (+) e può contenere qualsiasi numero di cifre. La prima cifra non può essere uno zero.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Fqdn</p></td>
<td><p>Consente di specificare un controller di dominio. Se non è specificato alcun controller di dominio, verrà utilizzato il primo disponibile.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se il contatto è stato abilitato per Lync Server. L'impostazione di questo parametro su False disabiliterà il contatto e l'Operatore automatico o l'accesso sottoscrittore associato con il contatto smetterà di funzionare.</p>
<p>Se si disabilita un account utilizzando il parametro Enabled, le informazioni associate a questo account (compresi i criteri segreteria telefonica ospitati assegnati) verranno mantenute. Se l'account viene riabilitato nuovamente utilizzando il parametro Enable, le informazioni associate all'account verranno ripristinate.</p></td>
</tr>
<tr class="even">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se il contatto è stato abilitato per VoIP aziendale. Se il valore è impostato su False, le funzionalità Operatore automatico o accesso sottoscrittore associate a questo contatto non saranno più disponibili.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExchangeArchivingPolicy</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>ExchangeArchivingPolicyOptionsEnum</p></td>
<td><p>Indica dove vengono archiviate le sessioni di messaggistica istantanea del contatto. I valori consentiti sono:</p>
<p>* Uninitialized</p>
<p>* UseLyncArchivingPolicy</p>
<p>* ArchivingToExchange</p>
<p>* NoArchiving</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>witchParameter</p></td>
<td><p>Restituisce i risultati del comando. Per impostazione predefinita, il cmdlet non genera alcun output.</p></td>
</tr>
<tr class="odd">
<td><p><em>SipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>L'indirizzo SIP del contatto. Deve essere un nuovo indirizzo che non è già esistente come utente o contatto in Servizi di dominio Active Directory.</p>
<p>La modifica di questo valore non comporterà la modifica dell'indirizzo SIP archiviato nella proprietà OtherIpPhone.</p>
<p>È possibile utilizzare SipAddress come valore Identity per i comandi del cmdlet <strong>Get-CsExUmContact</strong> per recuperare contatti specifici. Quando si chiama questo cmdlet, verrà utilizzato il nuovo indirizzo SIP. Le query sull'indirizzo SIP precedente non restituiranno alcun oggetto.</p></td>
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

Oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADExUmContact. Accetta l'input da pipeline di oggetti contatto di Messaggistica unificata di Exchange.

## Tipi restituiti

Questo cmdlet modifica un oggetto di tipo Microsoft.Rtc.Management.ADConnect.Schema.OCSADExUmContact. Se viene utilizzato il parametro PassThru, viene restituito anche un oggetto di questo tipo.

## Vedere anche

#### Ulteriori risorse

[New-CsExUmContact](new-csexumcontact.md)  
[Remove-CsExUmContact](remove-csexumcontact.md)  
[Get-CsExUmContact](get-csexumcontact.md)  
[Move-CsExUmContact](move-csexumcontact.md)

