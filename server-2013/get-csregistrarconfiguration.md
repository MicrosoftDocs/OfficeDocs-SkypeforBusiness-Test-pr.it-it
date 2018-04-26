---
title: Get-CsRegistrarConfiguration
TOCTitle: Get-CsRegistrarConfiguration
ms:assetid: 67f2caf6-84a8-46d8-b034-7161e9841ab8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398483(v=OCS.15)
ms:contentKeyID: 49300839
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsRegistrarConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce le informazioni sulle impostazioni di configurazione della funzione di registrazione attualmente in uso nella propria organizzazione. La funzione di registrazione viene utilizzata per autenticare richieste di accesso e per gestire informazioni sulla disponibilità e sullo stato degli utenti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsRegistrarConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsRegistrarConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 restituisce una raccolta di tutte le impostazioni di configurazione della registrazione attualmente in uso nella propria organizzazione.

    Get-CsRegistrarConfiguration

## ESEMPIO 2

L'Esempio 2 restituisce una singola raccolta di impostazioni di configurazione della registrazione: le impostazioni configurate per il sito Redmond (-Identity site:Redmond).

    Get-CsRegistrarConfiguration -Identity site:Redmond

## ESEMPIO 3

Nell'Esempio 3, vengono restituite le informazioni su tutte le impostazioni di configurazione della registrazione assegnate all'ambito del servizio. Per ottenere questo risultato, il comando utilizza il parametro Filter e il valore del filtro "service:\*"; questo valore del filtro consente di limitare i dati restituiti a quelle impostazioni la cui identità inizia con il valore di stringa "service:" inizia con la stringa "service:".

    Get-CsRegistrarConfiguration -Filter "service:*"

## ESEMPIO 4

Nell'esempio 4 vengono restituite le informazioni sulle impostazioni di configurazione della registrazione che consentono l'utilizzo di server DHCP per registrare i client. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsRegistrarConfiguration** senza alcun parametro aggiuntivo. In questo modo viene restituita una raccolta di tutte le impostazioni di configurazione della registrazione attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà EnableDHCPServer equivale a True.

    Get-CsRegistrarConfiguration | Where-Object {$_.EnableDHCPServer -eq $True}

## ESEMPIO 5

Nell'esempio 5 vengono restituite le informazioni su tutte le impostazioni di configurazione della registrazione che consentono più di otto endpoint per utente. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsRegistrarConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione della registrazione utilizzate nell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà MaxEndpointsPerUser è impostata su un valore maggiore di 8.

    Get-CsRegistrarConfiguration | Where-Object {$_.MaxEndpointsPerUser -gt 8}

## Descrizione dettagliata

La funzione di registrazione è forse il componente più importante di Lync Server. Dopo tutto, senza una tale funzione, gli utenti non potrebbero accedere al sistema e Lync Server non potrebbe tenere traccia degli utenti e del relativo stato corrente. Quando un utente accede a Lync Server, l'endpoint da cui l'utente sta eseguendo l'accesso invia una richiesta REGISTER alla funzione di registrazione. Il server a sua volta risponde inviando al dispositivo client una richiesta di verifica delle credenziali di autenticazione. Se il client supera la verifica della richiesta di autenticazione (presentando un set di credenziali valido), l'utente viene autenticato e le informazioni sull'endpoint (quali indirizzo IP, porta e nome utente) vengono registrate nel database di registrazione. Quando un utente si disconnette, queste informazioni vengono rimosse dal database. Tra l'accesso e la disconnessione, la funzione di registrazione mantiene aggiornate le informazioni sullo stato e aiuta a instradare i messaggi da e verso l'utente.

Le impostazioni di configurazione del servizio di registrazione vengono utilizzate per gestire gli endpoint e le sottoscrizioni agli endpoint; queste impostazioni possono essere applicate in ambito globale, del sito o del servizio. Le impostazioni nell'ambito del servizio possono essere utilizzate solo per il servizio di registrazione. Il cmdlet **Get-CsRegistrarConfiguration** consente di recuperare le informazioni su tutte le raccolte di configurazioni della registrazione attualmente in uso nella propria organizzazione.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsRegistrarConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsRegistrarConfiguration"}

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
<td><p>Consente di utilizzare i caratteri jolly per ottenere una o più raccolte di impostazioni di configurazione della registrazione. Ad esempio, per restituire tutte le impostazioni configurate nell'ambito del sito, utilizzare la seguente sintassi: -Filter &quot;site:*&quot;. Per restituire tutte le impostazioni configurate nell'ambito del servizio, utilizzare la seguente sintassi: -Filter &quot;service:*&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco delle impostazioni di configurazione della registrazione da ottenere. Per ottenere le impostazioni globali, utilizzare la seguente sintassi: -Identity global. Per ottenere le impostazioni configurate nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Per ottenere le impostazioni a livello di servizio, utilizzare una sintassi simile alla seguente: -Identity service:Registrar:atl-cs-001.litwareinc.com.</p>
<p>Se questo parametro non viene specificato, il cmdlet <strong>Get-CsRegistrarConfiguration</strong> restituirà tutte le impostazioni di configurazione della registrazione attualmente in uso nella propria organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati sulle impostazioni di configurazione della registrazione dalla copia locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsRegistrarConfiguration** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsRegistrarConfiguration** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Registrar.RegistrarSettings.

## Vedere anche

#### Ulteriori risorse

[New-CsRegistrarConfiguration](new-csregistrarconfiguration.md)  
[Remove-CsRegistrarConfiguration](remove-csregistrarconfiguration.md)  
[Set-CsRegistrarConfiguration](set-csregistrarconfiguration.md)

