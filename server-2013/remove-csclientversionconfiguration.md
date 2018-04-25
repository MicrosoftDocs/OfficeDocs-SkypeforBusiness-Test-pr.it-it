---
title: Remove-CsClientVersionConfiguration
TOCTitle: Remove-CsClientVersionConfiguration
ms:assetid: 42065d1d-a0ef-4fa4-826b-d65b14b343c9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425925(v=OCS.15)
ms:contentKeyID: 49300345
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsClientVersionConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove la raccolta specificata delle impostazioni di configurazione della versione del client. Le impostazioni di configurazione della versione del client determinano se Lync Server verifica il numero di versione di ogni applicazione client che accede al sistema. Se il filtro versione client è abilitato, la capacità dell'applicazione client di accedere al sistema dipenderà dalle impostazioni configurate nel criterio di versione client appropriato. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsClientVersionConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 consente di eliminare le impostazioni di configurazione della versione client con Identity "site:Redmond".

    Remove-CsClientVersionConfiguration -Identity site:Redmond

## ESEMPIO 2

Nell'esempio 2 vengono eliminate tutte le impostazioni di configurazione della versione client applicate nell'ambito del sito. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsClientVersionConfiguration** e il parametro Filter. Il valore di filtro "site:\*" garantisce la restituzione delle sole impostazioni di configurazione della versione client la cui identità inizia con il valore stringa "site:". La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsClientVersionConfiguration**, che elimina ogni elemento presente nella raccolta.

    Get-CsClientVersionConfiguration -Filter site:* | Remove-CsClientVersionConfiguration

## ESEMPIO 3

Nell'esempio 3 vengono eliminate tutte le impostazioni di configurazione della versione client attualmente disabilitate. A tale scopo, il comando utilizza innanzitutto il cmdlet **Get-CsClientVersionConfiguration** per restituire una raccolta di tutte le impostazioni di configurazione della versione client attualmente in uso nell'organizzazione. Dopo che sono stati restituiti questi dati, la raccolta viene inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le impostazioni in cui la proprietà Enabled è uguale a False. La raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsClientVersionConfiguration**, che elimina ogni elemento della raccolta.

    Get-CsClientVersionConfiguration | Where-Object {$_.Enabled -eq $False} | Remove-CsClientVersionConfiguration

## Descrizione dettagliata

Con Lync Server gli amministratori dispongono di uno spazio di manovra considerevole quando devono specificare il software client (e, ugualmente importante, il numero di versione del software) che gli utenti possono utilizzare per accedere al sistema. Non esistono ad esempio motivi tecnici per cui gli utenti debbano accedere a Lync Server utilizzando Lync. Da un punto di vista tecnico, niente impedisce agli utenti di accedere utilizzando Microsoft Office Communicator 2007 R2.

Potrebbe essere preferibile però per motivi non tecnici che gli utenti non accedano utilizzando Office Communicator 2007 R2. In Office Communicator 2007 R2 ad esempio non sono supportate tutte le caratteristiche e le funzionalità disponibili in Lync. L'esperienza degli utenti che effettuano l'accesso mediante Office Communicator 2007 R2 sarà pertanto diversa da quella degli utenti che accedono mediante Lync. Questo può creare difficoltà per gli utenti, nonché per il personale del supporto tecnico che deve fornire assistenza per numerose applicazioni client diverse.

Se questa situazione può rappresentare un problema per l'organizzazione, è possibile utilizzare il filtro versione client per specificare quali applicazioni client possono essere utilizzate per accedere a Lync Server. Quando si installa Lync Server, viene installato e abilitato un insieme globale di impostazioni di configurazione della versione client. Oltre alle impostazioni globali, è possibile applicare le impostazioni di configurazione della versione client nell'ambito del sito.

Qualsiasi impostazione del sito creata può essere successivamente eliminata utilizzando il cmdlet **Remove-CsClientVersionConfiguration**. È possibile eseguire il cmdlet **Remove-CsClientVersionConfiguration** anche per le impostazioni globali. In questo caso, le impostazioni globali però non vengono rimosse. Le proprietà globali vengono invece reimpostate sui rispettivi valori predefiniti.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Remove-CsClientVersionConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsClientVersionConfiguration"}

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
<td><p>Identificatore univoco per la raccolta di impostazioni di configurazione della versione del client da rimuovere. Per rimuovere la raccolta globale, utilizzare la seguente sintassi: -Identity global. Le impostazioni globali non vengono effettivamente rimosse; in realtà, le proprietà globali vengono semplicemente riportate ai valori predefiniti. Per rimuovere una raccolta di siti, utilizzare una sintassi simile alla seguente: -Identity site:Redmond. Non è possibile utilizzare i caratteri jolly quando si specifica l'identità.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration. Il cmdlet **Remove-CsClientVersionConfiguration** accetta le istanze dell'oggetto configurazione della versione client inviate tramite pipeline.

## Tipi restituiti

Nessuno. Il cmdlet elimina invece le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.ClientVersion.ClientVersionConfiguration.

## Vedere anche

#### Ulteriori risorse

[Get-CsClientVersionConfiguration](get-csclientversionconfiguration.md)  
[New-CsClientVersionConfiguration](new-csclientversionconfiguration.md)  
[Set-CsClientVersionConfiguration](set-csclientversionconfiguration.md)

