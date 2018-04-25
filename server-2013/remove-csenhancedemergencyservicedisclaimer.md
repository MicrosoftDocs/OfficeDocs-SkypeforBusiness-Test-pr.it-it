---
title: Remove-CsEnhancedEmergencyServiceDisclaimer
TOCTitle: Remove-CsEnhancedEmergencyServiceDisclaimer
ms:assetid: 30a5aa8c-04b8-4c1f-92b3-88c86bf69a52
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425810(v=OCS.15)
ms:contentKeyID: 49300084
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsEnhancedEmergencyServiceDisclaimer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove il testo della dichiarazione di non responsabilità utilizzato globalmente per richiedere informazioni sulla posizione per l'implementazione del servizio di chiamate di emergenza Enhanced 9-1-1 (E9-1-1). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsEnhancedEmergencyServiceDisclaimer -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Questo comando rimuove il testo della dichiarazione di non responsabilità del servizio enhanced emergency. Si noti che questo non rimuove la dichiarazione di non responsabilità globale, questa continua ad esistere. Semplicemente imposta la proprietà Body su una stringa vuota.

    Remove-CsEnhancedEmergencyServiceDisclaimer -Identity global

## Descrizione dettagliata

Affinché un'implementazione di VoIP aziendale fornisca il servizio per le chiamate di emergenza, è necessario mappare le posizioni a porte, subnet, commutatori e punti di accesso wireless per identificare la posizione del chiamante. Quando un chiamante si connette da fuori di uno di questi punti mappati, deve immettere manualmente la propria località per poter essere raggiunto dai servizio di emergenza. Questo cmdlet rimuove le stringhe di testo che vengono visualizzate agli utenti che scelgono di non immettere le informazioni sulla relativa località. Questo messaggio verrà visualizzato solo se la proprietà LocationRequired del criterio percorso dell'utente è impostata su Disclaimer. È possibile recuperare le impostazioni dei criteri percorso utilizzando il cmdlet **Get-CsLocationPolicy**. Dopo la chiamata al cmdlet, in questo caso agli utenti verrà visualizzato un messaggio vuoto.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Remove-CsEnhancedEmergencyServiceDisclaimer** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsEnhancedEmergencyServiceDisclaimer"}

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
<td><p>Questo valore è obbligatorio e deve essere impostato su Global.</p></td>
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
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Location.EnhancedEmergencyServiceDisclaimer. Accetta input tramite pipeline di un oggetto dichiarazione di non responsabilità del servizio di emergenza avanzato.

## Tipi restituiti

Questo cmdlet non restituisce alcun oggetto o valore. Consente di modificare un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Policy.Location.EnhancedEmergencyServiceDisclaimer.

## Vedere anche

#### Ulteriori risorse

[Set-CsEnhancedEmergencyServiceDisclaimer](set-csenhancedemergencyservicedisclaimer.md)  
[Get-CsEnhancedEmergencyServiceDisclaimer](get-csenhancedemergencyservicedisclaimer.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)

