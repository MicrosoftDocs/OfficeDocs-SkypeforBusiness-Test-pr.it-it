---
title: New-CsClsProvider
TOCTitle: New-CsClsProvider
ms:assetid: 9b0a90c1-27ab-49c8-88f2-a381cf14625e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619187(v=OCS.15)
ms:contentKeyID: 49301453
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsClsProvider

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo provider di traccia per la registrazione centralizzata. I provider di traccia sono componenti dell'applicazione che generano messaggi di traccia o eventi di traccia utili per la risoluzione dei problemi relativi a Lync Server. Questo cmdlet è stato introdotto in Lync Server 2013.

## Sintassi

    New-CsClsProvider -Flags <String> -Level <All | Fatal | Error | Warning | Info | Verbose | Debug> -Name <String> -Type <WPP | EventLog | IISLog> [-Guid <String>] [-Role <String>]

## Esempi

## Esempio 1

I comandi mostrati nell'esempio 1 creano un nuovo provider di scenari di registrazione centralizzata e aggiungono quindi tale provider allo scenario WAC configurato per il sito Redmond. A tale scopo, il primo comando dell'esempio utilizza il cmdlet **New-CsClsProvider** per creare un nuovo provider con il nome WebInfrastructure. Il nuovo provider viene archiviato in una variabile denominata $provider. Il secondo comando nell'esempio aggiunge quindi il nuovo provider allo scenario site:Redmond/WAC. Poiché il comando utilizza la sintassi @{Add=$provider}, il nuovo provider verrà aggiunto allo scenario WAC insieme agli altri provider già configurati.

    $provider = New-CsClsProvider -Name "WebInfrastructure" -Type "WPP" -Level "Warning" -Flags "All"
    
    Set-CsClsScenario -Identity "site:Redmond/WAC" -Provider @{Add=$provider}

## Esempio 2

Il comando mostrato nell'Esempio 2 rappresenta una variazione del comando mostrato nell'Esempio 1. Nell'Esempio 2, tuttavia, il nuovo provider sostituirà tutti i provider esistenti configurati per lo scenario WAC. A tale scopo viene utilizzata la sintassi @{Replace=$provider}.

    $provider = New-CsClsProvider -Name "WebInfrastructure" -Type "WPP" -Level "Warning" -Flags "All"
    
    Set-CsClsScenario -Identity "site:Redmond/WAC" -Provider @{Replace=$provider}

## Descrizione dettagliata

Il servizio di registrazione centralizzata, che sostituisce gli strumenti OCSLogger e OCSTracer utilizzati in Microsoft Lync Server 2010, consente agli amministratori di gestire la registrazione e la traccia per tutti i computer e i pool che eseguono Lync Server 2013. La registrazione centralizzata consente agli amministratori di arrestare, avviare e configurare la registrazione per uno o più pool e computer utilizzando un solo comando. È ad esempio possibile utilizzare un comando per abilitare la registrazione del servizio Rubrica in tutti i server della Rubrica. Questo comportamento è diverso rispetto agli strumenti OCSLogger e OCSTracer, che devono essere gestiti singolarmente (avviati e arrestati individualmente) in ogni server. Il servizio di registrazione centralizzata inoltre consente agli amministratori di eseguire ricerche nei log di traccia dal comando utilizzando l' interfaccia della riga di comando Windows PowerShell e il cmdlet [Search-CsClsLogging](search-csclslogging.md).

La registrazione centralizzata si basa su una serie di scenari predefiniti che offrono un approccio più mirato alla registrazione rispetto alle versioni precedenti di Lync Server. Tali scenari prevedono componenti server e registrazione predefiniti per l'utente e di conseguenza un amministratore che abilita lo scenario RGS può essere sicuro che registrerà solo informazioni dei log rilevanti per il servizio Response Group e non, ad esempio, per il servizio del provider di servizi di audioconferenza.

Ogni scenario di registrazione centralizzata richiede uno o più provider di traccia per generare i messaggi e gli eventi registrati nei log di traccia. Lync Server 2013 viene fornito con un numero elevato di questi provider predefiniti. Il cmdlet **New-CsClsProvider** consente agli sviluppatori che estendono Lync Server di usufruire della registrazione centralizzata per una nuova applicazione o un nuovo componente personalizzato.

È anche possibile definire scenari personalizzati utilizzando il cmdlet [New-CsClsScenario](new-csclsscenario.md).

Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsClsProvider"}

Pannello di controllo di Lync Server: le funzioni eseguite dal cmdlet **New-CsClsProvider** non sono disponibili in Pannello di controllo di Lync Server.

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
<td><p><em>Flags</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Specifica i singoli protocolli e componenti secondari coinvolti nella traccia. Il provider SipStack include, ad esempio, i flag seguenti: TF_COMPONENT, TF_RTCHTTP, TF_CONNECTION, TF_DIAG.</p>
<p>La maggior parte dei provider è configurata per l'utilizzo di tutti i flag disponibili.</p></td>
</tr>
<tr class="even">
<td><p><em>Level</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLoggingConfig.ProviderLevel</p></td>
<td><p>Livello di traccia per gli eventi registrati dal provider. I valori consentiti sono:</p>
<p>* Fatal</p>
<p>* Error</p>
<p>* Warning</p>
<p>* Info</p>
<p>* Verbose</p>
<p>* Debug</p></td>
</tr>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome univoco del nuovo provider.</p></td>
</tr>
<tr class="even">
<td><p><em>Type</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLoggingConfig.ProviderType</p></td>
<td><p>Tipo di traccia utilizzato dal provider. I valori consentiti sono:</p>
<p>* WPP (Windows software trace preprocessor)</p>
<p>* EventLog</p>
<p>* IISLog</p></td>
</tr>
<tr class="odd">
<td><p><em>Guid</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Identificatore univoco globale assegnato al provider.</p></td>
</tr>
<tr class="even">
<td><p><em>Role</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Ruolo server di Lync Server per il provider, ad esempio FE per il Front End Server o Edge per il server perimetrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet New-CsClsProvider non accetta input da pipeline.

## Tipi restituiti

Il cmdlet New-CsClsProvider crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CentralizedLogging.Provider.

## Vedere anche

#### Ulteriori risorse

[New-CsClsScenario](new-csclsscenario.md)  
[Set-CsClsScenario](set-csclsscenario.md)

