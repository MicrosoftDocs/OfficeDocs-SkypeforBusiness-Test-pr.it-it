---
title: Get-CsDiagnosticConfiguration
TOCTitle: Get-CsDiagnosticConfiguration
ms:assetid: f642bdca-82bb-4c72-9558-7e5ec43565fd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413034(v=OCS.15)
ms:contentKeyID: 49302482
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsDiagnosticConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle impostazioni di configurazione della diagnostica attualmente in uso nell'organizzazione. Tali impostazioni vengono utilizzate per determinare se il traffico proveniente o diretto verso un determinato dominio o URI (Uniform Resource Identifier) viene registrato nei file di log di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsDiagnosticConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsDiagnosticConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono restituite tutte le impostazioni di configurazione diagnostica attualmente in uso nell'organizzazione. Questa operazione viene eseguita chiamando il cmdlet **Get-CsDiagnosticConfiguration** senza alcun parametro.

    Get-CsDiagnosticConfiguration

## ESEMPIO 2

Nell'esempio 2 vengono restituite informazioni per le impostazioni di configurazione diagnostica applicate al sito Redmond (-Identity site:Redmond).

    Get-CsDiagnosticConfiguration -Identity site:Redmond

## ESEMPIO 3

Il comando mostrato nell'esempio 3 consente di visualizzare le informazioni sui singoli filtri contenuti all'interno delle impostazioni di configurazione diagnostica relative al sito Redmond. A tale scopo, il comando utilizza per prima cosa il cmdlet **Get-CsDiagnosticConfiguration** per restituire le impostazioni di filtro del sito Redmond. Queste informazioni vengono quindi inviate tramite pipe al cmdlet **Select-Object**, che utilizza il parametro ExpandProperty per "espandere" il valore della proprietà Filter. L'espansione della proprietà Filter consente di accedere alle proprietà e ai valori proprietà dei singoli filtri gestiti nelle impostazioni di configurazione diagnostica.

    Get-CsDiagnosticConfiguration -Identity site:Redmond | Select-Object -ExpandProperty Filter

## ESEMPIO 4

Il comando mostrato nell'esempio 4 restituisce un sottoinsieme di filtri presenti nelle impostazioni di configurazione diagnostica globali; in particolare, restituisce i filtri in cui la proprietà Uri include l'indirizzo SIP sip:diagnostics@litwareinc.com. A tale scopo, il comando utilizza per prima cosa il cmdlet **Get-CsDiagnosticConfiguration** per restituire tutte le informazioni di filtro per l'istanza globale delle impostazioni di configurazione diagnostica. Le informazioni vengono quindi inviate tramite pipe al cmdlet **Select-Object**, che espande la proprietà Filter. I singoli oggetti filtro vengono quindi inviati tramite pipe al cmdlet **Select-Object**, che estrae solo quei filtri in cui la proprietà Uri contiene l'indirizzo SIP sip:diagnostics@litwareinc.com.

    Get-CsDiagnosticConfiguration -Identity global | Select-Object -ExpandProperty Filter | Where-Object {$_.Uri -contains "sip:diagnostics@litwareinc.com"}

## ESEMPIO 5

Nell'esempio 5 è riportata una variazione del comando mostrato nell'esempio 4; tuttavia, i filtri vengono restituiti solo se le relative proprietà Uri non includono l'indirizzo SIP sip:diagnostics@litwareinc.com. A tale scopo, il comando chiama il cmdlet **Get-CsDiagnosticConfiguration** per restituire tutte le informazioni di configurazione diagnostica per l'istanza globale delle impostazioni di configurazione. Le informazioni vengono quindi inviate tramite pipe al cmdlet **Select-Object**, che espande la proprietà Filter. Tali oggetti filtro vengono quindi inviati tramite pipe al cmdlet **Select-Object**, che seleziona solo quei filtri in cui la proprietà Uri non include l'indirizzo SIP sip:diagnostics@litwareinc.com.

    Get-CsDiagnosticConfiguration -Identity global | Select-Object -ExpandProperty Filter | Where-Object {$_.Uri -notcontains "sip:diagnostics@litwareinc.com"}

## Descrizione dettagliata

Se la registrazione di Lync Server è abilitata, il traffico da un qualsiasi dominio o URI e verso gli stessi è incluso nei file di log per impostazione predefinita. In questo modo, nei file di log viene inclusa la maggior quantità di informazioni possibile.

Tuttavia, è possibile che una tale quantità di informazioni risulti addirittura eccessiva. Ad esempio, se si verificano dei problemi di connettività in un determinato dominio, è possibile limitare la registrazione al traffico fra la rete e tale dominio. In questo modo risulta più semplice identificare i relativi record e, a sua volta, potrebbero essere agevolate la diagnosi e la risoluzione del problema.

Le impostazioni di configurazione diagnostica consentono di specificare i domini o URI che verranno inclusi nei file di log. Lync Server consente di creare impostazioni di configurazione diagnostica nell'ambito del sito. Ciò consente a sua volta di applicare diverse impostazioni al sito Redmond indipendentemente dagli altri siti.

Il cmdlet **Get-CsDiagnosticConfiguration** consente di restituire le informazioni sulle impostazioni di configurazione diagnostica attualmente in uso nell'organizzazione.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Get-CsDiagnosticConfiguration** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsDiagnosticConfiguration"}

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
<td><p>Consente l'utilizzo di caratteri jolly per specificare la raccolta, o le raccolte, di impostazioni che si desidera vengano restituite. Ad esempio, la sintassi che segue restituisce tutte le informazioni configurate nell'ambito del sito: -Filter &quot;site:*&quot;.</p>
<p>Si noti che non è possibile utilizzare entrambi i parametri Filter e Identity nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco delle impostazioni di configurazione diagnostica da ottenere. Per restituire le impostazioni configurate nell'ambito del sito, utilizzare la sintassi: -Identity &quot;site:Redmond&quot;. Per restituire le impostazioni globali, utilizzare la seguente sintassi: -Identity global.</p>
<p>Se il parametro non viene specificato, verranno restituite tutte le impostazioni di configurazione diagnostica attualmente in uso nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione diagnostica dalla replica locale del archivio di gestione centrale anziché dallo stesso archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsDiagnosticConfiguration** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **Get-CsDiagnosticConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.DiagnosticFilterSettings.

## Vedere anche

#### Ulteriori risorse

[New-CsDiagnosticConfiguration](new-csdiagnosticconfiguration.md)  
[Remove-CsDiagnosticConfiguration](remove-csdiagnosticconfiguration.md)  
[Set-CsDiagnosticConfiguration](set-csdiagnosticconfiguration.md)

