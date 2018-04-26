---
title: New-CsBandwidthPolicyServiceConfiguration
TOCTitle: New-CsBandwidthPolicyServiceConfiguration
ms:assetid: 0cb07eda-ffbe-48e2-b6bc-995737e5ba32
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398175(v=OCS.15)
ms:contentKeyID: 49299661
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsBandwidthPolicyServiceConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea una nuova configurazione del servizio dei criteri di larghezza di banda. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsBandwidthPolicyServiceConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-EnableLogging <$true | $false>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-LogCleanUpInterval <TimeSpan>] [-MaxLogFileSizeMb <UInt32>] [-MaxTokenLifetime <TimeSpan>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Questo esempio consente di creare una nuova configurazione del servizio dei criteri di larghezza di banda per il sito Redmond (-Identity site:Redmond). Non sono specificati altri parametri, per cui vengono utilizzati i valori predefiniti per tutti i valori di configurazione.

    New-CsBandwidthPolicyServiceConfiguration -Identity site:Redmond

## ESEMPIO 2

In questo esempio, viene di nuovo creata una nuova configurazione del servizio dei criteri di larghezza di banda per il sito Dublin (-Identity site:Dublin). Per questo sito, al posto dei valori predefiniti viene abilitata la registrazione e impostato il numero dei giorni, fino a 30, trascorsi i quali i log vengono cancellati. Per ottenere questo risultato, il parametro EnableLogging viene impostato su True ($True) e parametro LogCleanupInterval viene impostato su 30.00:00:00. Il valore del parametro LogCleanupInterval è un oggetto TimeSpan (durata), espresso nel formato gg.hh:mm:ss, dove g è il numero di giorni, h è il numero di ore, m è il numero di minuti e s è il numero di secondi.

    New-CsBandwidthPolicyServiceConfiguration -Identity site:Dublin -EnableLogging $True -LogCleanupInterval 30.00:00:00

## Descrizione dettagliata

Il servizio Controllo di ammissione di chiamata consente di stabilire se consentire la creazione di sessioni di comunicazioni in tempo reale, ad esempio chiamate vocali o videochiamate, sulla base dei vincoli di larghezza di banda. Nell'ambito dell'implementazione del servizio Controllo di ammissione di chiamata in Lync Server, le aree, i siti e le subnet vengono definiti all'interno di una rete insieme alle relazioni e ai collegamenti tra queste entità in modo da inserire i vincoli di larghezza di banda tra di esse. Il servizio Criteri di larghezza di banda è il componente che esegue la funzionalità Controllo di ammissione di chiamata nella distribuzione di Lync Server e che consente di stabilire se la larghezza di banda disponibile è sufficiente per eseguire la chiamata. Questo cmdlet configura un nuovo servizio di criteri di larghezza di banda a livello di sito.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **New-CsBandwidthPolicyServiceConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsBandwidthPolicyServiceConfiguration"}

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
<td><p>Un identificatore univoco che contiene l'ambito e il nome della configurazione. Questa configurazione può essere creata solo nell'ambito del sito, pertanto l'identità sarà nel formato site:&lt;nome sito&gt;, dove &lt;nome sito&gt; è il nome del sito al quale è applicata la configurazione.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableLogging</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Boolean</p></td>
<td><p>Impostare questo parametro su True per creare i log dei collegamenti e degli errori CAC relativi al servizio dei criteri di larghezza di banda.</p>
<p>Valore predefinito: False</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione delle richieste di conferma che altrimenti verrebbero visualizzate prima che vengano apportate le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="even">
<td><p><em>LogCleanUpInterval</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Il periodo di tempo trascorso il quale i log di stato dei collegamenti e degli errori CAC vengono rimossi.</p>
<p>Questo valore deve essere compreso tra 1 e 60 giorni. Il valore deve essere immesso nel formato gg.hh:mm:ss, dove g è il numero di giorni, h è il numero di ore, m è il numero di minuti e s è il numero di secondi.</p>
<p>Valore predefinito: 10 giorni (10.00:00:00)</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxLogFileSizeMb</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.UInt32</p></td>
<td><p>La dimensione massima consentita del file di log. Il valore di questo parametro deve essere un numero positivo che specifica la dimensione del file in megabyte.</p>
<p>Valore predefinito: 3 (MB)</p></td>
</tr>
<tr class="even">
<td><p><em>MaxTokenLifetime</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.TimeSpan</p></td>
<td><p>Il tempo massimo di esistenza del token emesso dal servizio di autenticazione dei criteri di larghezza di banda.</p>
<p>Questo valore deve essere compreso tra 1 e 24 ore. Il valore deve essere immesso nel formato gg.hh:mm:ss, dove g è il numero di giorni, h è il numero di ore, m è il numero di minuti e s è il numero di secondi.</p>
<p>Valore predefinito: 8 ore (08:00:00)</p></td>
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

Nessuno.

## Tipi restituiti

Consente di creare un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.BandwidthPolicyServiceConfiguration.BandwidthPolicyServiceConfiguration.

## Vedere anche

#### Ulteriori risorse

[Remove-CsBandwidthPolicyServiceConfiguration](remove-csbandwidthpolicyserviceconfiguration.md)  
[Set-CsBandwidthPolicyServiceConfiguration](set-csbandwidthpolicyserviceconfiguration.md)  
[Get-CsBandwidthPolicyServiceConfiguration](get-csbandwidthpolicyserviceconfiguration.md)

