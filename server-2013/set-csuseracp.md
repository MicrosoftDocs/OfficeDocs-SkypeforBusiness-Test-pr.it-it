---
title: Set-CsUserAcp
TOCTitle: Set-CsUserAcp
ms:assetid: f3138d9f-fa3e-4a3c-aa8e-f6dbdda8a834
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413018(v=OCS.15)
ms:contentKeyID: 49302459
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsUserAcp

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Aggiunge un nuovo provider di servizi di audioconferenza a un utente o a un gruppo di utenti oppure modifica un provider di servizi di audioconferenza esistente già assegnato a un utente. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsUserAcp -Identity <UserIdParameter> -Domain <String> -Name <String> -ParticipantPasscode <String> -TollNumber <String> [-Confirm [<SwitchParameter>]] [-IsDefault <$true | $false>] [-PassThru <SwitchParameter>] [-TollFreeNumbers <String[]>] [-Url <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1, il cmdlet **Set-CsUserAcp** viene utilizzato per assegnare un nuovo provider di servizi di audioconferenza all'utente Davide Garghentini. Per questo scopo, viene utilizzato il parametro Identity per indicare l'account utente da modificare. Sono inclusi inoltre i parametri obbligatori TollNumber, ParticipantPassCode, Domain e Name, con i valori di parametro appropriati.

    Set-CsUserAcp -Identity "Ken Myer" -TollNumber "14255551298" -ParticipantPassCode 13761 -Domain "fabrikam.com" -Name "Fabrikam ACP"

## ESEMPIO 2

Con il comando mostrato nell'esempio 2 si assegna lo stesso provider di servizi di audioconferenza a tutti gli utenti che lavorano nel reparto Finance. Per questo scopo, viene utilizzato prima il cmdlet **Get-CsUser** e il parametro LdapFilter (con valore di filtro "Department=Finance") per restituire una raccolta di tutti gli utenti che lavorano nel reparto Finance. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsUserAcp**, che assegna lo stesso provider di servizi di audioconferenza (Fabrikam ACP) a ogni utente nella raccolta.

    Get-CsUser -LdapFilter "Department=Finance" | Set-CsUserAcp -TollNumber "14255551298" -ParticipantPassCode 13761 -Domain "fabrikam.com" -Name "Fabrikam ACP"

## ESEMPIO 3

Nell'esempio 3 viene assegnato un provider di servizi di audioconferenza Fabrikam ACP all'utente Ken Myer. Oltre a specificare i parametri TollNumber, ParticipantPassCode, Domain e Name, questo comando include anche una coppia di numeri verdi. Per assegnare questi due valori, includere il parametro TollFreeNumbers seguito dai due numeri di telefono, separati tra loro da una virgola.

    Set-CsUserAcp -Identity "Ken Myer" -TollNumber "14255551298" -ParticipantPassCode 13761 -Domain "fabrikam.com" -Name "Fabrikam ACP" -TollFreeNumbers "18005551010", "18005551020"

## Descrizione dettagliata

Un provider di servizi di audioconferenza è una società di terze parti che fornisce servizi di conferenza alle organizzazioni. Tra l'altro, i provider di servizi di audioconferenza consentono agli utenti in trasferta, che non sono connessi alla rete aziendale o a Internet, di accedere ai contenuti audio di una conferenza o di una riunione. Tali provider offrono spesso servizi di qualità elevata quali traduzione immediata, trascrizione e assistenza diretta di un operatore durante la conferenza.

Lync Server non consente l'integrazione completa con i provider di servizi di audioconferenza. I cmdlet **CsUserAcp** consentono agli amministratori di impostare un numero di telefono e un passcode, nonché di configurare altre informazioni che possono essere utilizzate per l'integrazione dei provider di servizi di audioconferenza ogni volta che un utente pianifica una riunione. Tuttavia, poiché tali cmdlet non sono stati progettati per la versione locale di Lync Server (sono infatti concepiti per essere utilizzati esclusivamente con Lync Online) non sono supportate altre opzioni di integrazione dei provider di servizi di audioconferenza oltre l'assegnazione dei valori delle proprietà.

È possibile assegnare i provider di servizi di audioconferenza a un account utente utilizzando il cmdlet **Set-CsUserAcp** (a un utente possono essere assegnati più provider di servizi di audioconferenza). Il cmdlet **Set-CsUserAcp** viene utilizzato anche per modificare le proprietà di un provider di servizi di audioconferenza esistente. Se si chiama il cmdlet **Set-CsUserAcp**, il cmdlet utilizza le informazioni dei parametri incluse nella chiamata per verificare i provider di servizi di audioconferenza esistenti assegnati all'utente. Se viene rilevata una corrispondenza, il provider esistente viene modificato. Ad esempio, si supponga di eseguire il comando seguente:

Set-CsUserAcp –Identity "Davide Garghentini" –TollNumber "15554251298" –ParticipantPassCode 13761 –Domain "fabrikam.com" –Name "Fabrikam ACP"

Si supponga quindi che a Davide Garghentini sia già stato assegnato un provider di servizi di audioconferenza denominato Fabrikam ACP con gli stessi parametri TollNumber e Domain specificati nel comando (ovvero, l'unica differenza è costituita da ParticipantPassCode). In tal caso, il cmdlet **Set-CsUserAcp** modificherà il provider Fabrikam ACP esistente. Se non viene rilevata una corrispondenza, verrà aggiunto un nuovo provider all'account utente di Davide Garghentini.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsUserAcp** in locale: RTCUniversalUserAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsUserAcp"}

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
<td><p><em>Domain</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome di dominio del provider di servizi di audioconferenza. Ad esempio: -Domain &quot;fabrikam.com&quot;.</p>
<p>Il nome di dominio verrà assegnato dal provider di servizi di audioconferenza.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Indica l'identità dell'account utente da modificare. L'identità utente può essere specificata con uno dei quattro formati riportati di seguito: 1) l'indirizzo SIP dell'utente; 2) l'UPN (User Principal Name) dell'utente; 3) il nome di dominio e il nome di accesso dell'utente, nella forma dominio\accesso (ad esempio litwareinc\davidegarghentini); 4) il nome visualizzato Servizi di dominio Active Directory dell'utente (ad esempio Davide Garghentini). È possibile fare riferimento alle identità utente anche utilizzando il nome distinto Active Directory dell'utente.</p>
<p>È possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il nome visualizzato come identità utente. Ad esempio, l'identità &quot;* Smith&quot; restituisce tutti gli utenti il cui nome visualizzato termina con il valore stringa &quot; Smith&quot;.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome del provider di servizi di audioconferenza. Ad esempio: -Name &quot;Fabrikam Conference Services&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>ParticipantPasscode</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Passcode obbligatorio quando ci si connette a una conferenza mediante il provider di servizi di audioconferenza. Ad esempio: -PassCode &quot;0712&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>TollNumber</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Numero telefonico a pagamento utilizzato per le audioconferenze. Ad esempio: -TollNumber &quot;14255551298&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>IsDefault</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se si tratta del provider di servizi di audioconferenza predefinito per l'utente. Ogni utente può avere un solo provider predefinito.</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di passare un oggetto tramite la pipeline che rappresenta l'utente per cui vengono configurate le proprietà dell'account. Il parametro PassThru è obbligatorio in tali casi, in quanto, per impostazione predefinita, il cmdlet <strong>Set-CsUserAcp</strong> non consente di passare oggetti tramite la pipeline.</p></td>
</tr>
<tr class="odd">
<td><p><em>TollFreeNumbers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String[]</p></td>
<td><p>Raccolta di numeri verdi utilizzati per le audioconferenze. Ad esempio: -TollFreeNumbers &quot;18005551298&quot;. Per aggiungere più numeri verdi, separarli mediante virgole: -TollFreeNumber &quot;18005551298&quot;, &quot;18005559876&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Url</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>URL Web per il provider di servizi di audioconferenza, ad esempio: -Url &quot;http://acp.fabrikam.com&quot;. L'URL Web consente ai provider di servizi di audioconferenza di indirizzare gli utenti a una pagina Web contenente numeri di telefono aggiuntivi per la conferenza telefonica ad accesso esterno, nonché informazioni sui servizi offerti dal provider di servizi di audioconferenza.</p></td>
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

Stringa o oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Il cmdlet **Set-CsUserAcp** accetta un valore stringa inviato tramite pipe che rappresenta l'identità di un account utente abilitato per Lync Server. Il cmdlet accetta anche istanze inviate tramite pipe dell'oggetto utente di Active Directory.

## Tipi restituiti

Nessuno.

## Vedere anche

#### Ulteriori risorse

[Get-CsUserAcp](get-csuseracp.md)  
[Remove-CsUserAcp](remove-csuseracp.md)

