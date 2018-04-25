---
title: Get-CsConferenceDisclaimer
TOCTitle: Get-CsConferenceDisclaimer
ms:assetid: 2382aaef-9c5e-43f8-99de-6c880134db7d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425714(v=OCS.15)
ms:contentKeyID: 49299936
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsConferenceDisclaimer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulla dichiarazione di non responsabilità per le conferenze in uso nell'organizzazione. Tale dichiarazione è un messaggio visualizzato agli utenti che accedono a una conferenza utilizzando un collegamento ipertestuale (ad esempio, incollando un collegamento alla conferenza in un browser come Windows Internet Explorer). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsConferenceDisclaimer [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsConferenceDisclaimer [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Con il comando mostrato nell'esempio 1 vengono restituite le informazioni sulla dichiarazione di non responsabilità per la conferenza configurata per l'uso nell'organizzazione. Dal momento che è necessario limitarsi a una singola dichiarazione di non responsabilità (configurata nell'ambito globale), non è necessario specificare un'identità durante l'esecuzione di questo comando.

    Get-CSConferenceDisclaimer

## Descrizione dettagliata

Quando si configurano le impostazioni di conferenza, gli amministratori possono includere una dichiarazione di non responsabilità legale da visualizzare ai partecipanti nel momento in cui prendono parte alle conferenze ospitate da Lync Server. Questa dichiarazione è generalmente utilizzata per esporre le questioni legali e le leggi sulla proprietà intellettuale relative alla conferenza. Gli utenti non possono partecipare alla conferenza senza accettare le condizioni precedentemente stabilite nella dichiarazione di non responsabilità. La dichiarazione di non responsabilità viene visualizzata solamente per gli utenti che accedono a una conferenza utilizzando un collegamento ipertestuale.

Il cmdlet **Get-CsConferenceDisclaimer** consente di visualizzare il corpo e l'intestazione della dichiarazione di non responsabilità dell'organizzazione.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Get-CsConferenceDisclaimer** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsConferenceDisclaimer"}

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare i valori dei caratteri jolly nel riferimento a una dichiarazione di non responsabilità per le conferenze. Dal momento che è possibile disporre di una singola istanza globale della dichiarazione di non responsabilità per le conferenze, non c'è motivo di utilizzare il parametro Filter. Tuttavia, è possibile utilizzare la sintassi riportata di seguito per referenziare la dichiarazione di non responsabilità globale: -Filter &quot;g*&quot;. Questa sintassi recupera tutte le dichiarazioni di non responsabilità per le conferenze la cui identità inizia con la lettera &quot;g&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identità univoca della dichiarazione di non responsabilità per le conferenze. Dal momento che è possibile disporre di una singola istanza globale di tale dichiarazione, non è necessario specificare un'identità nella chiamata al cmdlet <strong>Get-CsConferenceDisclaimer</strong>. È tuttavia possibile utilizzare la sintassi seguente per fare riferimento alla dichiarazione di non responsabilità globale: -Identity global.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati della dichiarazione di non responsabilità per le conferenze dalla replica locale del archivio di gestione centrale anziché dal archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Il cmdlet **Get-CsConferenceDisclaimer** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConferenceDisclaimer.

## Vedere anche

#### Ulteriori risorse

[Remove-CsConferenceDisclaimer](remove-csconferencedisclaimer.md)  
[Set-CsConferenceDisclaimer](set-csconferencedisclaimer.md)

