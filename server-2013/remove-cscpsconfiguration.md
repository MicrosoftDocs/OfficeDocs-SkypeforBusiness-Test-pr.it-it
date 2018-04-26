---
title: Remove-CsCpsConfiguration
TOCTitle: Remove-CsCpsConfiguration
ms:assetid: 546343e1-a2e4-4bc0-bf6d-c8ae9bb3e690
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398358(v=OCS.15)
ms:contentKeyID: 49300598
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsCpsConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una configurazione esistente del servizio Parcheggio di chiamata. Quest'ultimo è un servizio che consente a un utente di "parcheggiare" una chiamata telefonica in arrivo. Parcheggiare una chiamata significa trasferirla a un numero (o codice orbit) di uno specifico intervallo e quindi metterla immediatamente in attesa. Chiunque (non solo la persona che ha in origine risposto alla chiamata) può riprendere la conversazione da qualsiasi telefono immettendo il numero corretto. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsCpsConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene utilizzato il cmdlet **Remove-CsCpsConfiguration** per eliminare la configurazione del servizio Parcheggio di chiamata con identità (Identity) site:Redmond1. Poiché le identità sono univoche, con questo comando viene eliminata una sola configurazione.

    Remove-CsCpsConfiguration -Identity site:Redmond1

## ESEMPIO 2

Nell'esempio 2 vengono eliminate tutte le configurazioni del servizio Parcheggio di chiamata definite nell'ambito del sito. A tale scopo, il comando innanzitutto utilizza il cmdlet **Get-CsCpsConfiguration** e il parametro Filter per restituire tutte le configurazioni del servizio Parcheggio di chiamata definite nell'ambito del sito. Il valore con caratteri jolly in site:\* assicura che vengano restituite solo le impostazioni il cui parametro Identity inizia con il valore stringa site:. Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Remove-CsCpsConfiguration**, che procede all'eliminazione di ogni elemento della raccolta. Quando le impostazioni del servizio Parcheggio di chiamata vengono rimosse da un sito, questo inizia automaticamente a utilizzare le impostazioni del servizio Parcheggio di chiamata configurate nell'ambito globale.

    Get-CsCpsConfiguration -Filter site:* | Remove-CsCpsConfiguration

## Descrizione dettagliata

Questo cmdlet viene utilizzato per rimuovere una configurazione del servizio Parcheggio di chiamata. Questa configurazione specifica cosa accade a una chiamata quando viene parcheggiata. Se ad esempio non si risponde a una chiamata parcheggiata entro un determinato periodo, la chiamata può essere automaticamente inoltrata a un'altra persona, come un amministratore o un gruppo di risposta. Le chiamate possono essere configurate in modo da far squillare il telefono dopo un determinato periodo, affinché la chiamata non venga dimenticata. Inoltre, il servizio Parcheggio di chiamata può essere configurato per riprodurre una musica di attesa per il chiamante mentre la chiamata risulta parcheggiata.

Questo cmdlet può essere utilizzato per rimuovere qualsiasi configurazione di Parcheggio di chiamata, compresa la configurazione Global. Nel caso della configurazione Global, però, la configurazione non viene effettivamente rimossa; in realtà, viene semplicemente ripristinata ai valori predefiniti.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Remove-CsCpsConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsCpsConfiguration"}

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
<td><p>L'identificatore univoco della configurazione del servizio Parcheggio di chiamata che si desidera rimuovere. Questo identificatore sarà Global o site:&lt;nome sito&gt;, dove &lt;nome sito&gt; corrisponde al nome del sito a cui si applica la configurazione.</p></td>
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
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings. Consente di accettare l'input da pipeline di oggetti configurazione del servizio Parcheggio di chiamata.

## Tipi restituiti

Consente di rimuovere un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.CallParkServiceSettings.CallParkServiceSettings.

## Vedere anche

#### Ulteriori risorse

[New-CsCpsConfiguration](new-cscpsconfiguration.md)  
[Set-CsCpsConfiguration](set-cscpsconfiguration.md)  
[Get-CsCpsConfiguration](get-cscpsconfiguration.md)  
[Set-CsCallParkServiceMusicOnHoldFile](set-cscallparkservicemusiconholdfile.md)

