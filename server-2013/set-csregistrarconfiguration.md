---
title: Set-CsRegistrarConfiguration
TOCTitle: Set-CsRegistrarConfiguration
ms:assetid: 9616b967-09dd-470d-8d0a-acce1ff4fbf9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398764(v=OCS.15)
ms:contentKeyID: 49301376
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsRegistrarConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica i valori delle proprietà di una raccolta esistente di impostazioni di configurazione della registrazione. Le funzioni di registrazione vengono utilizzate per autenticare le richieste di accesso e per conservare le informazioni sulla disponibilità e sullo stato degli utenti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsRegistrarConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsRegistrarConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BackupStoreUnavailableThreshold <TimeSpan>] [-Confirm [<SwitchParameter>]] [-DefaultEndpointExpiration <Int32>] [-EnableDHCPServer <$true | $false>] [-Force <SwitchParameter>] [-MaxEndpointExpiration <Int32>] [-MaxEndpointsPerUser <UInt16>] [-MaxUserCount <UInt64>] [-MinEndpointExpiration <Int32>] [-PoolState <FailedOver | Active | FailingOver | FailingBack>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono modificate le impostazioni di configurazione della funzione di registrazione applicate al sito Redmond (-Identity site:Redmond). In questo esempio il valore della proprietà EnableDHCPServer viene impostato su True.

    Set-CsRegistrarConfiguration -Identity site:Redmond -EnableDHCPServer $True

## ESEMPIO 2

Nell'esempio 2 vengono modificate le impostazioni di configurazione del servizio di registrazione avanzata che supportano gli utenti con più di 8 endpoint. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsRegistrarConfiguration** senza parametri per restituire una raccolta di tutte le impostazioni di configurazione del servizio di registrazione avanzata in uso nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà MaxEndpointsPerUser è maggiore (-gt) di 8. Infine, la raccolta filtrata viene inviata tramite pipe al cmdlet **Set-CsRegistrarConfiguration**, che imposta il numero massimo di endpoint per ogni elemento della raccolta su 8.

    Get-CsRegistrarConfiguration | Where-Object {$_.MaxEndpointsPerUser -gt 8} | Set-CsRegistrarConfiguration -MaxEndpointsPerUser 8

## ESEMPIO 3

Il comando illustrato nell'esempio 3 disabilita la registrazione client tramite DHCP per ogni sito dell'organizzazione che ospita una raccolta di impostazioni di configurazione del servizio di registrazione avanzata. A tale scopo, nel comando viene chiamato il cmdlet **Get-CsRegistrarConfiguration** con il parametro Filter. Il valore di filtro "site:\*" circoscrive i dati restituiti limitandoli alle impostazioni configurate nell'ambito del sito. La raccolta viene quindi inviata tramite pipe al cmdlet **Set-CsRegistrarConfiguration**, che utilizza il parametro EnableDHCPServer con il valore $False per impedire ai client di utilizzare un server DHCP per individuare un servizio di registrazione avanzata.

    Get-CsRegistrarConfiguration -Filter "site:*"| Set-CsRegistrarConfiguration -EnableDHCPServer $False

## Descrizione dettagliata

La funzione di registrazione è forse il componente più importante di Lync Server. Dopo tutto, senza una tale funzione, gli utenti non potrebbero accedere al sistema e Lync Server non potrebbe tenere traccia degli utenti e del relativo stato corrente. Quando un utente accede a Lync Server, l'endpoint da cui l'utente sta eseguendo l'accesso invia una richiesta REGISTER alla funzione di registrazione. Il server a sua volta risponde inviando al dispositivo client una richiesta di verifica delle credenziali di autenticazione. Se il client supera la verifica della richiesta di autenticazione (presentando un set di credenziali valido), l'utente viene autenticato e le informazioni sull'endpoint (quali indirizzo IP, porta e nome utente) vengono registrate nel database di registrazione. Quando un utente si disconnette, queste informazioni vengono rimosse dal database. Tra l'accesso e la disconnessione, la funzione di registrazione mantiene aggiornate le informazioni sullo stato e aiuta a instradare i messaggi da e verso l'utente.

Le impostazioni di configurazione del servizio di registrazione sono utilizzate per gestire gli endpoint e le sottoscrizioni agli endpoint; le impostazioni possono essere applicate nell'ambito globale, del sito o del servizio. Le impostazioni nell'ambito del servizio sono utilizzate solo con il servizio di registrazione. È possibile utilizzare il cmdlet **Set-CsRegistrarConfiguration** per modificare una o tutte le raccolte di configurazioni del servizio di registrazione attualmente in uso nell'organizzazione.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Set-CsRegistrarConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsRegistrarConfiguration"}

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
<td><p><em>BackupStoreUnavailableThreshold</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Specifica l'intervallo di tempo che deve trascorrere prima che il sistema determini che l'archivio di backup non è disponibile. A questo punto verrà attivata la modalità Survivability per gli utenti. Il valore predefinito è 30 minuti (00:30:00).</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>DefaultEndpointExpiration</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>All'accesso, gli endpoint possono richiedere un timeout di scadenza, che specifica l'intervallo per cui un endpoint può rimanere connesso al sistema prima di dover contattare il server e richiedere un'estensione. La proprietà DefaultEndpointExpiration rappresenta il timeout di scadenza per i client che non richiedono un valore di timeout specifico.</p>
<p>DefaultEndpointExpiration deve essere compreso tra 300 (5 minuti) e 900 (15 minuti). Il valore predefinito è 600 (10 minuti).</p></td>
</tr>
<tr class="even">
<td><p><em>EnableDHCPServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se gli endpoint possono utilizzare i server DHCP per individuare un servizio di registrazione. Se l'impostazione è True, i client invieranno un messaggio DHCP Inform al primo avvio; il server DHCP risponderà inviando il nome di dominio completo di un servizio di registrazione utilizzabile per l'accesso dell'utente.</p></td>
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
<td><p>Identificatore univoco per le impostazioni di configurazione del servizio di registrazione da modificare. Per modificare le impostazioni globali, utilizzare la sintassi seguente: -Identity global. Per modificare le impostazioni configurate nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Per modificare le impostazioni a livello del servizio, utilizzare una sintassi simile alla seguente: -Identity service:Registrar:atl-cs-001.litwareinc.com. Le impostazioni del servizio di registrazione possono essere applicate solo al servizio stesso. Se si tenta di applicare queste impostazioni a un altro servizio viene visualizzato un messaggio di errore.</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto RegistrarSettings</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxEndpointExpiration</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>All'accesso, gli endpoint possono richiedere un timeout di scadenza, che specifica l'intervallo per cui un endpoint può rimanere connesso al sistema prima di dover contattare il server e richiedere un'estensione. La proprietà MaxEndpointExpiration rappresenta il tempo massimo che può essere concesso ai client. Ad esempio, se il tempo massimo è impostato su 600 secondi e un client richiede un intervallo di timeout di 800 secondi, al client viene assegnato il periodo di scadenza massimo, 600 secondi.</p>
<p>MaxEndpointExpiration deve essere compreso tra 300 (5 minuti) e 900 (15 minuti). Il valore predefinito è 900.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxEndpointsPerUser</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Indica il numero massimo di endpoint che un utente può avere contemporaneamente connessi al sistema. Ad esempio, un utente connesso a Lync Server sia da un computer sia da un telefono cellulare utilizza due endpoint. Il parametro MaxEndPointsPerUser deve essere impostato su un valore compreso tra 1 e 64, inclusi. Il valore predefinito è 8.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxUserCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt64</p></td>
<td><p>Indica il numero massimo di utenti che possono accedere simultaneamente a un servizio di registrazione avanzata. Il parametro MaxUserCount può essere impostato su un numero intero compreso tra 2000 e 100000, estremi inclusi. Il valore predefinito è 12000.</p></td>
</tr>
<tr class="odd">
<td><p><em>MinEndpointExpiration</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>All'accesso, gli endpoint possono richiedere un timeout di scadenza, che specifica l'intervallo per cui un endpoint può rimanere connesso al sistema prima di dover contattare il server e richiedere un'estensione. La proprietà MinEndpointExpiration rappresenta il tempo minimo che può essere concesso ai client. Ad esempio, se il tempo minimo è impostato su 600 secondi e un client richiede un intervallo di timeout di 200 secondi, al client viene assegnato il periodo di scadenza minimo, 600 secondi.</p>
<p>MinEndpointExpiration deve essere compreso tra 300 (5 minuti) e 900 (15 minuti). Il valore predefinito è 300.</p></td>
</tr>
<tr class="even">
<td><p><em>PoolState</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.WritableConfig.Settings.Registrar.PoolState</p></td>
<td><p>Stato corrente del pool di registrazione. I valori consentiti sono:</p>
<p>* Active</p>
<p>* FailedOver</p>
<p>* FailingOver</p>
<p>* FailedBack</p>
<p>Il valore predefinito è Active.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Registrar.RegistrarSettings. Il cmdlet **Set-CsRegistrarConfiguration** accetta le istanze inviate tramite pipeline dell'oggetto impostazioni per la registrazione avanzata.

## Tipi restituiti

Il cmdlet **Set-CsRegistrarConfiguration** non restituisce alcun oggetto o valore. Configura invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Registrar.RegistrarSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsRegistrarConfiguration](get-csregistrarconfiguration.md)  
[New-CsRegistrarConfiguration](new-csregistrarconfiguration.md)  
[Remove-CsRegistrarConfiguration](remove-csregistrarconfiguration.md)

