---
title: Get-CsDiagnosticHeaderConfiguration
TOCTitle: Get-CsDiagnosticHeaderConfiguration
ms:assetid: a5b247b8-621a-463b-8034-f2f6970706fe
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412774(v=OCS.15)
ms:contentKeyID: 49301553
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsDiagnosticHeaderConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce le informazioni sulle impostazioni di configurazione delle intestazioni di diagnostica attualmente in uso nell'organizzazione. Tali impostazioni determinano se i messaggi SIP sono corredati da informazioni di intestazione. Queste informazioni possono essere utili per la risoluzione dei problemi e la segnalazione degli errori. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsDiagnosticHeaderConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsDiagnosticHeaderConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Il comando precedente restituisce informazioni su tutte le impostazioni di configurazione delle intestazioni di diagnostica attualmente in uso nell'organizzazione. A tale scopo, viene chiamato il cmdlet **Get-CsDiagnosticHeaderConfiguration** senza alcun parametro.

    Get-CsDiagnosticHeaderConfiguration

## ESEMPIO 2

Nell'esempio 2 viene restituita un'unica raccolta di impostazioni di configurazione delle intestazioni di diagnostica: la raccolta con Identity site:Redmond.

    Get-CsDiagnosticHeaderConfiguration -Identity site:Redmond

## ESEMPIO 3

Il comando mostrato nell'esempio 3 restituisce tutte impostazioni delle intestazioni di diagnostica configurate nell'ambito del servizio. A tale scopo, viene chiamato il cmdlet **Get-CsDiagnosticHeaderConfiguration** con il parametro Filter. Il valore di filtro "service:\*" garantisce che vengano restituite solo le impostazioni con un'identità (Identity) che inizia con i caratteri "service:".

    Get-CsDiagnosticHeaderConfiguration -Filter "service:*"

## ESEMPIO 4

Nell'esempio 4 vengono restituite tutte le impostazioni di configurazione delle intestazioni di diagnostica che consentono l'invio delle intestazioni alle reti esterne. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsDiagnosticHeaderConfiguration** senza alcun parametro. In questo modo viene restituita una raccolta di tutte le impostazioni delle intestazioni di diagnostica attualmente in uso nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona unicamente le impostazioni con proprietà SendToExternalNetworks uguale a True.

    Get-CsDiagnosticHeaderConfiguration | Where-Object {$_.SendToExternalNetworks -eq $True}

## ESEMPIO 5

Il comando mostrato nell'esempio 5 restituisce informazioni sulle impostazioni di configurazione delle intestazioni di diagnostica che soddisfano almeno uno dei criteri seguenti: 1) la proprietà SendToExternalNetworks è uguale a True e/o 2) la proprietà SendToOutsideUnauthenticatedUsers è uguale a True. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsDiagnosticHeaderConfiguration** per restituire una raccolta di tutte le impostazioni delle intestazioni di diagnostica attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona le impostazioni con proprietà SendToExternalNetworks e/o SendToOutsideUnauthenticatedUsers uguali a True.

L'operatore -or indica che per essere restituite le impostazioni devono soddisfare solo uno dei criteri specificati. Se si desidera che le impostazioni soddisfino entrambi i criteri specificati, utilizzare piuttosto l'operatore -and:

Where-Object {$\_.SendToExternalNetworks -eq $True -and $\_.SendToOutsideUnauthenticatedUsers -eq $True}

    Get-CsDiagnosticHeaderConfiguration | Where-Object {$_.SendToExternalNetworks -eq $True -or $_.SendToOutsideUnauthenticatedUsers -eq $True}

## Descrizione dettagliata

Quando si inviano messaggi SIP (Session Initiation Protocol), si ha la possibilità di allegare un'intestazione di diagnostica Ms a ogni messaggio. In tale messaggio (non visibile agli utenti finali) sono incluse informazioni che potrebbero essere utili nella risoluzione dei problemi di connessione o nella segnalazione di errori. L'intestazione di diagnostica può ad esempio includere codici di errore che consentono all'applicazione client (come Lync 2013) di eseguire azioni predeterminate nel caso in cui si verifichi una situazione specifica.

Pochi sono i motivi per non includere le intestazioni di diagnostica per i messaggi SIP inviati entro la rete interna: hanno infatti un impatto minimo sulle dimensioni del messaggio e possono essere uno strumento davvero utile per gli amministratori che devono risolvere i problemi di connessione. È tuttavia possibile che nelle intestazioni di diagnostica siano contenute anche informazioni, quali i nomi di dominio completo (FQDN) dei server SIP, che non si desidera rendere disponibili per le persone al di fuori della rete interna. Per questo motivo, le impostazioni di configurazione delle intestazioni di diagnostica consentono di decidere se inviare tali intestazioni agli utenti di reti esterne (ad esempio utenti in un dominio federato) e/o a utenti esterni. Per utenti esterni si intendono gli utenti che non effettuano la connessione dalla rete interna e che non sono stati ancora autenticati.

Per impostazione predefinita, le intestazioni non sono incluse in messaggi inviati a rete esterne o a utenti non autenticati. Tuttavia, è possibile modificare le impostazioni delle intestazioni di diagnostica globali per includere le intestazioni a reti esterne e/o utenti non autenticati. In alternativa, è possibile creare impostazioni personalizzate nell'ambito del sito o nell'ambito del servizio (per il server perimetrale o il servizio di registrazione). In questo modo è possibile scegliere di includere intestazioni di diagnostica nei messaggi inviati da un sito oppure tramite un server perimetrale, non consentendo invece le intestazioni nei messaggi inviati da altri siti o tramite altri server perimetrali.

Il cmdlet **Get-CsDiagnosticHeaderConfiguration** consente di recuperare le informazioni sulle impostazioni di configurazione delle intestazioni di diagnostica attualmente in uso nell'organizzazione.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsDiagnosticHeaderConfiguration** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsDiagnosticHeaderConfiguration"}

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
<td><p>Consente l'utilizzo di caratteri jolly per specificare la raccolta, o le raccolte, di impostazioni che si desidera vengano restituite. Ad esempio, la sintassi che segue restituisce tutte le informazioni configurate nell'ambito del sito: -Filter &quot;site:*&quot;. La seguente sintassi restituisce tutte le impostazioni configurate nell'ambito del servizio: -Filter &quot;service:*&quot;.</p>
<p>Si noti che non è possibile utilizzare entrambi i parametri Filter e Identity nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per le impostazioni di configurazione delle intestazioni di diagnostica da restituire. Per restituire le impostazioni configurate nell'ambito del sito, utilizzare la sintassi: -Identity &quot;site:Redmond&quot;. Per le impostazioni configurate con ambito servizio, utilizzare la sintassi: -Identity &quot;service:EdgeServer:atl-edge-001.litwareinc.com&quot;. Per restituire le impostazioni globali, utilizzare la seguente sintassi: -Identity global.</p>
<p>Se il parametro non viene specificato, verranno restituite tutte le impostazioni di configurazione delle intestazioni di diagnostica attualmente in uso nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera i dati di configurazione dell'intestazione di diagnostica dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsDiagnosticHeaderConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsDiagnosticHeaderConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.DiagnosticHeaderSettings.

## Vedere anche

#### Ulteriori risorse

[New-CsDiagnosticHeaderConfiguration](new-csdiagnosticheaderconfiguration.md)  
[Remove-CsDiagnosticHeaderConfiguration](remove-csdiagnosticheaderconfiguration.md)  
[Set-CsDiagnosticHeaderConfiguration](set-csdiagnosticheaderconfiguration.md)

