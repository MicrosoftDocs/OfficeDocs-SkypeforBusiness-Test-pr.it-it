---
title: Set-CsEnhancedEmergencyServiceDisclaimer
TOCTitle: Set-CsEnhancedEmergencyServiceDisclaimer
ms:assetid: 7c7f5594-4014-4ae0-afe1-6f73340be08c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398620(v=OCS.15)
ms:contentKeyID: 49301103
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsEnhancedEmergencyServiceDisclaimer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Imposta la dichiarazione di non responsabilità che verrà utilizzata globalmente per richiedere informazioni sulla posizione per l'implementazione del servizio di chiamate di emergenza (E9-1-1). Questo cmdlet è stato introdotto in Lync Server 2010. L'utilizzo del cmdlet è deprecato con Lync Server 2013. Per Lync Server 2013, le dichiarazioni di non responsabilità per E9-1-1 devono essere configurate utilizzando i cmdlet [New-CsLocationPolicy](new-cslocationpolicy.md) e [Set-CsLocationPolicy](set-cslocationpolicy.md).

## Sintassi

    Set-CsEnhancedEmergencyServiceDisclaimer [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsEnhancedEmergencyServiceDisclaimer [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Body <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene sostituito il testo della dichiarazione di non responsabilità del servizio enhanced emergency globale con il testo contenuto nella stringa fornita al parametro Body. Questa impostazione può essere applicata solo in ambito globale, che è la scelta predefinita per l'identità è che perciò non è necessario che venga specificato.

    Set-CsEnhancedEmergencyServiceDisclaimer -Body "Warning: If you do not provide a location, emergency services may be delayed in reaching your location should you need to call for help."

## Descrizione dettagliata

Affinché un'implementazione di VoIP aziendale fornisca il servizio di chiamate di emergenza, è necessario eseguire il mapping tra le posizioni e le porte, le subnet, i commutatori e i punti di accesso wireless per identificare la posizione del chiamante. Quando un chiamante si connette dall'esterno di uno di questi punti mappati, deve immettere manualmente la propria posizione per poter essere ricevuto da un servizio di emergenza. Questo cmdlet imposta le stringhe di testo che vengono mostrate agli utenti che decidono di non immettere le informazioni sulla loro posizione. Questo messaggio viene visualizzato solo se la proprietà LocationRequired dei criteri percorso dell'utente è impostata su Disclaimer. È possibile recuperare le impostazioni dei criteri percorso utilizzando il cmdlet **Get-CsLocationPolicy**.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsEnhancedEmergencyServiceDisclaimer** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsEnhancedEmergencyServiceDisclaimer"}

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
<td><p><em>Body</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Una stringa contenente informazioni che verranno mostrate agli utenti che sono connessi da località che non possono essere risolte con la mappatura (wiremap) e che scelgono di non immettere manualmente la loro località.</p></td>
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
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Sarà sempre globale.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>EnhancedEmergencyServiceDisclaimer</p></td>
<td><p>Un riferimento ad un oggetto dichiarazione di non responsabilità del servizio enhanced emergency. Deve essere di tipo EnhancedEmergencyServiceDisclaimer.</p></td>
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

[Remove-CsEnhancedEmergencyServiceDisclaimer](remove-csenhancedemergencyservicedisclaimer.md)  
[Get-CsEnhancedEmergencyServiceDisclaimer](get-csenhancedemergencyservicedisclaimer.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)

