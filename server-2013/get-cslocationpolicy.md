---
title: Get-CsLocationPolicy
TOCTitle: Get-CsLocationPolicy
ms:assetid: d338af1b-3865-4010-a7fc-d5841c515ae6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398911(v=OCS.15)
ms:contentKeyID: 49302075
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsLocationPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni su come è stato eventualmente configurato il servizio Informazioni percorso per le chiamate di emergenza Enhanced 9-1-1 (E9-1-1). Questo servizio consente agli operatori che rispondono alle chiamate di emergenza di determinare la posizione geografica del chiamante. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsLocationPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsLocationPolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene restituita una raccolta di tutti i criteri di identificazione della posizione attualmente in uso nell'organizzazione, semplicemente chiamando il cmdlet **Get-CsLocationPolicy** senza specificare alcun parametro.

    Get-CsLocationPolicy

## ESEMPIO 2

Il comando mostrato nell'esempio 2 restituisce solo quei criteri di identificazione della posizione il cui valore Identity è uguale a Reno. Poiché le identità devono essere univoche, il comando restituirà al massimo un criterio di identificazione della posizione.

    Get-CsLocationPolicy -Identity Reno

## ESEMPIO 3

Nell'esempio 3 viene utilizzato il parametro Filter per restituire tutti i criteri di identificazione della posizione configurati con ambito per utente. I criteri configurati creati con ambito per utente possono essere assegnati direttamente a utenti e siti della rete. La stringa con carattere jolly tag:\* indica al cmdlet **Get-CsLocationPolicy** di limitare i dati restituiti ai criteri percorso con valore Identity che inizia con il valore stringa tag:. Sebbene non occorra specificare il prefisso tag: quando si recupera un singolo criterio, è possibile utilizzare tale prefisso per applicare un filtro a tutti i criteri per utente.

    Get-CsLocationPolicy -Filter tag:*

## ESEMPIO 4

Nell'esempio 4 viene restituita una raccolta di tutti i criteri percorso con servizi di chiamate di emergenza disabilitati. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsLocationPolicy** per restituire una raccolta di tutti i criteri percorso attualmente in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**. A sua volta, il cmdlet **Where-Object** applica un filtro per limitare i dati restituiti ai criteri con proprietà EnhancedEmergencyServicesEnabled uguale a (-eq) False ($False).

    Get-CsLocationPolicy | Where-Object {$_.EnhancedEmergencyServicesEnabled -eq $False}

## Descrizione dettagliata

Il criterio percorso viene utilizzato per applicare le impostazioni relative alla funzionalità del servizio di chiamate di emergenza. Il criterio percorso determina se un utente è abilitato per le chiamate di emergenza e, in tal caso, qual è il comportamento di una chiamata di emergenza. Ad esempio, è possibile utilizzare il criterio percorso per definire i numeri che rappresentano una chiamata di emergenza (113 in Italia), per definire se inviare o meno una notifica all'ufficio di sicurezza aziendale, la modalità di instradamento della chiamata e così via. Questo cmdlet recupera uno o più criteri di identificazione della posizione.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Get-CsLocationPolicy** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsLocationPolicy"}

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
<td><p>Una stringa contenente caratteri jolly che recupererà criteri di identificazione della posizione in base alla corrispondenza del valore Identity del criterio alla stringa jolly.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>L'identificatore univoco del criterio di identificazione della posizione che si desidera recuperare. Per recuperare un criterio percorso globale, utilizzare il valore Global. Per un criterio creato nell'ambito del sito, il valore avrà il formato site:&lt;nome sito&gt;, dove nome sito è il nome di un sito definito nella distribuzione di Lync Server, ad esempio site:Redmond. Per un criterio creato nell'ambito per utente, il valore corrisponderà semplicemente al nome del criterio, ad esempio Reno.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera le informazioni relative al criterio percorso dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Il cmdlet **Get-CsLocationPolicy** restituisce le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Location.LocationPolicy.

## Vedere anche

#### Ulteriori risorse

[New-CsLocationPolicy](new-cslocationpolicy.md)  
[Remove-CsLocationPolicy](remove-cslocationpolicy.md)  
[Set-CsLocationPolicy](set-cslocationpolicy.md)  
[Grant-CsLocationPolicy](grant-cslocationpolicy.md)  
[Test-CsLocationPolicy](test-cslocationpolicy.md)

