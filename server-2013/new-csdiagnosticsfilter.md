---
title: New-CsDiagnosticsFilter
TOCTitle: New-CsDiagnosticsFilter
ms:assetid: f1af92b1-4d1f-4eb3-9874-7fa6f6ae39c5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413009(v=OCS.15)
ms:contentKeyID: 49302431
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsDiagnosticsFilter

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo filtro di diagnostica da utilizzare con le impostazioni di configurazione della diagnostica. Tali impostazioni vengono utilizzate per stabilire se il traffico da o verso un determinato dominio o URI (Uniform Resource Identifier) viene registrato nei file di log di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsDiagnosticsFilter [-Enabled <$true | $false>] [-ExcludeConferenceMessages <$true | $false>] [-ExcludePresenceNotifications <$true | $false>] [-ExcludeRegisterMessages <$true | $false>] [-ExcludeSubscribeMessages <$true | $false>] [-ExcludeSuccessfulRequests <$true | $false>] [-Fqdn <PSListModifier>] [-Uri <PSListModifier>]

## Esempi

## ESEMPIO 1

Nei comandi mostrati nell'esempio 1 viene utilizzato il cmdlet **New-CsDiagnosticsFilter** per creare un nuovo filtro di diagnostica e assegnare tale filtro alle impostazioni globali di configurazione della diagnostica. Per eseguire tale attività, il primo comando chiama il cmdlet **New-CsDiagnosticsFilter** per creare un filtro diagnostico solo in memoria. Questo filtro aggiunge il nome di dominio completo (FQDN) fabrikam.com e l'URI user@fabrikam.com al filtro. Questo comando inoltre imposta la proprietà Enabled su True ($True) per attivare il filtro. Il filtro virtuale risultante viene quindi memorizzato nella variabile $x.

Nel secondo comando viene utilizzato il cmdlet **Set-CsDiagnosticConfiguration** per assegnare il nuovo filtro alle impostazioni globali di configurazione della diagnostica. In questo caso, i valori esistenti nella proprietà Filter verranno sostituiti dal nuovo filtro memorizzato in $x.

    $x = New-CsDiagnosticsFilter -Fqdn "fabrikam.com" -Enabled $False
    Set-CsDiagnosticConfiguration -Identity global -Filter $x 

## ESEMPIO 2

I comandi mostrati nell'esempio 2 rappresentano una variante dei comandi mostrati nell'esempio 1. Nell'esempio 2, tuttavia, i due nomi di dominio completo (fabrikam.com e contoso.com) vengono aggiunti alla proprietà Fqdn del filtro. A tal fine, entrambi i nomi (delimitati da una virgola) vengono utilizzati come valori di parametro del parametro Fqdn.

    $x = New-CsDiagnosticsFilter -Fqdn "fabrikam.com","contoso.com" -Enabled $False
    Set-CsDiagnosticConfiguration -Identity global -Filter $x

## Descrizione dettagliata

Se la registrazione di Lync Server è abilitata, il traffico da un qualsiasi dominio o URI e verso gli stessi è incluso nei file di log per impostazione predefinita. In questo modo, nei file di log viene inclusa la maggior quantità di informazioni possibile.

D'altro canto, ciò può anche comportare una quantità eccessiva di informazioni. Se ad esempio si verificano problemi di connettività con un determinato dominio, è possibile limitare la registrazione al traffico tra la rete e il dominio in questione. In questo modo risulterà più semplice identificare i record pertinenti e potrebbero pertanto essere agevolate la diagnosi e la risoluzione del problema.

Le impostazioni di configurazione della diagnostica consentono di specificare i domini o gli URI che verranno registrati nei file di log. Ad esempio, è possibile decidere di registrare solo il traffico diretto o proveniente da determinati domini. Oltre alle impostazioni globali, Lync Server consente di creare impostazioni di diagnostica nell'ambito del sito o del servizio per il server perimetrale o il servizio Registrazione avanzata. In questo modo, è possibile applicare al sito Redmond impostazioni diverse da quelle degli altri siti.

Il cmdlet **New-CsDiagnosticsFilter** consente di aggiungere un filtro a una raccolta di impostazioni di diagnostica. Questa raccolta contiene i domini e gli URI il cui traffico sarà incluso nei file di log. Quando si aggiunge un filtro, verranno registrate solo le informazioni relative ai domini e agli URI nel filtro. Ai fini della registrazione, il traffico proveniente da altri domini e URI verrà ignorato.

Il cmdlet **New-CsDiagnosticsFilter** consente di creare istanze di un filtro diagnostico solo nella memoria. Una volta creato uno di tali filtri virtuali, sarà necessario utilizzare il cmdlet **New-CsDiagnosticConfiguration** o il cmdlet **Set-CsDiagnosticConfiguration** per aggiungere il filtro a una raccolta.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **New-CsDiagnosticsFilter** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsDiagnosticsFilter"}

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
<td><p><em>Enabled</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se il filtro deve essere utilizzato o meno. Il valore predefinito è True ($True).</p></td>
</tr>
<tr class="even">
<td><p><em>ExcludeConferenceMessages</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, le informazioni relative ai messaggi di conferenza, ovvero ai messaggi con un URI conferenza nell'intestazione A o Da, non verranno registrate nei file di log. Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExcludePresenceNotifications</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, le informazioni relative alle notifiche di presenza, ovvero ai messaggi per cui viene utilizzato il metodo NOTIFY o BENOTIFY, non verranno registrate nei file di log. Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>ExcludeRegisterMessages</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se impostato su True, le informazioni relative alle registrazioni client, ovvero ai messaggi per cui viene utilizzato il metodo REGISTER, non verranno registrate nei file di log. Il valore predefinito è False.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExcludeSubscribeMessages</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se il parametro è impostato su True, le informazioni relative alle sottoscrizioni client, ovvero i messaggi per cui viene utilizzato il metodo SUBSCRIBE, non verranno registrate nei file di log. Il valore predefinito è False.</p></td>
</tr>
<tr class="even">
<td><p><em>ExcludeSuccessfulRequests</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se questo parametro viene impostato su True, nei file di log non verranno salvate le informazioni relative alle richieste SIP eseguite correttamente. Verranno salvate solo le informazioni relative alle richieste non riuscite.</p></td>
</tr>
<tr class="odd">
<td><p><em>Fqdn</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Raccolta di domini da includere nel filtro (da un punto di vista più tecnico, tali domini rappresentano la parte host di un indirizzo SIP). Per la proprietà FQDN, è possibile utilizzare un nome di dominio completo (FQDN) come il seguente: fabrikam.com. In alternativa, è possibile utilizzare i caratteri jolly per rappresentare più domini: *.fabrikam.com. È possibile includere più domini in un singolo filtro.</p></td>
</tr>
<tr class="even">
<td><p><em>Uri</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Raccolta di URI da includere nel filtro (l'URI è la parte user@host di un indirizzo SIP). Un URI può essere costituito da uno dei seguenti formati:</p>
<p>user@fabrikam.com</p>
<p>user@*</p>
<p>*@fabrikam.com</p>
<p>È possibile includere più URI in un singolo filtro.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **New-CsDiagnosticsFilter** non accetta l'input da pipeline.

## Tipi restituiti

Il cmdlet **New-CsDiagnosticsFilter** consente di creare nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.Filter.

## Vedere anche

#### Ulteriori risorse

[New-CsDiagnosticConfiguration](new-csdiagnosticconfiguration.md)  
[Set-CsDiagnosticConfiguration](set-csdiagnosticconfiguration.md)

