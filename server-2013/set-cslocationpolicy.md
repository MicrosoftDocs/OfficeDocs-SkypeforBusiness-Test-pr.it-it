---
title: Set-CsLocationPolicy
TOCTitle: Set-CsLocationPolicy
ms:assetid: efa2840c-2e21-408e-b9fe-6f9998c81db2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412987(v=OCS.15)
ms:contentKeyID: 49302402
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsLocationPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un criterio percorso esistente. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsLocationPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsLocationPolicy [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-ConferenceMode <oneway | twoway>] [-ConferenceUri <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-EmergencyDialMask <String>] [-EmergencyDialString <String>] [-EnhancedEmergencyServiceDisclaimer <String>] [-EnhancedEmergencyServicesEnabled <$true | $false>] [-Force <SwitchParameter>] [-LocationRefreshInterval <Int64>] [-LocationRequired <yes | no | disclaimer>] [-NotificationUri <String>] [-PstnUsage <String>] [-UseLocationForE911Only <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo comando viene utilizzato il cmdlet **Set-CsLocationPolicy** per modificare il criterio percorso con valore Identity site:Redmond. In altri termini, viene modificato il criterio posizione applicato al sito Redmond. In tal caso, il comando consente di impostare su True il valore della proprietà EnhancedEmergencyServicesEnabled, che abiliterà la funzionalità E9-1-1 per tutti gli utenti connessi al sito Redmond (in questo caso).

    Set-CsLocationPolicy -Identity site:Redmond -EnhancedEmergencyServicesEnabled $True

## ESEMPIO 2

Nell'esempio 2 vengono modificati tutti i criteri percorso in uso nell'organizzazione per i quali è stato definito un URI conferenza in modo che la modalità conferenza sia impostata come bidirezionale. Per eseguire questa attività, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsLocationPolicy** per restituire una raccolta di tutti i criteri percorso attualmente definiti. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object** per circoscrivere la raccolta ai criteri percorso la cui proprietà ConferenceUri non è vuota (diversa da Null). In questo modo si ottiene una raccolta di criteri posizione che dispongono di valori ConferenceUri. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsLocationPolicy**, che modifica il valore della proprietà ConferenceMode per ogni criterio della raccolta impostando tale valore su twoway.

    Get-CsLocationPolicy | Where-Object {$_.ConferenceUri -ne $null} | Set-CsLocationPolicy -ConferenceMode twoway

## Descrizione dettagliata

Il criterio percorso consente di applicare impostazioni relative alla funzionalità per chiamate di emergenza e alla posizione del client. Determina infatti se un utente è abilitato per le chiamate di emergenza e, in tal caso, qual è il comportamento di una chiamata di emergenza. Ad esempio, è possibile utilizzare il criterio percorso per definire il numero che rappresenta una chiamata di emergenza (112 in Italia), per specificare se l'ufficio che si occupa della sicurezza aziendale deve essere avvisato automaticamente e per impostare la modalità di instradamento della chiamata. Questo cmdlet consente di modificare un criterio percorso esistente.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Set-CsLocationPolicy** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsLocationPolicy"}

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
<td><p><em>ConferenceMode</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Location.ConferenceModeEnum</p></td>
<td><p>Se viene specificato un valore per il parametro ConferenceUri, il parametro ConferenceMode determinerà se terze persone possono partecipare alla chiamata o solo ascoltare. I valori disponibili sono i seguenti:</p>
<p>- oneway: terze persone possono solo ascoltare la conversazione tra il chiamante e l'operatore del 112.</p>
<p>- twoway: terze persone possono ascoltare e partecipare alla chiamata tra il chiamante e l'operatore del 112.</p></td>
</tr>
<tr class="even">
<td><p><em>ConferenceUri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>L'URI (Uniform Resource Identifier) SIP, in questo caso il numero di telefono, di terze persone che parteciperanno alle chiamate di emergenza effettuate. Ad esempio, l'ufficio che si occupa della sicurezza aziendale potrebbe ricevere una chiamata quando viene effettuata una chiamata di emergenza e ascoltare o partecipare alla chiamata (in base al valore della proprietà ConferenceMode).</p>
<p>La stringa deve avere una lunghezza compresa tra 1 e 256 caratteri e deve iniziare con il prefisso sip:.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Una descrizione dettagliata della posizione. Ad esempio, &quot;Edificio 30, terzo piano, angolo nord-est&quot;.</p></td>
</tr>
<tr class="odd">
<td><p><em>EmergencyDialMask</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Un numero composto che viene convertito nel valore della proprietà EmergencyDialString. Ad esempio, se il valore di EmergencyDialMask è &quot;911&quot; e il valore di EmergencyDialString è &quot;112&quot;, quando un utente compone il 911, la chiamata verrà effettuata al 112. In questo modo si ha la garanzia di contattare comunque i servizi di emergenza, anche qualora un utente straniero componga un numero di emergenza alternativo specifico del proprio paese/area geografica anziché quello attivo in Italia. È possibile definire più maschere di composizione numeri di emergenza separando i diversi valori con punto e virgola, ad esempio -EmergencyDialMask &quot;212;414&quot;.</p>
<p>IMPORTANTE: accertarsi che il valore specificato come maschera di composizione non corrisponda a un numero dell'intervallo di un orbit del parcheggio di chiamata. L'instradamento del parcheggio di chiamata avrà infatti la precedenza sulla conversione delle stringhe di composizione per le chiamate di emergenza. Per visualizzare gli intervalli degli orbit del parcheggio di chiamata esistenti, chiamare il cmdlet <strong>Get-CsCallParkOrbit</strong>.</p>
<p>La lunghezza massima della stringa è 100 caratteri. Ogni carattere deve essere costituito da una cifra compresa tra 0 e 9.</p></td>
</tr>
<tr class="even">
<td><p><em>EmergencyDialString</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il numero che viene composto per chiamare i servizi di emergenza. In Italia il numero è &quot;112&quot;.</p>
<p>La stringa deve essere costituita da cifre comprese tra 0 e 9 e da una lunghezza massima di 10 caratteri.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnhancedEmergencyServiceDisclaimer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Valore di testo contenente informazioni che verranno visualizzate dagli utenti connessi da posizioni che non possono essere risolte mediante la mappatura della posizione (wiremap) che scelgono di immettere manualmente la loro posizione. Per rimuovere una dichiarazione di non responsabilità del servizio dai criteri percorso, impostare questa proprietà su un valore null:</p>
<p>-EnhancedEmergencyServiceDisclaimer $Null</p>
<p>I criteri percorso e la proprietà EnhancedEmergencyServiceDisclaimer devono essere utilizzati in Lync Server 2013 per impostare dichiarazioni di non responsabilità per il servizio E9-1-1. Questa caratteristica differisce da Lync Server 2010, dove veniva utilizzato il cmdlet Set-CsEnhancedEmergencyServiceDisclaimer per impostare una dichiarazione di non responsabilità globale per l'intera organizzazione. Utilizzando criteri percorso per impostare queste dichiarazioni di non responsabilità, è possibile creare dichiarazioni di non responsabilità diverse per le diverse impostazioni locali o per i diversi insiemi di utenti.</p></td>
</tr>
<tr class="even">
<td><p><em>EnhancedEmergencyServicesEnabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Specifica se gli utenti associati al criterio sono abilitati per la funzionalità relativa alle chiamate di emergenza. Impostare il valore su True per abilitare il servizio; i client Lync Server recupereranno le informazioni sulla posizione specificate alla registrazione e includeranno tali informazioni quando viene effettuata una chiamata di emergenza.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Un identificatore univoco del criterio percorso da modificare. Per modificare il criterio percorso globale, utilizzare un valore Global. Per un criterio creato nell'ambito del sito, tale valore avrà il formato site:&lt;nome sito&gt;, dove nome sito è il nome di un sito definito nella distribuzione di Lync Server, ad esempio site:Redmond. Per un criterio creato nell'ambito per utente, tale valore sarà semplicemente il nome del criterio, ad esempio Reno.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>LocationPolicy</p></td>
<td><p>Un riferimento all'oggetto criterio posizione. L'oggetto deve essere di tipo Microsoft.Rtc.Management.WritableConfig.Policy.Location.LocationPolicy, recuperabile chiamando il cmdlet <strong>Get-CsLocationPolicy</strong>. Recuperare l'oggetto, modificare le proprietà in memoria, quindi passare il riferimento oggetto come valore al parametro per aggiornare il criterio percorso.</p></td>
</tr>
<tr class="even">
<td><p><em>LocationRefreshInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int64</p></td>
<td><p>Specifica un periodo di tempo (in ore) tra le richieste client di aggiornamento della posiziona del servizio di informazioni sulla posizione. LocationRefreshInterval può essere impostato su qualsiasi valore da 1 a 12. Il valore predefinito è 4.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocationRequired</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Policy.Location.LocationRequiredEnum</p></td>
<td><p>Se il client non è in grado di recuperare una posizione dal database di configurazione delle posizioni, all'utente potrà essere richiesta l'immissione manuale. I valori validi per questo parametro sono i seguenti:</p>
<p>- no: all'utente non verrà richiesto di immettere la posizione. Quando viene effettuata una chiamata senza informazioni sulla posizione, il provider dei servizi di emergenza risponderà alla chiamata e richiederà la posizione.</p>
<p>- yes: all'utente verrà richiesta l'immissione delle informazioni sulla posizione quando il client registra una nuova posizione. L'utente può ignorare il prompt e non immettere alcuna informazione. Se le informazioni vengono immesse, alla chiamata effettuata al 112 risponderà innanzitutto il provider dei servizi di emergenza per verificare la posizione prima dell'instradamento all'operatore del 112.</p>
<p>- disclaimer: questa opzione è analoga all'opzione - yes, con la differenza che se l'utente ignora la richiesta, viene visualizzato il testo della dichiarazione di non responsabilità in cui vengono comunicate le conseguenze derivanti dal rifiuto di immettere le informazioni sulla posizione. Per impostare il testo della dichiarazione di non responsabilità, chiamare il cmdlet <strong>Set-CsEnhancedEmergencyServiceDisclaimer</strong>.</p>
<p>Il valore viene ignorato se EnhancedEmergencyServicesEnabled è impostato su False (impostazione predefinita). Agli utenti non verrà richiesto di immettere le informazioni sulla posizione.</p></td>
</tr>
<tr class="even">
<td><p><em>NotificationUri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Uno o più URI SIP a cui inviare una notifica quando viene effettuata una chiamata di emergenza. Ad esempio, l'ufficio che si occupa della sicurezza aziendale potrebbe ricevere una notifica tramite messaggio istantaneo ogni volta che viene effettuata una chiamata di emergenza. Se la posizione del chiamante è disponibile, verrà inclusa nella notifica.</p>
<p>È possibile includere più URI SIP in un elenco delimitato da virgole, ad esempio -NotificationUri sip:security@litwareinc.com,sip:kmyer@litwareinc.com. Notare che, con il rilascio di Lync Server 2013, è ora possibile configurare le liste di distribuzione come URI di notifica.</p>
<p>La stringa deve avere una lunghezza compresa tra 1 e 256 caratteri e deve iniziare con il prefisso sip:.</p></td>
</tr>
<tr class="odd">
<td><p><em>PstnUsage</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>L'utilizzo della rete PSTN (Public Switched Telephone Network) in base al quale verrà determinata la route vocale di cui avvalersi per instradare le chiamate al 112 dai client con questo profilo. La route associata a questo utilizzo deve puntare a un SIP trunk dedicato alle chiamate di emergenza.</p>
<p>L'utilizzo deve già esistere nell'elenco globale degli utilizzi PSTN. Per recuperare tale elenco, chiamare il cmdlet <strong>Get-CsPstnUsage</strong>. Per creare un nuovo utilizzo, chiamare il cmdlet <strong>Set-CsPstnUsage</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>UseLocationForE911Only</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Le informazioni sulla posizione possono essere utilizzate dal client Lync Server per diversi motivi, ad esempio per la notifica della posizione corrente ai membri del team. Impostare questo valore su True per assicurarsi che le informazioni sulla posizione siano disponibili per l'utilizzo con una chiamata di emergenza.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Location.LocationPolicy. Accetta l'input da pipeline di oggetti criterio percorso.

## Tipi restituiti

Questo cmdlet non restituisce un valore o un oggetto. Il cmdlet piuttosto configura le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Location.LocationPolicy.

## Vedere anche

#### Ulteriori risorse

[New-CsLocationPolicy](new-cslocationpolicy.md)  
[Remove-CsLocationPolicy](remove-cslocationpolicy.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)  
[Grant-CsLocationPolicy](grant-cslocationpolicy.md)  
[Test-CsLocationPolicy](test-cslocationpolicy.md)  
[Get-CsPstnUsage](get-cspstnusage.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)

