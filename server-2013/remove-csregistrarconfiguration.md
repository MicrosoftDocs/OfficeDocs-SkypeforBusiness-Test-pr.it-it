---
title: Remove-CsRegistrarConfiguration
TOCTitle: Remove-CsRegistrarConfiguration
ms:assetid: 67ee01a1-fdfe-4994-b03a-57a332aa45be
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398482(v=OCS.15)
ms:contentKeyID: 49300837
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsRegistrarConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una raccolta esistente di impostazioni di configurazione della registrazione. I servizi di registrazione vengono utilizzati per autenticare richieste di accesso e per gestire informazioni sulla disponibilità e sullo stato degli utenti. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsRegistrarConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di eliminare le impostazioni di configurazione della registrazione assegnate al sito Redmond. Quando queste impostazioni vengono eliminate, le registrazioni del sito Redmond utilizzeranno automaticamente le impostazioni di registrazione globali.

    Remove-CsRegistrarConfiguration -Identity site:Redmond

## ESEMPIO 2

Nell'esempio 2 vengono eliminate tutte impostazioni di configurazione della registrazione avanzata assegnate all'ambito del servizio. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsRegistrarConfiguration** e il parametro Filter. Il valore di filtro "service:\*" restituisce solo i dati relativi alle impostazioni la cui identità (Identity) inizia con i caratteri "service:" La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsRegistrarConfiguration**, che elimina ogni elemento della raccolta.

    Get-CsRegistrarConfiguration -Filter "service:*" | Remove-CsRegistrarConfiguration

## ESEMPIO 3

Nell'esempio 3 vengono eliminate tutte le impostazioni di configurazione della registrazione nelle quali la proprietà EnableDHCPServer è impostata su True. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsRegistrarConfiguration** senza alcun parametro aggiuntivo. In questo modo viene restituita una raccolta di tutte le impostazioni di configurazione della registrazione attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà EnableDHCPServer equivale a True. Questa raccolta filtrata viene a sua volta inviata tramite pipe al cmdlet **Remove-CsRegistrarConfiguration**, che elimina ogni elemento della raccolta.

    Get-CsRegistrarConfiguration | Where-Object {$_.EnableDHCPServer -eq $True} | Remove-CsRegistrarConfiguration

## Descrizione dettagliata

La funzione di registrazione è forse il componente più importante di Lync Server. Dopo tutto, senza una tale funzione, gli utenti non potrebbero accedere al sistema e Lync Server non potrebbe tenere traccia degli utenti e del relativo stato corrente. Quando un utente accede a Lync Server, l'endpoint da cui l'utente sta eseguendo l'accesso invia una richiesta REGISTER alla funzione di registrazione. Il server a sua volta risponde inviando al dispositivo client una richiesta di verifica delle credenziali di autenticazione. Se il client supera la verifica della richiesta di autenticazione (presentando un set di credenziali valido), l'utente viene autenticato e le informazioni sull'endpoint (quali indirizzo IP, porta e nome utente) vengono registrate nel database di registrazione. Quando un utente si disconnette, queste informazioni vengono rimosse dal database. Tra l'accesso e la disconnessione, la funzione di registrazione mantiene aggiornate le informazioni sullo stato e aiuta a instradare i messaggi da e verso l'utente.

Le impostazioni di configurazione del servizio di registrazione vengono utilizzate per gestire gli endpoint e le sottoscrizioni agli endpoint; queste impostazioni possono essere applicate in ambito globale, del sito o del servizio. Le impostazioni nell'ambito del servizio possono essere utilizzate solo per il servizio di registrazione.

Il cmdlet **Remove-CsRegistrarConfiguration** consente di rimuovere le impostazioni di configurazione della registrazione applicate nell'ambito del sito o del servizio. Si noti che in realtà nessuna delle registrazioni viene eliminata o disinstallata; più semplicemente, vengono rimosse le impostazioni di configurazione che regolano quelle registrazioni. Se queste impostazioni non esistono nell'ambito del sito o del servizio, la registrazione verrà gestita utilizzando le impostazioni globali.

È possibile eseguire il cmdlet **Remove-CsRegistrarConfiguration** anche per le impostazioni di configurazione della registrazione globali. In questo caso tuttavia le impostazioni non verranno rimosse, in quanto non è possibile eliminare le impostazioni globali. Per tutte le proprietà di tale raccolta globale verranno ripristinati i valori predefiniti. Se a esempio per la proprietà MinEndpointExpiration è stato specificato il valore 500, verrà reimpostato al valore predefinito 300.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Remove-CsRegistrarConfiguration** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsRegistrarConfiguration e"}

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
<td><p>Identificatore univoco delle impostazioni di configurazione della registrazione da rimuovere. Per rimuovere le impostazioni configurate nell'ambito del sito, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Per rimuovere le impostazioni a livello di servizio, utilizzare una sintassi simile alla seguente: -Identity service:Registrar:atl-cs-001.litwareinc.com.</p>
<p>Si noti che è possibile eseguire il cmdlet <strong>Remove-CsRegistrarConfiguration</strong> anche per le impostazioni globali (-identity global). In questo caso tuttavia le impostazioni globali non verranno rimosse, ma verranno ripristinati i valori predefiniti di tutte le proprietà della raccolta globale.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Registrar.RegistrarSettings. Il cmdlet **Remove-CsRegistrarConfiguration** accetta le istanze inviate tramite pipeline dell'oggetto impostazioni per la registrazione avanzata.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsRegistrarConfiguration** invece elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.Registrar.RegistrarSettings.

## Vedere anche

#### Ulteriori risorse

[Get-CsRegistrarConfiguration](get-csregistrarconfiguration.md)  
[New-CsRegistrarConfiguration](new-csregistrarconfiguration.md)  
[Set-CsRegistrarConfiguration](set-csregistrarconfiguration.md)

