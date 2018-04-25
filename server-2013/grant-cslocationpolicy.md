---
title: Grant-CsLocationPolicy
TOCTitle: Grant-CsLocationPolicy
ms:assetid: f820f892-c247-447c-947a-00414189842e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413049(v=OCS.15)
ms:contentKeyID: 49302514
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Grant-CsLocationPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Assegna un criterio percorso di Enhanced 9-1-1 (E9-1-1) a singoli utenti o gruppi. Il servizio E9-1-1 consente agli operatori che rispondono alle chiamate di emergenza di determinare la posizione geografica del chiamante. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Grant-CsLocationPolicy -Identity <UserIdParameter> -PolicyName <String> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1, il cmdlet **Grant-CsLocationPolicy** viene utilizzato per assegnare il criterio percorso Reno all'utente Davide Garghentini.

    Grant-CsLocationPolicy -Identity "Ken Myer" -PolicyName Reno

## ESEMPIO 2

Nell'esempio 2 il criterio AccountingArea viene assegnato a tutti gli utenti presenti nel reparto Contabilità. Per restituire una raccolta di tutti gli utenti nel reparto Contabilità, il cmdlet **Get-CsUser** viene utilizzato insieme al parametro LDAPFilter. Il valore della query passato a LDAPFilter -- "Department=Accounting" -- restituisce tutti gli utenti che possiedono un'impostazione del reparto Contabilità in Active Directory. La raccolta viene quindi passata al cmdlet **Grant-CsLocationPolicy**, che procede all'assegnazione del criterio AccountingArea a ciascun utente nella raccolta.

    Get-CsUser -LDAPFilter "Department=Accounting" | Grant-CsLocationPolicy -PolicyName AccountingArea

## ESEMPIO 3

Nell'esempio viene concesso il criterio percorso Reno all'utente con identità (in questo caso il nome visualizzato) Davide Garghentini. Inoltre, nell'esempio è presente il parametro PassThru, che consentirà di visualizzare le informazioni utente relative all'utente Davide Garghentini dopo che è stato concesso il criterio percorso. Tuttavia, anziché visualizzare immediatamente le informazioni utente sulla console, le informazioni vengono inviate tramite pipe al cmdlet **Select-Object**, che visualizzerà solamente le proprietà DisplayName e LocationPolicy dell'utente.

Nell'esempio, il criterio percorso appena concesso verrà visualizzato nell'output in LocationPolicy, ma verrà visualizzato come valore di ancoraggio anziché come nome del criterio. (Il valore di ancoraggio è un valore numerico assegnato automaticamente ad un criterio nel momento in cui viene creato). Per verificare che il nome del criterio sia stato applicato, eseguire il comando Get-CsUser –Identity "Davide Garghentini" | Select-Object DisplayName, LocationPolicy.

    Grant-CsLocationPolicy -Identity "Ken Myer" -PolicyName Reno -PassThru | Select-Object DisplayName, LocationPolicy

## Descrizione dettagliata

Il criterio percorso viene utilizzato per applicare le impostazioni relative alla funzionalità del servizio di chiamate di emergenza. Il criterio percorso determina se un utente è abilitato per le chiamate di emergenza e, in tal caso, qual è il comportamento di una chiamata di emergenza. Ad esempio, è possibile utilizzare il criterio percorso per definire i numeri che rappresentano una chiamata di emergenza (113 in Italia), per definire se inviare o meno una notifica all'ufficio di sicurezza aziendale e la modalità di instradamento della chiamata. Questo cmdlet concede un criterio percorso a un utente o gruppo specifico.

IMPORTANTE: il criterio percorso si comporta diversamente dagli altri criteri di Lync Server in termini di ordine dell'ambito. Per tutti gli altri criteri, se viene definito un criterio nell'ambito per utente, viene applicato a qualsiasi utente a cui è stato concesso il criterio. Se all'utente non è stato concesso un criterio per utente, viene applicato il criterio di sito. Se non è presente alcun criterio di sito, viene applicato il criterio globale. I criteri percorso vengono applicati nello stesso modo, con una sola eccezione: un criterio percorso per utente può anche essere assegnato a un sito di rete (un sito di rete è formato da un gruppo di sottoreti). Se l'utente effettua la chiamata di emergenza da una posizione mappata a un sito di rete nell'organizzazione, viene assegnato il criterio a livello di utente a tale sito di rete. Questa funzionalità sostituisce eventuali criteri per utente concessi all'utente. Se l'utente chiama da una posizione sconosciuta o non mappata nell'organizzazione, viene applicato l'ambito del criterio standard.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Grant-CsLocationPolicy** in locale: RTCUniversalUserAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Grant-CsLocationPolicy"}

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
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Indica l'identità dell'account utente a cui assegnare i criteri. Le identità utente possono essere specificate con uno dei quattro formati riportati di seguito: 1) l'indirizzo SIP dell'utente; 2) l'UPN (User Principal Name) dell'utente; 3) il nome di dominio e il nome di accesso dell'utente, nel formato dominio\accesso (ad esempio, litwareinc\davidegarghentini); 4) il nome visualizzato Active Directory dell'utente (ad esempio, Davide Garghentini). Il nome SAMAccountName non può essere utilizzato come identità.</p>
<p>È inoltre possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il valore di Display Name per il parametro Identity per l'utente. Ad esempio, il parametro Identity &quot;* Smith&quot; assegna i criteri a tutti gli utenti con cognome Smith.</p></td>
</tr>
<tr class="even">
<td><p><em>PolicyName</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>L'identità del criterio percorso da applicare all'utente.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DomainController</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Consente di specificare un controller di dominio. Se non è specificato alcun controller di dominio, verrà utilizzato il primo disponibile.</p></td>
</tr>
<tr class="odd">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Includendo questo parametro (che non richiede alcun valore) le informazioni utente vengono visualizzate al completamento del cmdlet. In genere non si ottiene alcun output quando si esegue questo cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Stringa. Accetta un valore stringa inviato tramite pipe che rappresenta l'identità di un account utente a cui viene concesso il criterio percorso.

## Tipi restituiti

Se utilizzato con il parametro PassThru, restituisce un oggetto del tipo Microsoft.Rtc.Management.ADConnect.Schema.OCSADUserOrAppContact.

## Vedere anche

#### Ulteriori risorse

[New-CsLocationPolicy](new-cslocationpolicy.md)  
[Remove-CsLocationPolicy](remove-cslocationpolicy.md)  
[Set-CsLocationPolicy](set-cslocationpolicy.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)  
[Test-CsLocationPolicy](test-cslocationpolicy.md)  
[Get-CsUser](get-csuser.md)

