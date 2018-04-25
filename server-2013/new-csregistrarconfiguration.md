---
title: New-CsRegistrarConfiguration
TOCTitle: New-CsRegistrarConfiguration
ms:assetid: 3cd02e36-629f-4ace-841a-1064fc423cfd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425893(v=OCS.15)
ms:contentKeyID: 49300264
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsRegistrarConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova raccolta di impostazioni di configurazione della registrazione. I servizi di registrazione vengono utilizzati per autenticare richieste di accesso e per gestire informazioni sulla disponibilità e sullo stato degli utenti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsRegistrarConfiguration -Identity <XdsIdentity> [-BackupStoreUnavailableThreshold <TimeSpan>] [-Confirm [<SwitchParameter>]] [-DefaultEndpointExpiration <Int32>] [-EnableDHCPServer <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-MaxEndpointExpiration <Int32>] [-MaxEndpointsPerUser <UInt16>] [-MaxUserCount <UInt64>] [-MinEndpointExpiration <Int32>] [-PoolState <FailedOver | Active | FailingOver | FailingBack>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene creata una nuova raccolta di impostazioni di configurazione della registrazione per il sito Redmond (-Identity site:Redmond). Oltre a specificare l'identità per le nuove impostazioni, il comando imposta su 4 il numero massimo di endpoint per utente (-MaxEndpointsPerUser 4) e abilita l'utilizzo del server DHCP per la registrazione client (-EnableDHCPServer $True). Si noti che questo comando avrà esito negativo se al sito Redmond è già stata assegnata una raccolta di impostazioni di configurazione della registrazione.

    New-CsRegistrarConfiguration -Identity site:Redmond -MaxEndpointsPerUser 4 -EnableDHCPServer $True

## ESEMPIO 2

Anche i comandi riportati nell'Esempio 2 consentono di creare una nuova raccolta di impostazioni di configurazione della registrazione per il sito Redmond (-Identity site:Redmond). In questo esempio, però, le impostazioni vengono inizialmente create in memoria e solo in seguito applicate al sito.

A tale scopo, il primo comando utilizza il cmdlet **New-CsRegistrarConfiguration** per creare una nuova raccolta di impostazioni per il sito Redmond. Il parametro InMemory viene aggiunto alla fine del comando per garantire che tali impostazioni vengano create solo in memoria e non vengano immediatamente applicate al sito Redmond. Dal momento che queste impostazioni esistono solo in memoria, è necessario archiviarle in una variabile. In questo esempio è una variabile denominata $x.

Nei comandi 2 e 3 vengono modificate due proprietà di queste nuove impostazioni virtuali (MaxEndpointsPerUser e EnableDHCPServer). L'ultimo comando dell'esempio utilizza il cmdlet **Set-CsRegistrarConfiguration** per trasformare le impostazioni virtuali archiviate in $x in un gruppo effettivo di impostazioni di configurazione della funzione di registrazione applicate al sito Redmond. Se non si chiama il cmdlet **Set-CsRegistrarConfiguration**, non verranno create nuove impostazioni per il sito Redmond e le impostazioni virtuali verranno rimosse non appena si chiude la sessione di Windows PowerShell o si elimina la variabile $x.

    $x = New-CsRegistrarConfiguration -Identity site:Redmond -InMemory 
    $x.MaxEndpointsPerUser = 4 
    $x.EnableDHCPServer = $True
    Set-CsRegistrarConfiguration -Instance $x

## Descrizione dettagliata

Il servizio di registrazione è forse il componente più importante di Lync Server; infatti, senza il servizio di registrazione gli utenti non sarebbero in grado di accedere al sistema e Lync Server non sarebbe in grado di tenere traccia degli utenti e del loro stato attuale. Quando un utente accede a Lync Server, l'endpoint da cui l'utente accede invia una richiesta REGISTER al servizio di registrazione; il server, a sua volta, risponde richiedendo al dispositivo client le credenziali di autenticazione. Se il client viene accettato (cioè fornisce credenziali valide), l'utente viene autenticato e le informazioni relative all'endpoint, quali indirizzo IP, porta e nome utente, vengono salvate nel database di registrazione. Quando un utente si disconnette, queste informazioni vengono eliminate dal database. Nel periodo tra l'accesso e la disconnessione, il servizio di registrazione mantiene aggiornate le informazioni sullo stato e contribuisce all'instradamento dei messaggi da e verso l'utente.

Le impostazioni di configurazione del servizio di registrazione vengono utilizzate per gestire gli endpoint e le sottoscrizioni agli endpoint; queste impostazioni possono essere applicate in ambito globale, del sito o del servizio. Le impostazioni nell'ambito del servizio possono essere utilizzate solo per il servizio di registrazione.

Il cmdlet **New-CsRegistrarConfiguration** consente di creare nuove impostazioni di configurazione della registrazione nell'ambito del sito o del servizio. Si noti che un determinato sito o servizio può avere al massimo una raccolta di impostazioni di questo tipo; se si tenta di aggiungere una nuova raccolta a un sito o servizio che ospita già una raccolta di impostazioni di configurazione della registrazione, il comando avrà esito negativo. Il comando avrà esito negativo anche se si tenta di creare nuove impostazioni nell'ambito globale.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **New-CsRegistrarConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsRegistrarConfiguration"}

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
<td><p>Identificatore univoco delle impostazioni di configurazione della registrazione da creare. Per creare le impostazioni configurate nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Per creare le impostazioni a livello di servizio, utilizzare una sintassi simile alla seguente: -Identity service:Registrar:atl-cs-001.litwareinc.com. Si noti che ciascun sito o servizio può avere al massimo un'unica raccolta di impostazioni della registrazione. Se si tenta di creare una nuova raccolta con Identity site:Redmond per il sito Redmond e questo sito ospita già una raccolta di impostazioni della registrazione, il comando avrà esito negativo.</p>
<p>Inoltre, non è possibile creare nuove impostazioni nell'ambito globale. Se si desidera modificare i valori in ambito globale, utilizzare il cmdlet <strong>Set-CsRegistrarConfiguration</strong>.</p></td>
</tr>
<tr class="even">
<td><p><em>BackupStoreUnavailableThreshold</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Specifica l'intervallo di tempo che deve trascorrere prima che il sistema determini che l'archivio di backup non è disponibile. A questo punto verrà attivata la modalità Survivability per gli utenti. Il valore predefinito è 30 minuti (00:30:00).</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>DefaultEndpointExpiration</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Quando accedono, gli endpoint possono scegliere di richiedere un timeout di scadenza, specificando cioè un intervallo di tempo in cui l'endpoint può restare collegato al sistema prima che debba contattare il server e richiedere un'estensione. La proprietà DefaultEndpointExpiration esprime il timeout di scadenza per i client per cui non viene specificato uno intervallo particolare.</p>
<p>Il valore della proprietà DefaultEndpointExpiration deve essere compreso tra 300 (5 minuti) e 900 (15 minuti). Il valore predefinito è 600 (10 minuti).</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableDHCPServer</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Indica se gli endpoint possono utilizzare i server DHCP per individuare un server di registrazione. Se impostato su True, i client invieranno un messaggio informativo DHCP quando vengono avviati; il server DHCP risponderà inviando il nome di dominio completo (FQDN) del server di registrazione disponibile per l'accesso dell'utente.</p></td>
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
<td><p><em>MaxEndpointExpiration</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Quando accedono, gli endpoint possono scegliere di richiedere un timeout di scadenza, specificando cioè un intervallo di tempo in cui l'endpoint può restare collegato al sistema prima che debba contattare il server e richiedere un'estensione. La proprietà MaxEndpointExpiration esprime la durata massima del periodo di concessione dei client. Ad esempio, se la durata massima è impostata su 600 secondi e il client richiede un intervallo di timeout pari a 800 secondi, al client verrà assegnato il periodo di validità massimo consentito: 600 secondi.</p>
<p>Il valore della proprietà MaxEndpointExpiration deve essere compreso tra 300 (5 minuti) e 900 (15 minuti). Il valore predefinito è 900.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxEndpointsPerUser</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt16</p></td>
<td><p>Indica il numero massimo di endpoint che possono essere connessi simultaneamente al sistema per un utente. Ad esempio, un utente che ha eseguito l'accesso a Lync Server tramite computer e telefono cellulare utilizza due endpoint. La proprietà MaxEndpointsPerUser deve essere impostata su un valore compreso tra 1 e 64, estremi inclusi. Il valore predefinito è 8.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxUserCount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt64</p></td>
<td><p>Indica il numero massimo di utenti che possono essere contemporaneamente connessi a una funzione di registrazione. Il parametro MaxUserCount può essere impostato su un numero intero compreso tra 2000 e 100000, inclusi. Il valore predefinito è 12000.</p></td>
</tr>
<tr class="odd">
<td><p><em>MinEndpointExpiration</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Int32</p></td>
<td><p>Quando accedono, gli endpoint possono scegliere di richiedere un timeout di scadenza, specificando cioè un intervallo di tempo in cui l'endpoint può restare collegato al sistema prima che debba contattare il server e richiedere un'estensione. La proprietà MinEndpointExpiration esprime la durata minima del periodo di concessione dei client. Ad esempio, se la durata minima è impostata su 600 secondi e il client richiede un intervallo di timeout pari a 200 secondi, al client verrà assegnato il periodo di validità minimo consentito: 600 secondi.</p>
<p>Il valore della proprietà MinEndpointExpiration deve essere compreso tra 300 (5 minuti) e 900 (15 minuti). Il valore predefinito è 300.</p></td>
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

Nessuno. Il cmdlet **New-CsRegistrarConfiguration** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **New-CsRegistrarConfiguration** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Registrar.RegistrarSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsRegistrarConfiguration](get-csregistrarconfiguration.md)  
[Remove-CsRegistrarConfiguration](remove-csregistrarconfiguration.md)  
[Set-CsRegistrarConfiguration](set-csregistrarconfiguration.md)

