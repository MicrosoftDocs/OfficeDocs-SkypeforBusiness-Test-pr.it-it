---
title: Set-CsVoicemailReroutingConfiguration
TOCTitle: Set-CsVoicemailReroutingConfiguration
ms:assetid: c16a0d47-318b-46e4-991c-e4842403dbe3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412948(v=OCS.15)
ms:contentKeyID: 49301856
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsVoicemailReroutingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica le impostazioni che forniscono numeri di telefono PSTN (Public Switched Telephone Network) per accedere alle funzionalità Operatore automatico e Accesso sottoscrittore della Messaggistica unificata di Exchange. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsVoicemailReroutingConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsVoicemailReroutingConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-AutoAttendantNumber <String>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-SubscriberAccessNumber <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio viene mostrato come abilitare le impostazioni di configurazione di reindirizzamento della segreteria telefonica per il sito Redmond1.

    Set-CsVoicemailReroutingConfiguration -Identity site:Redmond1 -Enabled $True

## ESEMPIO 2

In questo esempio vengono modificate le impostazioni di reindirizzamento della segreteria telefonica che si riferiscono al sito Redmond1 configurando il numero di telefono per la funzione Accesso sottoscrittore su +14255551213.

    Set-CsVoicemailReroutingConfiguration -Identity site:Redmond1 -SubscriberAccessNumber "+14255551213"

## Descrizione dettagliata

Questo cmdlet consente di modificare le impostazioni che determinano dove vengono reinstradate le chiamate Operatore automatico e Accesso sottoscrittore quando si perde la connettività IP con un server della Messaggistica unificata di Exchange.

Operatore automatico e Accesso sottoscrittore sono funzionalità della Messaggistica unificata di Exchange. La funzionalità Operatore automatico mette a disposizione il riconoscimento vocale e il controllo a toni (multifrequenza a doppio tono o DTMF) per consentire ai chiamanti esterni di navigare nel sistema telefonico di una società al fine di raggiungere il reparto o il dipendente desiderato oppure di accettare nella modalità di sola ricezione dei messaggi per gli utenti. Per la modalità di sola ricezione è consigliato il reindirizzamento vocale. La funzionalità Accesso sottoscrittore consente agli utenti interni di accedere alla propria casella postale di Microsoft Outlook da un telefono. I numeri forniti da queste impostazioni consentono ai chiamanti di lasciare messaggi in segreteria telefonica per gli utenti di VoIP aziendale (impostazione AutoAttendantNumber) e agli utenti di recuperare i messaggi vocali anche se la connettività IP dalla distribuzione di Lync Server in un sito remoto alla Messaggistica unificata di Exchange nel data center non è disponibile (impostazione SubscriberAccessNumber).

Queste impostazioni non sono disponibili, a meno che la proprietà Enabled non sia stata impostata su True.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsVoicemailReroutingConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsVoicemailReroutingConfiguration"}

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
<td><p><em>AutoAttendantNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Il numero di telefono di Operatore automatico a cui devono essere reinstradati i tentativi di registrazione di messaggi nella segreteria telefonica.</p>
<p>Il numero fornito a questo parametro deve essere un LineUri di un oggetto contatto esistente.</p>
<p>Il valore deve essere un numero che inizia con cifre da 1 a 9 preceduto, a propria scelta, da un segno più (+), seguito da un numero qualsiasi di cifre.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Boolean</p></td>
<td><p>Indica se i tentativi di accesso alla segreteria telefonica devono essere reinstradati attraverso la rete PSTN in caso di connettività IP non attiva.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>XdsIdentity</p></td>
<td><p>L'identificatore univoco della configurazione che si desidera modificare. Per questo cmdlet, l'identità sarà Global o Site:&lt;nome sito&gt;, dove &lt;nome sito&gt; è il nome del sito a cui sono applicate le impostazioni.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>VoicemailReroutingConfiguration</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p>
<p>Questo oggetto deve essere di tipo Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration, che può essere recuperato chiamando il cmdlet <strong>Get-CsVoicemailReroutingConfiguration</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>SubscriberAccessNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>String</p></td>
<td><p>Il numero di Accesso sottoscrittore a cui devono essere reinstradati i tentativi di recupero di messaggi di segreteria telefonica.</p>
<p>Il numero fornito a questo parametro deve essere un LineUri di un oggetto contatto esistente.</p>
<p>Il valore deve essere un numero che inizia con cifre da 1 a 9 preceduto, a propria scelta, da un segno più (+), seguito da un numero qualsiasi di cifre.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration. Accetta l'input da pipeline di oggetti di configurazione del reindirizzamento della segreteria telefonica.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Modifica un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsVoicemailReroutingConfiguration](new-csvoicemailreroutingconfiguration.md)  
[Remove-CsVoicemailReroutingConfiguration](remove-csvoicemailreroutingconfiguration.md)  
[Get-CsVoicemailReroutingConfiguration](get-csvoicemailreroutingconfiguration.md)

