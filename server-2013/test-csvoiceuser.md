---
title: Test-CsVoiceUser
TOCTitle: Test-CsVoiceUser
ms:assetid: f29c3b43-d315-4964-ab5c-9fb14612db34
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413013(v=OCS.15)
ms:contentKeyID: 49302437
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsVoiceUser

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Identifica la route che una telefonata, effettuata da un determinato utente, dovrebbe seguire per essere completata sulla base di regole vocali, route e criteri. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsVoiceUser -DialedNumber <PhoneNumber> -SipUri <UserIdParameter> [-Force <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio viene eseguito un test vocale sull'utente con indirizzo SIP sip:kmyer@litwareinc.com. Il test viene eseguito sul numero di telefono fornito dal parametro DialedNumber ("+14255559999"). Se non vengono identificate corrispondenze di regole o route, il cmdlet restituisce un valore NULL. È stato incluso anche il parametro Verbose. Verbose è un comune parametro Windows PowerShell che visualizzerà informazioni aggiuntive durante l'esecuzione del test, come ad esempio quale dial plan e criterio vocale vengono caricati per il test.

    Test-CsVoiceUser -DialedNumber "+14255559999" -SipUri "sip:kmyer@litwareinc.com" -Verbose

## ESEMPIO 2

Nell'esempio viene eseguito un test di routing vocale per tutti gli utenti abilitati per Lync Server o Office Communications Server. Il comando inizia con una chiamata al cmdlet **Get-CsUser**, che restituisce una raccolta di tutti gli utenti abilitati per Lync Server o Office Communications Server. Nell'esempio la raccolta di utenti viene quindi inviata tramite pipe al cmdlet **ForEach-Object**. Il cmdlet analizzerà ogni singolo oggetto utente ed eseguirà le azioni specificate tra parentesi graffe ({}).

La prima azione è inviare il nome visualizzato dell'utente corrente. L'utente corrente è rappresentato dai caratteri $\_; pertanto il nome visualizzato è nella proprietà DisplayName di $\_. A questo punto è possibile visualizzare quale account utente viene sottoposto al test. Successivamente, viene chiamato il cmdlet **Test-CsVoiceUser**, passando i parametri DialedNumber ("+14255559999") e SipUri dell'utente corrente. Nell'esempio viene utilizzato l'indirizzo SIP dell'utente ($\_.SipAddress).

Al termine, dato che per impostazione predefinita l'output è in formato tabella e può venire interrotto, i risultati del test vengono inviati tramite pipe al cmdlet **Format-List**, di conseguenza ogni singolo nome visualizzato dell'utente sarà seguito da una linea per ciascun campo di output.

    Get-CsUser | ForEach-Object {$_.DisplayName; Test-CsVoiceUser -DialedNumber "+14255559999" -SipUri $_.SipAddress} | Format-List

## Descrizione dettagliata

Quando un utente effettua una telefonata, la route che la telefonata segue per raggiungere la propria destinazione dipende dai criteri e dai dial plan assegnati a un determinato utente. Specificando un indirizzo SIP dell'utente e un numero di telefono, il cmdlet restituisce il numero convertito in formato E.164 (sulla base del dial plan dell'utente), la regola di normalizzazione che ha fornito tale conversione, la prima route (sulla base della priorità delle route) con un formato numero corrispondente al numero di telefono e l'utilizzo telefono che collegherebbe il criterio vocale di un determinato utente alla route vocale.

Il cmdlet può essere utilizzato per determinare se uno specifico numero di telefono verrà utilizzato per il routing e verrà convertito come previsto sulla base delle impostazioni utente e consente di risolvere i problemi riscontrati dai singoli utenti.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Test-CsVoiceUser** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsVoiceUser"}

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
<td><p><em>DialedNumber</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Voice.PhoneNumber</p></td>
<td><p>Il numero di telefono da testare.</p>
<p>Tipo di dati completi: Microsoft.Rtc.Management.Voice.PhoneNumber</p></td>
</tr>
<tr class="even">
<td><p><em>SipUri</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>L'URI SIP dell'utente su cui viene eseguito il test. Questo è il parametro Identity dell'utente utilizzato nei cmdlet CsUser. L'identità utente può essere specificata con uno dei quattro formati riportati di seguito: 1) l'indirizzo SIP dell'utente; 2) l'UPN (User Principal Name) dell'utente; 3) il nome di dominio e il nome di accesso dell'utente, nella forma dominio\accesso (ad esempio litwareinc\kenmyer); 4) il nome visualizzato Active Directory dell'utente (ad esempio Ken Myer). Notare che SamAccountName non può essere utilizzato come identità.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di prompt di conferma o messaggi di errore non irreversibile che possono verificarsi quando si esegue il cmdlet.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Restituisce un oggetto di tipo Microsoft.Rtc.Management.Voice.OcsVoiceUserTestResult.

## Vedere anche

#### Ulteriori risorse

[Get-CsUser](get-csuser.md)

