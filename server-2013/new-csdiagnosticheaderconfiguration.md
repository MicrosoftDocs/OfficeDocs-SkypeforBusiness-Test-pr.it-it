---
title: New-CsDiagnosticHeaderConfiguration
TOCTitle: New-CsDiagnosticHeaderConfiguration
ms:assetid: 5322e63e-c02c-4dec-8206-04f701258d6b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398350(v=OCS.15)
ms:contentKeyID: 49300537
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsDiagnosticHeaderConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta di impostazioni di configurazione delle intestazioni di diagnostica. Le impostazioni di configurazione delle intestazioni di diagnostica determinano se i messaggi SIP sono completi di informazioni di intestazione che possono essere utili nella risoluzione dei problemi e nella segnalazione di errori. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsDiagnosticHeaderConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-SendToExternalNetworks <$true | $false>] [-SendToOutsideUnauthenticatedUsers <$true | $false>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con l'esempio 1 viene creata una nuova configurazione dell'intestazione di diagnostica per il sito Redmond (-Identity site:Redmond). Oltre a specificare l'identità, il comando utilizza il parametro SendToOutsideAuthenticatedUsers e il valore di parametro $True per consentire l'invio di informazioni agli utenti autenticati esterni alla rete interna.

    New-CsDiagnosticHeaderConfiguration -Identity site:Redmond -SendToOutsideUnauthenticatedUsers $True

## ESEMPIO 2

Con i comandi riportati nell'esempio 2 viene illustrato come creare una raccolta di impostazioni delle intestazioni di diagnostica inizialmente esistenti solo in memoria. A tale scopo, il primo comando dell'esempio chiama il cmdlet **New-CsDiagnosticHeaderConfiguration** con i parametri Identity e InMemory. L'oggetto risultante viene archiviato nella variabile $x.

Dopo la creazione delle impostazioni virtuali, i comandi 2 e 3 consentono di modificare i valori delle proprietà SendToOutsideUnauthenticatedUsers e SendToExternalNetworks. Il comando 4 infine consente di trasformare le impostazioni virtuali di configurazione delle intestazioni di diagnostica in una raccolta effettiva di impostazioni applicate al sito Redmond. Questo comando finale è obbligatorio. Se non si chiama il cmdlet **Set-CsDiagnosticHeaderConfiguration**, le impostazioni non verranno applicate al sito e le impostazioni virtuali verranno eliminate al termine della sessione di Windows PowerShell o a seguito dell'eliminazione della variabile $x.

    $x = New-CsDiagnosticHeaderConfiguration -Identity site:Redmond -InMemory
    $x.SendToOutsideUnauthenticatedUsers = $True
    $x.SendToExternalNetworks = $True
    Set-CsDiagnosticHeaderConfiguration -Instance $x

## Descrizione dettagliata

Gli amministratori hanno la possibilità di allegare un'intestazione ms-diagnostic a ogni messaggio SIP inviato in un'organizzazione. Nel messaggio (non visibile per gli utenti finali) sono contenute informazioni che potrebbero essere utili nella risoluzione dei problemi di connessione o nella segnalazione di errori. Ad esempio, l'intestazione di diagnostica potrebbe includere codici di errore che consentono all'applicazione client (come Lync) di eseguire azioni predeterminate qualora si verifichi una situazione specifica.

Pochi sono i motivi per non includere le intestazioni di diagnostica per i messaggi SIP inviati entro la rete interna: hanno infatti un impatto minimo sulle dimensioni del messaggio e possono essere uno strumento davvero utile per gli amministratori che devono risolvere i problemi di connessione. Tuttavia, le intestazioni di diagnostica contengono inoltre informazioni, quali i nomi di dominio completi (FQDN) dei server SIP, che si potrebbe non voler rendere disponibili alle persone esterne alla rete interna. Per questo motivo, le impostazioni di configurazione delle intestazioni di diagnostica consentono di decidere se si desidera inviare le intestazioni agli utenti di reti esterne (ad esempio gli utenti in un dominio federato) e/o a utenti esterni. Gli utenti esterni sono quelli connessi dall'esterno della rete aziendale e che non sono ancora stati autenticati.

Per impostazione predefinita, le intestazioni di diagnostica non sono incluse in messaggi inviati a rete esterne o a utenti non autenticati. Tuttavia, è possibile modificare le impostazioni delle intestazioni di diagnostica globali per includere le intestazioni a reti esterne e/o utenti non autenticati. In alternativa, è possibile creare impostazioni personalizzate nell'ambito del sito o nell'ambito del servizio (per il server perimetrale o il servizio di registrazione). In questo modo è possibile scegliere di includere intestazioni di diagnostica nei messaggi inviati da un sito oppure tramite un server perimetrale, non consentendo invece le intestazioni nei messaggi inviati da altri siti o tramite altri server perimetrali.

Le impostazioni personalizzate dell'intestazione di diagnostica vengono create tramite il cmdlet **New-CsDiagnosticHeaderConfiguration**. Come osservato, è possibile creare le nuove impostazioni nell'ambito del sito o del servizio (ma solo per il server perimetrale e il servizio di registrazione). Occorre ricordare che è possibile disporre di una sola raccolta di tali impostazioni per sito o servizio. Ad esempio, si supponga di voler creare una nuova raccolta per il sito Redmond e che tale sito ospiti già una raccolta di impostazioni dell'intestazione di diagnostica. In tal caso, il comando avrà esito negativo. Analogamente, il comando avrà esito negativo se si tenta di creare una nuova raccolta con ambito globale.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **New-CsDiagnosticHeaderConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsDiagnosticHeaderConfiguration"}

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
<td><p>Identificatore univoco per le impostazioni di configurazione dell'intestazione di diagnostica da creare. Per creare una nuova raccolta di impostazioni nell'ambito del sito, utilizzare una sintassi simile a quella riportata di seguito: -Identity &quot;site:Redmond&quot;. Per creare una nuova raccolta di impostazioni nell'ambito del servizio, utilizzare la sintassi riportata di seguito: -Identity &quot;service:EdgeServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>Non è possibile creare nuove impostazioni nell'ambito globale. Inoltre, non è possibile creare nuove impostazioni nell'ambito del sito o del servizio se il sito o il servizio specificato (ad esempio site:Redmond) ospita già una raccolta di impostazioni.</p></td>
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
<td><p>Impedisce la visualizzazione di eventuali messaggi di errore non irreversibili che potrebbero verificarsi durante l'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>SendToExternalNetworks</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, le intestazioni di diagnostica verranno allegate ai messaggi inviati agli utenti esterni.</p></td>
</tr>
<tr class="even">
<td><p><em>SendToOutsideUnauthenticatedUsers</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se questo parametro è impostato su True, le intestazioni di diagnostica verranno allegate ai messaggi inviati agli utenti esterni, ovvero utenti che si sono connessi dall'esterno della rete interna, ad esempio tramite un server proxy, e che non sono stati ancora autenticati.</p>
<p>Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsDiagnosticHeaderConfiguration** non accetta input inviato tramite pipe.

## Tipi restituiti

Il cmdlet **New-CsDiagnosticHeaderConfiguration** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.DiagnosticHeaderSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsDiagnosticConfiguration](get-csdiagnosticconfiguration.md)  
[Remove-CsDiagnosticHeaderConfiguration](remove-csdiagnosticheaderconfiguration.md)  
[Set-CsDiagnosticHeaderConfiguration](set-csdiagnosticheaderconfiguration.md)

