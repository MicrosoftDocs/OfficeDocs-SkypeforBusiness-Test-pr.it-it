---
title: Set-CsCommonAreaPhone
TOCTitle: Set-CsCommonAreaPhone
ms:assetid: 765ab74c-33ca-4b17-ba15-edb2fe559ebb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398579(v=OCS.15)
ms:contentKeyID: 49301009
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsCommonAreaPhone

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica i valori delle proprietà di un telefono di area comune gestito da Lync Server. I telefoni di area comune sono telefoni posizionati nelle sale d'attesa degli edifici, nelle sale di ritrovo del personale o in altre posizioni in cui possono essere utilizzati da persone diverse e per usi diversi. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsCommonAreaPhone -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-Description <String>] [-DisplayName <String>] [-DisplayNumber <String>] [-DomainController <Fqdn>] [-Enabled <$true | $false>] [-EnterpriseVoiceEnabled <$true | $false>] [-ExchangeArchivingPolicy <Uninitialized | UseLyncArchivingPolicy | NoArchiving | ArchivingToExchange>] [-LineURI <String>] [-PassThru <SwitchParameter>] [-SipAddress <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene modificato il nome visualizzato di Active Directory per il telefono di area comune con il numero 1-425-555-6710. A tale scopo, viene chiamato innanzitutto il cmdlet **Get-CsCommonAreaPhone** insieme al parametro Filter. Il valore di filtro {LineUri -eq "tel:+14255556710"} limita il numero di dati restituiti al telefono di area comune in cui la proprietà LineUri è uguale a tel:+14255556710. L'oggetto restituito viene quindi inviato tramite pipe al cmdlet **Set-CsCommonAreaPhone**, che imposta il valore della proprietà DisplayName su "Employee Lounge".

    Get-CsCommonAreaPhone -Filter {LineUri -eq "tel:+14255556710"} | Set-CsCommonAreaPhone -DisplayName "Employee Lounge"

## ESEMPIO 2

Il comando illustrato nell'esempio 2 abilita tutti i telefoni di area comune attualmente configurati per l'utilizzo all'interno dell'organizzazione. A tale scopo, il comando chiama il cmdlet **Get-CsCommonAreaPhone** senza alcun parametro per ottenere una raccolta di tutti i telefoni di area comune. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsCommonAreaPhone**, che imposta la proprietà Enabled su True per ogni elemento della raccolta.

    Get-CsCommonAreaPhone | Set-CsCommonAreaPhone -Enabled $True

## ESEMPIO 3

Nell'esempio 3 viene aggiunta una descrizione generica a tutti i telefoni di area comune alla cui proprietà Description non è stato assegnato un valore. A tale scopo, viene chiamato il cmdlet **Get-CsCommonAreaPhone** con il parametro Filter. Il valore di filtro {Description -eq $Null} garantisce che gli unici elementi restituiti siano i telefoni di area comune in cui la proprietà Description è uguale a un valore Null. Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Set-CsCommonAreaPhone**, che assegna la descrizione generica "Common area phone" a ogni elemento della raccolta.

    Get-CsCommonAreaPhone -Filter {Description -eq $Null} | Set-CsCommonAreaPhone -Description "Common area phone"

## Descrizione dettagliata

I telefoni di area comune sono telefoni IP non associati a un singolo utente. Invece di essere installati in qualche ufficio, tali telefoni sono generalmente posizionati nelle sale d'attesa degli edifici, nelle mense, nelle aree riservate ai dipendenti, nelle sale riunioni e in altri luoghi in cui è probabile si ritrovino molte persone. Per gli amministratori questa è una sfida gestionale, in quanto l'utilizzo dei telefoni in Lync Server viene normalmente gestito mediante criteri vocali e dial plan assegnati a utenti singoli. Ai telefoni di area comune non viene assegnato un utente specifico.

Una soluzione a questa sfida è rappresentata dalla creazione di oggetti contatto di Active Directory per tutti i telefoni nelle aree comuni. Questi oggetti contatto possono essere creati usando il cmdlet **New-CsCommonAreaPhone**. Come nel caso degli account utente, anche a questi oggetti contatto è possibile assegnare criteri e voice plan. Di conseguenza, sarà possibile mantenere il controllo dei telefoni nelle aree comuni anche se non sono associati a singoli utenti. Ad esempio, se si desidera evitare che le persone possano trasferire o parcheggiare le chiamate da un telefono in un'area comune, è possibile creare un criterio vocale che impedisca il trasferimento o il parcheggio delle chiamate e quindi assegnare questo criterio ai telefoni nelle aree comuni (oppure, più correttamente, all'oggetto contatto che rappresenta il telefono nell'area comune). Questo comando assegna il criterio vocale CommonAreaPhoneVoicePolicy a tutti i telefoni nelle aree comuni:

Get-CsCommonAreaPhone | Grant-CsVoicePolicy –PolicyName "CommonAreaPhoneVoicePolicy"

Il cmdlet **Set-CsCommonAreaPhone** consente di modificare le proprietà degli oggetti contatto associati ai telefoni di area comune. Tra l'altro, è possibile modificare il nome visualizzato di Active Directory del contatto o l'URI (Uniform Resource Identifier) di linea associato al telefono. È altresì possibile utilizzare il parametro Enabled per abilitare e disabilitare l'account per l'utilizzo con Lync Server.

È inoltre possibile configurare l'hotdesking per telefoni di area comune utilizzando i cmdlet CsClientPolicy. Con un telefono di tipo Hot Desk, gli utenti possono accedere al telefono utilizzando le credenziali di Lync Server. In questo modo, possono accedere in modo semplice ai contatti. Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Set-CsClientPolicy](set-csclientpolicy.md).

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsCommonAreaPhone** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins. Il permesso di eseguire questo cmdlet per siti specifici o specifiche unità organizzative di Active Directory (OU) può essere assegnato utilizzando il cmdlet **Grant-CsOUPermission**. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsCommonAreaPhone"}

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
<td><p>Identificatore univoco per il telefono di area comune. I telefoni di area comune vengono identificati tramite il nome distinto Active Directory dell'oggetto contatto associato. Per impostazione predefinita, i telefoni di area comune utilizzano un identificatore univoco globale (GUID) come nome comune. Avranno quindi un parametro Identity analogo al seguente: CN={ce84964a-c4da-4622-ad34-c54ff3ed361f},OU=Redmond,DC=Litwareinc,DC=com. Pertanto, potrebbe risultare più semplice recuperare i telefoni di area comune utilizzando il cmdlet <strong>Get-CsCommonAreaPhone</strong> e inviando quindi tramite pipe al cmdlet <strong>Set-CsCommonAreaPhone</strong> gli oggetti restituiti.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Consente di modificare l'attributo della descrizione di Active Directory per il telefono dell'area comune. Ciò consente di fornire ulteriori informazioni relative al telefono: ad esempio, potrebbe essere opportuno fornire dettagli su chi contattare in caso di problemi con l'apparecchio.</p></td>
</tr>
<tr class="even">
<td><p><em>DisplayName</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Consente di modificare il nome visualizzato di Active Directory per il telefono dell'area comune.</p></td>
</tr>
<tr class="odd">
<td><p><em>DisplayNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Numero di telefono come viene visualizzato in Lync. La proprietà DisplayNumber può essere formattata in qualsiasi modo, ad esempio 1-800-555-1234, 1-(800)-555-1234, 1.800.555.1234 e così via. Quando si sceglie un numero da visualizzare, tenere presente che il numero verrà visualizzato sullo schermo del telefono di area comune solo se può essere normalizzato. La normalizzazione è il processo di conversione delle stringhe di numeri in un formato standard dei numeri di telefono. Se non esiste una regola di normalizzazione per il formato dei numeri di telefono utilizzato durante la configurazione del numero da visualizzare, sullo schermo del telefono di area comune verrà visualizzato il valore della proprietà LineUri anziché il valore della proprietà DisplayNumber.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Fqdn</p></td>
<td><p>Consente la connessione al controller di dominio specificato per modificare le informazioni sul contatto. Per la connessione a uno specifico controller di dominio, includere il parametro DomainController seguito dal nome computer (ad esempio atl-mcs-001) o dal suo nome di dominio completo (FQDN) ad esempio: atl-mcs-001.litwareinc.com.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se l'oggetto contatto per il telefono di area comune è stato abilitato o meno per Lync Server.</p>
<p>Se si disabilita un contatto utilizzando il parametro Enabled, le informazioni associate a tale account (compresi i criteri assegnati e l'abilitazione del contatto per VoIP aziendale, il controllo delle chiamate remote e/o l'integrazione della segreteria telefonica) vengono mantenute. Se in seguito si riabilita l'account utilizzando il parametro Enabled, le informazioni sull'account associate vengono ripristinate.</p></td>
</tr>
<tr class="even">
<td><p><em>EnterpriseVoiceEnabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se l'oggetto contatto del telefono dell'area comune è stato abilitato per VoIP aziendale, la soluzione Voice over Internet Protocol (VoIP) offerta da Microsoft. Con VoIP aziendale, è possibile effettuare chiamate via Internet anziché utilizzare la rete telefonica standard.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExchangeArchivingPolicy</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>ExchangeArchivingPolicyOptionsEnum</p></td>
<td><p>Indica la posizione in cui vengono archiviate le sessioni di messaggistica istantanea del contatto. I valori consentiti sono:</p>
<p>* Uninitialized</p>
<p>* UseLyncArchivingPolicy</p>
<p>* ArchivingToExchange</p>
<p>* NoArchiving</p></td>
</tr>
<tr class="even">
<td><p><em>LineURI</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Numero di telefono per il telefono nell'area comune. L'URI di linea deve essere specificato utilizzando il formato E.164 e il prefisso &quot;TEL:&quot;. Ad esempio: TEL:+14255551297. Qualsiasi numero di interno deve essere aggiunto alla fine dell'URI di linea, ad esempio: TEL:+14255551297;ext=51297.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Restituisce un oggetto che rappresenta il telefono nell'area comune.</p></td>
</tr>
<tr class="even">
<td><p><em>SipAddress</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Identificatore univoco che consente al telefono di area comune di comunicare con i dispositivi SIP, ad esempio Lync. L'indirizzo SIP deve essere preceduto dal prefisso sip: e includere un dominio SIP valido. Ad esempio: sip:bldg14lobby@litwareinc.com.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact.

## Tipi restituiti

Per impostazione predefinita, il cmdlet **Set-CsCommonAreaPhone** non restituisce oggetti o valori. Se tuttavia si include il parametro PassThru, il cmdlet restituirà istanze dell'oggetto Microsoft.Rtc.Management.ADConnect.Schema.OCSADCommonAreaPhoneContact.

## Vedere anche

#### Ulteriori risorse

[Get-CsCommonAreaPhone](get-cscommonareaphone.md)  
[Move-CsCommonAreaPhone](move-cscommonareaphone.md)  
[New-CsCommonAreaPhone](new-cscommonareaphone.md)  
[Remove-CsCommonAreaPhone](remove-cscommonareaphone.md)

