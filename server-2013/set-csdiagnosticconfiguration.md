---
title: Set-CsDiagnosticConfiguration
TOCTitle: Set-CsDiagnosticConfiguration
ms:assetid: 26463da9-cd6a-4ea3-961c-2570a8801cba
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425734(v=OCS.15)
ms:contentKeyID: 49299972
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsDiagnosticConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica impostazioni di configurazione della diagnostica esistenti. Le impostazioni di configurazione della diagnostica vengono utilizzate per stabilire se il traffico da o verso un determinato dominio o URI (Uniform Resource Identifier) viene registrato nei file di log di Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsDiagnosticConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsDiagnosticConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Filter <Filter>] [-Force <SwitchParameter>] [-LogAllSipHeaders <$true | $false>] [-LoggingShare <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

I comandi riportati nell'esempio 1 utilizzano il cmdlet **New-CsDiagnosticsFilter** per creare un nuovo filtro di diagnostica e quindi assegnano tale filtro alle impostazioni di configurazione della diagnostica globali. A tale scopo, il primo comando chiama il cmdlet **New-CsDiagnosticsFilter** per creare un filtro di diagnostica solo in memoria che utilizza l'FQDN fabrikam.com e l'URI sip:user@fabrikam.com. Questo filtro "virtuale" risultante viene quindi archiviato nella variabile $x.

Nel secondo comando viene utilizzato il cmdlet **Set-CsDiagnosticConfiguration** per assegnare il nuovo filtro alle impostazioni di configurazione della diagnostica globali. In questo caso, i valori esistenti della proprietà Filter verranno sostituiti dal nuovo filtro appena creato.

    $x = New-CsDiagnosticsFilter -Fqdn fabrikam.com -Uri sip:user@fabrikam.com 
    Set-CsDiagnosticConfiguration -Identity global -Filter $x

## ESEMPIO 2

Nell'esempio 2 viene illustrato come aggiungere un nuovo FQDN alla proprietà Filter delle impostazioni di configurazione della diagnostica globali. A tale scopo, il primo comando dell'esempio utilizza il cmdlet **Get-CsDiagnosticConfiguration** per recuperare il valore della proprietà Filter delle impostazioni globali. Questa operazione viene eseguita racchiudendo tra parentesi la chiamata al cmdlet **Get-CsDiagnosticConfiguration**. In questo modo, nell'interfaccia della riga di comando Windows PowerShell tale comando viene eseguito prima di qualunque altra operazione. Dopo che le impostazioni globali sono state restituite, il valore della proprietà Filter viene estratto e archiviato in una variabile denominata $x.

Nel secondo comando viene utilizzato il metodo Add per aggiungere un nuovo FQDN (fabrikam.com) al filtro. Successivamente, l'ultimo comando dell'esempio utilizza il cmdlet **Set-CsDiagnosticConfiguration** per salvare la raccolta di diagnostica modificata. Come risultato finale, fabrikam.com verrà aggiunto a ogni FQDN già incluso nella proprietà Filter.

    $x = (Get-CsDiagnosticConfiguration -Identity global).Filter
    $x.Fqdn.Add("fabrikam.com")
    Set-CsDiagnosticConfiguration -Identity global -Filter $x

## ESEMPIO 3

I comandi riportati nell'esempio 3 rimuovono un FQDN (fabrikam.com) dalla proprietà Filter delle impostazioni di configurazione della diagnostica globali. Il primo comando dell'esempio utilizza il cmdlet **Get-CsDiagnosticConfiguration** per recuperare il valore corrente della proprietà Filter delle impostazioni globali. Questo valore viene archiviato in una variabile denominata $x. Dopo il recupero di tale valore, viene utilizzato il metodo Remove per rimuovere l'FQDN fabrikam.com. Dopo la rimozione dell'FQDN, viene utilizzato il cmdlet **Set-CsDiagnosticConfiguration** per scrivere nelle impostazioni globali il filtro modificato, archiviato nella variabile $x.

    $x = (Get-CsDiagnosticConfiguration -Identity global).Filter
    $x.Fqdn.Remove("fabrikam.com")
    Set-CsDiagnosticConfiguration -Identity global -Filter $x

## ESEMPIO 4

Nell'esempio 4 vengono rimossi tutti gli elementi della proprietà Filter delle impostazioni di configurazione della diagnostica globali. Per ottenere questo risultato, la proprietà Filter viene impostata su un valore Null.

    Set-CsDiagnosticConfiguration -Identity global -Filter $Null

## Descrizione dettagliata

Se la registrazione di Lync Server è abilitata, il traffico da o verso un dominio o URI viene incluso nei file di log per impostazione predefinita. In questo modo nei file di log vengono registrate più informazioni possibili.

Tuttavia, ciò può occasionalmente causare la registrazione di troppe informazioni. Ad esempio, in caso di problemi di connettività su un particolare dominio, è opportuno limitare la registrazione del traffico tra la rete e quel dominio, in quanto ciò agevola l'identificazione delle registrazioni importanti e, di conseguenza, facilita la diagnosi e la risoluzione del problema.

Le impostazioni di configurazione diagnostica rendono possibile specificare i domini o URI da registrare nei file di log. Lync Server consente di creare impostazioni di configurazione diagnostica in ambito di sito. Ciò consente altresì di applicare impostazioni diverse, ad esempio al sito Redmond, da quelle applicate a tutti gli altri siti.

Il cmdlet **Set-CsDiagnosticConfiguration** può essere utilizzato anche per aggiungere o rimuovere i filtri da una determinata raccolta. I filtri vengono utilizzati per indicare i domini di cui si deve registrare il traffico.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsDiagnosticConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsDiagnosticConfiguration"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.Filter</p></td>
<td><p>Raccolta di domini e URI di cui si deve registrare il traffico. La proprietà Filter consta di tre elementi separati e deve essere creata utilizzando il cmdlet <strong>New-CsDiagnosticsFilter</strong>:</p>
<p>Fqdn - Raccolta dei domini da includere nel filtro. Da un punto di vista più tecnico, indica la parte host di un indirizzo SIP. Un nome di dominio completo (FQDN) ad esempio può essere simile al seguente: fabrikam.com. In alternativa, è possibile utilizzare i caratteri jolly per rappresentare più domini: *.fabrikam.com. È possibile includere più di un dominio in un singolo filtro.</p>
<p>Uri – Raccolta degli URI da includere nel filtro. La porzione URI è la sezione user@host di un indirizzo SIP. Un URI può essere costituito da uno qualunque dei seguenti modelli: user@fabrikam.com; user@*; *@fabrikam.com. È possibile includere più di un URI in un singolo filtro.</p>
<p>Enabled – Indica se il filtro deve essere attivato o meno.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco per le impostazioni di configurazione diagnostica da modificare. Per modificare le impostazioni configurate nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity &quot;site:Redmond&quot;. Per modificare le impostazioni globali, utilizzare la seguente sintassi: -Identity global.</p>
<p>Se questo parametro non è specificato, il cmdlet <strong>Set-CsDiagnosticConfiguration</strong> modificherà automaticamente le impostazioni globali.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto DiagnosticFilterSettings</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.DiagnosticFilterSettings. Il cmdlet **Set-CsDiagnosticConfiguration** accetta le istanze dell'oggetto impostazioni di configurazione della diagnostica inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CsDiagnosticConfiguration** non restituisce oggetti o valori. Il cmdlet invece configura le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Diagnostics.DiagnosticFilterSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsDiagnosticConfiguration](get-csdiagnosticconfiguration.md)  
[New-CsDiagnosticConfiguration](new-csdiagnosticconfiguration.md)  
[New-CsDiagnosticsFilter](new-csdiagnosticsfilter.md)  
[Remove-CsDiagnosticConfiguration](remove-csdiagnosticconfiguration.md)

