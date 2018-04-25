---
title: New-CsVoicemailReroutingConfiguration
TOCTitle: New-CsVoicemailReroutingConfiguration
ms:assetid: 37750c6d-9b75-4dde-aa52-79210afe34c2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425849(v=OCS.15)
ms:contentKeyID: 49300206
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsVoicemailReroutingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea impostazioni che, se abilitate, forniscono numeri di telefono utilizzati da Lync Server per il routing sulla rete PSTN (Public Switched Telephone Network) qualora non sia disponibile la connettività IP tra Lync Server nel sito di succursale e il servizio Messaggistica unificata di Exchange nel data center. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsVoicemailReroutingConfiguration -Identity <XdsIdentity> [-AutoAttendantNumber <String>] [-Confirm [<SwitchParameter>]] [-Enabled <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-SubscriberAccessNumber <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con questo esempio vengono create nuove impostazioni di reindirizzamento della segreteria telefonica da applicare al sito Redmond1. Il parametro Enabled viene impostato su True per attivare la configurazione, quindi viene fornito un numero di telefono (+14255551212) per specificare l'operatore automatico a cui instradare le chiamate.

    New-CsVoicemailReroutingConfiguration -Identity site:Redmond1 -Enabled $True -AutoAttendantNumber "+14255551212"

## ESEMPIO 2

Con questo esempio vengono create nuove impostazioni di reindirizzamento della segreteria telefonica da applicare al sito Redmond1. Viene fornito un numero di telefono (+14255551213) per specificare il numero di Accesso sottoscrittore a cui instradare le chiamate. Il parametro Enabled non è stato impostato. Enabled è impostato su False per impostazione predefinita, quindi le chiamate di Accesso sottoscrittore non saranno instradate a questo numero fin quando la proprietà Enabled non viene impostata su True.

    New-CsVoicemailReroutingConfiguration -Identity site:Redmond1 -SubscriberAccessNumber "+14255551213"

## Descrizione dettagliata

Questo cmdlet consente di creare impostazioni che vengono applicate a livello globale o di sito per determinare dove vengono reinstradate su PSTN le chiamate Operatore automatico e Accesso sottoscrittore nel caso in cui venga persa la connettività IP.

Operatore automatico e Accesso sottoscrittore sono funzionalità del servizio Messaggistica unificata di Exchange. Operatore automatico fornisce il riconoscimento vocale e il controllo della composizione a toni (DTMF, Dual-Tone Multifrequency) per consentire ai chiamanti esterni di spostarsi nel sistema telefonico della società e raggiungere il dipendente o il reparto desiderato oppure, nella modalità di sola ricezione dei messaggi, di accettare messaggi per gli utenti. È consigliabile eseguire il rerouting vocale per la modalità di sola ricezione dei messaggi. Accesso sottoscrittore consente agli utenti interni di accedere alla cassetta postale di Microsoft Outlook da un telefono. I numeri forniti da queste impostazioni consentono ai chiamanti di lasciare messaggi in segreteria telefonica per gli utenti di VoIP aziendale (impostazione AutoAttendantNumber) e a tali utenti di recuperare i messaggi in segreteria telefonica anche se non è disponibile la connettività IP tra la distribuzione di Lync Server in un sito remoto e il servizio Messaggistica unificata di Exchange nel data center (impostazione SubscriberAccessNumber).

Queste impostazioni non sono disponibili, a meno che la proprietà Enabled non sia stata impostata su True.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **New-CsVoicemailReroutingConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsVoicemailReroutingConfiguration"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Questo parametro contiene un identificatore univoco che specifica l'ambito a cui viene applicata la configurazione. Le nuove configurazioni di routing della segreteria telefonica possono essere create solo a livello di sito, quindi Identity deve essere nel formato site:&lt;nome sito&gt;, dove &lt;nome sito&gt; è il nome del sito a cui sono applicate le impostazioni. Una configurazione di routing di segreteria telefonica globale è presente per impostazione predefinita e non può essere ricreata chiamando il cmdlet <strong>New-CsVoicemailReroutingConfiguration</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>AutoAttendantNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il numero di telefono dell'Operatore automatico a cui devono essere reindirizzati i tentativi di deposito dei messaggi sulla segreteria telefonica.</p>
<p>Il numero fornito a questo parametro deve essere un LineUri di un oggetto contatto esistente.</p>
<p>Il valore deve essere un numero che inizia con cifre da 1 a 9 preceduto, a propria scelta, da un segno più (+), seguito da un numero qualsiasi di cifre.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se i tentativi di accesso alla segreteria telefonica devono essere reindirizzati attraverso la rete PSTN quando la connettività IP non è attiva.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>SubscriberAccessNumber</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Il numero di accesso sottoscrittore a cui devono essere reindirizzati i tentativi di recupero dei messaggi nella segreteria telefonica.</p>
<p>Il numero fornito a questo parametro deve essere un LineUri di un oggetto contatto esistente.</p>
<p>Il valore deve essere un numero che inizia con cifre da 1 a 9 preceduto, a propria scelta, da un segno più (+), seguito da un numero qualsiasi di cifre.</p></td>
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

Nessuno.

## Tipi restituiti

Crea un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration.

## Vedere anche

#### Ulteriori risorse

[Remove-CsVoicemailReroutingConfiguration](remove-csvoicemailreroutingconfiguration.md)  
[Set-CsVoicemailReroutingConfiguration](set-csvoicemailreroutingconfiguration.md)  
[Get-CsVoicemailReroutingConfiguration](get-csvoicemailreroutingconfiguration.md)

