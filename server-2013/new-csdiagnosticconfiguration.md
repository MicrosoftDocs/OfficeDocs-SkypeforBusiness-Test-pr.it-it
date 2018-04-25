---
title: New-CsDiagnosticConfiguration
TOCTitle: New-CsDiagnosticConfiguration
ms:assetid: 9028d9c1-e812-4055-bdf0-59cb83c6f50f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398733(v=OCS.15)
ms:contentKeyID: 49301314
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsDiagnosticConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea nuove impostazioni di configurazione della diagnostica esistenti. Le impostazioni di configurazione della diagnostica vengono utilizzate per stabilire se il traffico da o verso un determinato dominio o URI (Uniform Resource Identifier) viene registrato nei file di log di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsDiagnosticConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Filter <Filter>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-LogAllSipHeaders <$true | $false>] [-LoggingShare <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene creata una nuova raccolta di impostazioni di configurazione diagnostica per il sito Redmond.

    New-CsDiagnosticConfiguration -Identity site:Redmond

## ESEMPIO 2

I comandi illustrati nell'esempio 2 creano un nuovo filtro di diagnostica e lo assegnano a una nuova raccolta di impostazioni di diagnostica. A tale scopo, nel primo comando viene chiamato il cmdlet **New-CsDiagnosticsFilter** per creare un filtro di diagnostica solo in memoria. Tramite questo comando vengono aggiunti al filtro il nome di dominio completo fabrikam.com e l'URI sip:user@fabrikam.com. Questo comando imposta inoltre la proprietà Enabled su True ($True) per attivare il filtro. Il filtro virtuale risultante viene quindi archiviato nella variabile $x.

Nel comando 2 il cmdlet **New-CsDiagnosticConfiguration** viene utilizzato per creare una nuova raccolta di impostazioni di configurazione diagnostica per il sito Redmond. Queste nuove impostazioni utilizzeranno il filtro di diagnostica archiviato nella variabile $x.

    $x = New-CsDiagnosticsFilter -Fqdn fabrikam.com -Uri "sip:user@fabrikam.com" -Enabled $False 
    
    New-CsDiagnosticConfiguration -Identity site:Redmond -Filter $x

## ESEMPIO 3

I comandi mostrati nell'esempio 3 illustrano come creare impostazioni di configurazione diagnostica che inizialmente esistono solo in memoria. A tale scopo, il primo comando chiama il cmdlet **New-CsDiagnosticConfiguration** insieme a due parametri: Identity, che specifica l'identità per le impostazioni, e InMemory, che indica che le nuove impostazioni devono essere create solo in memoria. L'oggetto risultante viene archiviato nella variabile $x.

Dopo che le impostazioni virtuali sono state create, il secondo comando viene utilizzato per configurare la proprietà LoggingShare per il percorso UNC \\\\atl-fs-001\\logs. Il comando finale viene quindi utilizzato per trasformare le impostazioni di configurazione diagnostica virtuali in una raccolta effettiva di impostazioni applicate al sito Redmond. Si noti che il comando finale è obbligatorio. Se non si chiama il cmdlet **Set-CsDiagnosticConfiguration**, non verranno applicate nuove impostazioni al sito Redmond e le impostazioni virtuali scompariranno non appena si termina la sessione di Windows PowerShell o si elimina la variabile $x.

    $x = New-CsDiagnosticConfiguration -Identity site:Redmond -InMemory
    $x.LoggingShare = "\\atl-fs-001\logs"
    Set-CsDiagnosticConfiguration -Instance $x

## Descrizione dettagliata

Se si abilita la registrazione di Lync Server, il traffico da o verso qualsiasi dominio o URI viene incluso nei file di log per impostazione predefinita. Ciò garantisce che nei file di log vengano registrate più informazioni possibili.

Tuttavia, ciò può occasionalmente causare la registrazione di troppe informazioni. Ad esempio, in caso di problemi di connettività su un particolare dominio, è opportuno limitare la registrazione del traffico tra la rete e quel dominio, in quanto ciò agevola l'identificazione delle registrazioni importanti e, di conseguenza, facilita la diagnosi e la risoluzione del problema.

Le impostazioni di configurazione diagnostica rendono possibile specificare i domini o URI da registrare nei file di log; ad esempio, è possibile registrare solo il traffico da e per domini specificati. Lync Server consente di creare impostazioni di configurazione diagnostica in ambito di sito. Ciò consente altresì di applicare impostazioni diverse, ad esempio, al sito Redmond, da quelle applicate a tutti gli altri siti.

Si noti che non è possibile creare le impostazioni di configurazione diagnostica in ambito globale, poiché l'ambito globale ospita già queste impostazioni. Allo stesso modo, non è possibile creare nuove raccolte di impostazioni in ambito di sito se quel sito già contiene impostazioni di configurazione diagnostica. Ad esempio, il comando avrà esito negativo se si tenta di creare una nuova raccolta per il sito Redmond e quel sito ospita già una raccolta di impostazioni di configurazione diagnostica.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **New-CsDiagnosticConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsDiagnosticConfiguration"}

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
<td><p>Identificatore univoco delle impostazioni di configurazione diagnostica da creare. Poiché le nuove impostazioni possono essere create solo in ambito di sito si dovrà utilizzare una sintassi simile alla seguente: -Identity &quot;site:Redmond&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.Filter</p></td>
<td><p>Raccolta di domini e URI il cui traffico sarà registrato, quando viene abilitato il filtro di diagnostica. La proprietà Filter consta di tre elementi separati:</p>
<p>Fqdn – Raccolta dei domini da includere nel filtro. Da un punto di vista più tecnico, la parte host di un indirizzo SIP. Ad esempio, un nome di dominio completo (FQDN) potrebbe essere simile al seguente: fabrikam.com. In alternativa, è possibile utilizzare i caratteri jolly per rappresentare più domini: *.fabrikam.com. È possibile includere più di un dominio in un singolo filtro.</p>
<p>Uri – Raccolta degli URI da includere nel filtro. La porzione URI è la sezione user@host di un indirizzo SIP. Un URI può essere costituito da uno qualunque dei seguenti modelli: user@fabrikam.com; user@*; *@fabrikam.com. È possibile includere più di un URI in un singolo filtro.</p>
<p>Enabled – Indica se il filtro deve essere attivato o meno.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>LogAllSipHeaders</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Se questo parametro viene impostato su False, vengono registrate solo le intestazioni SIP di base nei log. Impostando questo valore su False, è possibile ridurre le dimensioni dei file di log. Se invece questo parametro viene impostato su True, vengono registrate tutte le intestazioni SIP.</p></td>
</tr>
<tr class="odd">
<td><p><em>LoggingShare</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Cartella condivisa dove possono essere caricate le registrazioni diagnostiche.</p></td>
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

Nessuno. Il cmdlet **New-CsDiagnosticConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **New-CsDiagnosticConfiguration** crea nuove istanze di Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.DiagnosticFilterSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsDiagnosticConfiguration](get-csdiagnosticconfiguration.md)  
[New-CsDiagnosticsFilter](new-csdiagnosticsfilter.md)  
[Remove-CsDiagnosticConfiguration](remove-csdiagnosticconfiguration.md)  
[Set-CsDiagnosticConfiguration](set-csdiagnosticconfiguration.md)

