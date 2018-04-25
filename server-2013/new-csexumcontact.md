---
title: New-CsExUmContact
TOCTitle: New-CsExUmContact
ms:assetid: 085d0a0f-0efb-4c65-b742-2c1cb7a5ae8f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398139(v=OCS.15)
ms:contentKeyID: 49299597
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsExUmContact

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo oggetto contatto Operatore automatico o Accesso sottoscrittore per Messaggistica unificata di Exchange ospitata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsExUmContact -DisplayNumber <String> -OU <OUIdParameter> -RegistrarPool <Fqdn> -SipAddress <String> [-AutoAttendant <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene chiamato il cmdlet **New-CsExUmContact** per creare un nuovo oggetto contatto Active Directory di Messaggistica unificata di Exchange. Per creare un nuovo contatto, è necessario fornire l'indirizzo SIP (in questo esempio sip:exumsa1@fabrikam.com) dell'Operatore automatico o dell'Accesso sottoscrittore. È inoltre necessario fornire il nome del pool in cui è in esecuzione il servizio di registrazione di Lync Server (RedmondPool.litwareinc.com), l'unità organizzativa in cui saranno archiviate tali informazioni (OU=ExUmContacts,DC=litwareinc,DC=com) e il numero di telefono dell'Operatore automatico o dell'Accesso sottoscrittore (2065554567). Poiché il parametro AutoAttendant non è stato impostato esplicitamente, verrà applicato il valore predefinito False e pertanto questo oggetto contatto sarà considerato come un contatto Accesso sottoscrittore.

    New-CsExUmContact -SipAddress sip:exumsa1@fabrikam.com -RegistrarPool RedmondPool.litwareinc.com -OU "OU=ExUmContacts,DC=litwareinc,DC=com" -DisplayNumber 2065554567

## ESEMPIO 2

In questo esempio, simile all'esempio 1, viene chiamato il cmdlet **New-CsExUmContact** per creare un nuovo contatto di Messaggistica unificata di Exchange. Anche in questo caso viene creato un nuovo contatto Operatore automatico o Accesso sottoscrittore, questa volta con indirizzo SIP sip:exumaa1@fabrikam.com. Vengono inoltre forniti il nome del pool in cui è in esecuzione il servizio di registrazione di Lync Server (RedmondPool.litwareinc.com), l'unità organizzativa in cui saranno archiviate tali informazioni (OU=ExUmContacts,DC=litwareinc,DC=com) e il numero di telefono dell'Operatore automatico o dell'Accesso sottoscrittore (2065554567). La differenza rilevabile in questo esempio è l'impostazione del parametro facoltativo AutoAttendant su True ($True) per indicare che questo oggetto è in effetti un contatto Operatore automatico.

    New-CsExUmContact -SipAddress sip:exumaa1@fabrikam.com -RegistrarPool RedmondPool.litwareinc.com -OU "OU=ExUmContacts,DC=litwareinc,DC=com" -DisplayNumber 2065559876 -AutoAttendant $True

## Descrizione dettagliata

Lync Server interagisce con Messaggistica unificata di Exchange per fornire diverse funzionalità vocali, tra cui Operatore automatico e Accesso sottoscrittore. Se si fornisce Messaggistica unificata di Exchange come servizio ospitato (anziché locale), è necessario creare oggetti contatto con questo cmdlet per applicare le funzionalità Operatore automatico e Accesso sottoscrittore. Per creare questi oggetti viene chiamato il cmdlet **New-CsExUmContact**.

Un oggetto contatto creato con questo cmdlet non sarà disponibile per l'uso nel sistema fin quando non sarà applicato un criterio di segreteria telefonica ospitato che configuri il routing per il contatto. Per recuperare i criteri di segreteria telefonica ospitati è possibile chiamare il cmdlet **Get-CsHostedVoicemailPolicy**. Dai criteri recuperati è possibile determinare se esiste un criterio globale o di sito appropriato, oppure se esiste un criterio per utente che deve essere assegnato a questo contatto.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **New-CsExUmContact** in locale: RTCUniversalUserAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsExUmContact"}

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
<td><p><em>DisplayNumber</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Il numero di telefono del contatto. I numeri visualizzati per ogni contatto devono essere univoci (ad esempio, due contatti Messaggistica unificata di Exchange non possono avere lo stesso numero visualizzato).</p>
<p>Questo valore può iniziare con un segno più (+) e può contenere qualsiasi numero di cifre. La prima cifra non può essere uno zero.</p></td>
</tr>
<tr class="even">
<td><p><em>OU</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
<td><p>L'unità organizzativa che conterrà questo contatto in Active Directory.</p>
<p>Tipo di dati completi: Microsoft.Rtc.Management.AD.OUIdParameter</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPool</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Il nome di dominio completo del pool su cui è in esecuzione il servizio di registrazione.</p>
<p>Un contatto Messaggistica unificata di Exchange in Lync Server non può essere spostato nei pool che fanno parte di distribuzioni di Microsoft Office Communications Server 2007 o di Microsoft Office Communications Server 2007 R2.</p>
<p>Tipo di dati completi: Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
</tr>
<tr class="even">
<td><p><em>SipAddress</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>L'indirizzo SIP del contatto. Deve essere un nuovo indirizzo che non è già esistente come utente o contatto in Servizi di dominio Active Directory. Questo valore deve iniziare con la stringa sip: seguita dall'indirizzo SIP.</p></td>
</tr>
<tr class="odd">
<td><p><em>AutoAttendant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Specifica se questo oggetto contatto è un Operatore automatico. La funzionalità Operatore automatico mette a disposizione una serie di istruzioni vocali che consentono ai chiamanti di navigare nel sistema telefonico fino a raggiungere l'utente desiderato.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Una descrizione del contatto. La descrizione consente agli amministratori di identificare il tipo di contatto (Operatore automatico o Accesso sottoscrittore), l'ubicazione, il provider o qualsiasi altra informazione che identifichi lo scopo di ciascun contatto Messaggistica unificata di Exchange.</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Restituisce i risultati di questo comando. Con l'esecuzione del cmdlet viene visualizzato l'oggetto appena creato; se si include questo parametro tale output viene ripetuto, pertanto l'uso del parametro si rivela ridondante.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Consente di creare un oggetto di tipo Microsoft.Rtc.Management.ADConnect.Schema.OCSADExUmContact.

## Vedere anche

#### Ulteriori risorse

[Remove-CsExUmContact](remove-csexumcontact.md)  
[Set-CsExUmContact](set-csexumcontact.md)  
[Get-CsExUmContact](get-csexumcontact.md)  
[Move-CsExUmContact](move-csexumcontact.md)  
[Get-CsHostedVoicemailPolicy](get-cshostedvoicemailpolicy.md)

