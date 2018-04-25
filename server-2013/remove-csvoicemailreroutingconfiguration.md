---
title: Remove-CsVoicemailReroutingConfiguration
TOCTitle: Remove-CsVoicemailReroutingConfiguration
ms:assetid: 758cea84-5979-417c-a0cd-c76748e0da79
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398573(v=OCS.15)
ms:contentKeyID: 49301010
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsVoicemailReroutingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove le impostazioni che forniscono numeri di telefono PSTN (Public Switched Telephone Network) per accedere alle funzionalità Operatore automatico e Accesso sottoscrittore della Messaggistica unificata di Exchange. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsVoicemailReroutingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con questo esempio vengono rimosse le impostazioni di configurazione del reindirizzamento della segreteria telefonica per il sito Redmond1.

    Remove-CsVoicemailReroutingConfiguration -Identity site:Redmond1

## ESEMPIO 2

Con questo esempio vengono rimosse tutte le impostazioni di rerouting della segreteria telefonica per questa distribuzione di Lync Server. Il comando recupera innanzitutto tutte le impostazioni di configurazione del rerouting della segreteria telefonica chiamando il cmdlet **Get-CsVoicemailReroutingConfiguration**. Le impostazioni recuperate da questa chiamata vengono passate al cmdlet **Remove-CsVoicemailReroutingConfiguration** per l'eliminazione.

    Get-CsVoicemailReroutingConfiguration | Remove-CsVoicemailReroutingConfiguration

## Descrizione dettagliata

Questo cmdlet consente di rimuovere le impostazioni che determinano dove vengono reindirizzate su PSTN le chiamate Operatore automatico e Accesso sottoscrittore nel caso in cui venga persa la connettività IP.

Operatore automatico e Accesso sottoscrittore sono funzionalità della Messaggistica unificata di Exchange. La funzionalità Operatore automatico offre il riconoscimento vocale e il controllo DTMF per consentire ai chiamanti esterni di navigare nel sistema telefonico di una società per raggiungere il reparto o il dipendente desiderato oppure, nella modalità di sola ricezione dei messaggi, per accettare i messaggi per gli utenti. Per la modalità di sola ricezione dei messaggi è consigliato il reindirizzamento vocale. La funzionalità Accesso sottoscrittore consente agli utenti interni di accedere alla propria cassetta postale di Microsoft Outlook da un telefono. I numeri forniti da queste impostazioni consentono ai chiamanti di lasciare messaggi in segreteria telefonica per gli utenti di VoIP aziendale (impostazione AutoAttendantNumber) e agli utenti di recuperare i messaggi in segreteria anche se la connettività IP dalla distribuzione di Lync Server in un sito remoto alla Messaggistica unificata di Exchange nel data center non è disponibile (impostazione SubscriberAccessNumber).

Se si chiama questo cmdlet per rimuovere le impostazioni globali, le impostazioni saranno semplicemente riportate ai valori predefiniti.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Remove-CsVoicemailReroutingConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsVoicemailReroutingConfiguration"}

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
<td><p>Identificatore univoco della configurazione che si desidera rimuovere. Per questo cmdlet, l'identità sarà Global o Site:&lt;nome sito&gt;, dove &lt;nome sito&gt; è il nome del sito a cui sono applicate le impostazioni.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration. Consente di accettare l'input da pipeline di oggetti di configurazione del reindirizzamento della segreteria telefonica.

## Tipi restituiti

Rimuove un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.ExumRouting.VoicemailReroutingConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsVoicemailReroutingConfiguration](new-csvoicemailreroutingconfiguration.md)  
[Set-CsVoicemailReroutingConfiguration](set-csvoicemailreroutingconfiguration.md)  
[Get-CsVoicemailReroutingConfiguration](get-csvoicemailreroutingconfiguration.md)

