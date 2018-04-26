---
title: Remove-CsConferencingConfiguration
TOCTitle: Remove-CsConferencingConfiguration
ms:assetid: a3dff4b0-100b-46fa-9078-d3b0d4914d87
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412767(v=OCS.15)
ms:contentKeyID: 49301545
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsConferencingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove la raccolta specificata di impostazioni di configurazione delle conferenze. Le impostazioni di conferenza definiscono ad esempio la dimensione massima consentita per il contenuto e gli stampati delle conferenze, il periodo di tolleranza dei contenuti e gli URL per il download esterno e interno del client supportato. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsConferencingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 vengono eliminate le impostazioni di configurazione delle conferenze applicate al sito Redmond. Quando si eliminano impostazioni del sito di questo genere, gli utenti del sito ereditano automaticamente le impostazioni di configurazione delle conferenze globali.

    Remove-CsConferencingConfiguration -Identity site:Redmond

## ESEMPIO 2

Nell'esempio 2 il comando elimina tutte le impostazioni di configurazione di conferenza applicate nell'ambito del sito. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsConferencingConfiguration** insieme al parametro Filter. Il valore di filtro "site:" assicura che vengano restituite solo le impostazioni la cui identità (Identity) inizia con i caratteri "site:". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsConferencingConfiguration**, che elimina ogni elemento presente nella raccolta.

    Get-CsConferencingConfiguration -Filter site:* | Remove-CsConferencingConfiguration

## ESEMPIO 3

Nell'esempio 3 vengono eliminate tutte le impostazioni di configurazione di conferenza per le quali l'organizzazione non è impostata su Litwareinc. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsConferencingConfiguration** senza parametri. Viene restituita una raccolta di tutte le impostazioni di configurazione di conferenza utilizzate nell'organizzazione. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni con proprietà Organization diversa da Litwareinc. La raccolta filtrata viene infine inviata tramite pipe al cmdlet **Remove-CsConferencingConfiguration**, che elimina tutte le impostazioni presenti nella raccolta.

    Get-CsConferencingConfiguration | Where-Object {$_.Organization -ne "Litwareinc"} | Remove-CsConferencingConfiguration

## Descrizione dettagliata

Per le conferenze, la gestione e l'amministrazione sono suddivise in due insiemi di cmdlet. Se si desidera definire le azioni che gli utenti sono autorizzati o non autorizzati a eseguire (ad esempio invitare partecipanti anonimi a una conferenza, offrire la condivisione delle applicazioni in una conferenza, trasferire file durante una conferenza), sarà necessario utilizzare i cmdlet **CsConferencingPolicy**.

Oltre alle attività degli utenti, gli amministratori devono gestire il servizio Web Conferencing. Devono ad esempio poter eseguire operazioni quali specificare la quantità massima di spazio di archiviazione dei contenuti assegnata a una singola conferenza e specificare il periodo di tolleranza consentito prima dell'eliminazione automatica del contenuto della conferenza. Devono inoltre poter specificare le porte utilizzate per attività quali la condivisione di applicazioni e il trasferimento di file.

Queste ultime attività possono essere gestite utilizzando i cmdlet **CsConferencingConfiguration**. Questi cmdlet consentono di gestire direttamente i server. I cmdlet **CsConferencingConfiguration** infatti (che possono essere applicati agli ambiti globale, del sito e del servizio) non vengono utilizzati per specificare se un utente può condividere applicazioni durante una conferenza. Se tuttavia è abilitata la condivisione delle applicazioni, tali cmdlet consentono di indicare quali porte utilizzare per tale attività. Allo stesso modo, i cmdlet consentono di specificare aspetti quali i limiti di archiviazione e i periodi di scadenza, nonché i puntatori a URL interni ed esterni da cui gli utenti possono ottenere assistenza e risorse per le conferenze.

Il cmdlet **Remove-CsConferencingConfiguration** consente di eliminare le raccolte personalizzate delle impostazioni di configurazione di conferenza create per l'utilizzo nell'organizzazione. Quando si elimina una raccolta di impostazioni, i server che in precedenza facevano riferimento a tali impostazioni rientrano automaticamente nella raccolta successiva nella gerarchia (servizio - sito - ambito). Se le impostazioni eliminate erano applicate nell'ambito del servizio, i server verranno gestiti in base alle impostazioni del sito. Se nell'ambito del sito non è presente alcuna impostazione, i server verranno gestiti in base alle impostazioni globali. Allo stesso modo, se si eliminano le impostazioni nell'ambito del sito, i server precedentemente gestiti da tali impostazioni verranno gestiti tramite le impostazioni globali.

Si noti che è anche possibile eseguire il cmdlet **Remove-CsConferencingConfiguration** per le impostazioni globali. In questo caso tuttavia le impostazioni globali non verranno rimosse, perché Lync Server non consente di rimuovere le impostazioni globali. Verranno invece ripristinati i valori predefiniti di tutte le proprietà della raccolta globale. Se ad esempio in precedenza il valore massimo di archiviazione del contenuto è stato impostato su 200 megabyte, per questa proprietà verrà ripristinato il valore predefinito di 100 megabyte.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsConferencingConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsConferencingConfiguration"}

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
<td><p>Identificatore univoco della raccolta delle impostazioni di configurazione di conferenza da rimuovere. Per rimuovere le impostazioni configurate nell'ambito del sito, utilizzare una sintassi simile a quella riportata di seguito: -Identity &quot;site:Redmond&quot;. Per rimuovere le impostazioni configurate in ambito servizio, utilizzare una sintassi simile alla seguente: -Identity &quot;service:ConferencingServer:atl-cs-001.litwareinc.com&quot;.</p>
<p>È inoltre possibile eseguire il cmdlet <strong>Remove-CsConferencingConfiguration</strong> per le impostazioni globali. In questo caso però le impostazioni non vengono effettivamente rimosse. In realtà, per tutte le proprietà vengono ripristinate i valori predefiniti.</p></td>
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
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConfSettings. Il cmdlet **Remove-CsConferencingConfiguration** accetta istanze dell'oggetto configurazione di conferenza inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsConferencingConfiguration** elimina invece le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.WebConf.ConfSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsConferencingConfiguration](get-csconferencingconfiguration.md)  
[New-CsConferencingConfiguration](new-csconferencingconfiguration.md)  
[Set-CsConferencingConfiguration](set-csconferencingconfiguration.md)

