---
title: Get-CsEnhancedEmergencyServiceDisclaimer
TOCTitle: Get-CsEnhancedEmergencyServiceDisclaimer
ms:assetid: b5e3a01e-4056-47a0-9c3c-efdf55a08f69
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412877(v=OCS.15)
ms:contentKeyID: 49301734
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsEnhancedEmergencyServiceDisclaimer

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera il testo della dichiarazione di non responsabilità utilizzato globalmente per richiedere informazioni sulla posizione per l'implementazione del servizio di chiamate di emergenza Enhanced 9-1-1 (E9-1-1). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsEnhancedEmergencyServiceDisclaimer [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsEnhancedEmergencyServiceDisclaimer [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Questo comando recupera il testo relativo alla dichiarazione di non responsabilità del servizio di emergenza avanzato.

    Get-CsEnhancedEmergencyServiceDisclaimer

## Descrizione dettagliata

Affinché un'implementazione di VoIP aziendale fornisca il servizio di chiamate di emergenza (E9-1-1), è necessario eseguire il mapping tra le posizioni e le porte, le subnet, i commutatori e i punti di accesso wireless per identificare la posizione del chiamante. Quando il chiamante si connette dall'esterno di uno di questi punti mappati, deve immettere manualmente la propria posizione perché venga ricevuta dai servizi di emergenza. Questo cmdlet recupera una stringa di testo che verrà visualizzata agli utenti che decidono di non immettere le informazioni sulla propria posizione. Questo messaggio verrà visualizzato solo se la proprietà LocationRequired dei criteri percorso dell'utente è impostata su Disclaimer. Per recuperare le impostazioni dei criteri percorso, è possibile chiamare il cmdlet **Get-CsLocationPolicy**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsEnhancedEmergencyServiceDisclaimer** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsEnhancedEmergencyServiceDisclaimer"}

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
<td><p>Questo parametro consente ricerche con caratteri jolly dell'identità. Poiché tuttavia l'unico valore valido per Identity è Global, questo parametro non è utile per il cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Sarà sempre Global.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera le informazioni relative alla dichiarazione di non responsabilità dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Restituisce un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Policy.Location.EnhancedEmergencyServiceDisclaimer.

## Vedere anche

#### Ulteriori risorse

[Remove-CsEnhancedEmergencyServiceDisclaimer](remove-csenhancedemergencyservicedisclaimer.md)  
[Set-CsEnhancedEmergencyServiceDisclaimer](set-csenhancedemergencyservicedisclaimer.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)

