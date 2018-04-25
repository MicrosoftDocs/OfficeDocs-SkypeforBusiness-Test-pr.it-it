---
title: Remove-CsConferenceDisclaimer
TOCTitle: Remove-CsConferenceDisclaimer
ms:assetid: 196252a1-2526-4944-9064-01d1846f3266
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398243(v=OCS.15)
ms:contentKeyID: 49299823
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConferenceDisclaimer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Cancella il testo dell'intestazione e del corpo della dichiarazione di non responsabilità relativa alle conferenze utilizzata nell'organizzazione. Tale dichiarazione è un messaggio visualizzato agli utenti che accedono a una conferenza utilizzando un collegamento ipertestuale (ad esempio, incollando un collegamento alla conferenza in un browser come Windows Internet Explorer). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsConferenceDisclaimer -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono reimpostati i valori delle proprietà della dichiarazione di non responsabilità globale. Ciò significa che l'intestazione e il corpo della dichiarazione di non responsabilità vengono impostati su valori Null e viene restituito un documento vuoto.

    Remove-CsConferenceDisclaimer -Identity global

## Descrizione dettagliata

Quando si configurano le impostazioni di conferenza, gli amministratori possono includere una dichiarazione di non responsabilità legale da visualizzare ai partecipanti nel momento in cui prendono parte alle conferenze ospitate da Lync Server. La dichiarazione di non responsabilità è generalmente utilizzata per esporre le questioni legali e le leggi sulla proprietà intellettuale relative alla conferenza. Gli utenti non possono partecipare alla conferenza senza accettare le condizioni precedentemente stabilite nella dichiarazione di non responsabilità. La dichiarazione di non responsabilità viene visualizzata solamente per gli utenti che accedono a una conferenza utilizzando un collegamento ipertestuale.

Lync Server consente una singola istanza globale della dichiarazione di non responsabilità per le conferenze. Il cmdlet **Remove-CsConferenceDisclaimer** consente di reimpostare la dichiarazione di non responsabilità per le conferenze: quando si esegue questo cmdlet, l'intestazione e il corpo della dichiarazione vengono impostati su valori Null.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Remove-CsConferenceDisclaimer** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsConferenceDisclaimer"}

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
<td><p>Identità univoca della dichiarazione di non responsabilità relativa alle conferenze da rimuovere. Sebbene sia possibile disporre solamente di un'unica istanza globale di tale dichiarazione, è comunque necessario utilizzare il parametro Identity quando si chiama il cmdlet <strong>Remove-CsConferenceDisclaimer</strong>.</p></td>
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
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer. Il cmdlet **Remove-CsConferenceDisclaimer** accetta l'input da pipeline di oggetti dichiarazione di non responsabilità per le conferenze.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsConferenceDisclaimer** invece reimposta le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer sui rispettivi valori delle proprietà predefiniti.

## Vedere anche

#### Ulteriori risorse

[Get-CsConferenceDisclaimer](get-csconferencedisclaimer.md)  
[Set-CsConferenceDisclaimer](set-csconferencedisclaimer.md)

