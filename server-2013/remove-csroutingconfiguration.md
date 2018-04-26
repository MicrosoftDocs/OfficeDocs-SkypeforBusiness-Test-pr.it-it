---
title: Remove-CsRoutingConfiguration
TOCTitle: Remove-CsRoutingConfiguration
ms:assetid: 80239fed-89ef-4ccc-be9b-d9149182d0c3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398643(v=OCS.15)
ms:contentKeyID: 49301137
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsRoutingConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Ripristina le impostazioni predefinite della configurazione di routing. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsRoutingConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con questo esempio la configurazione di routing Global (e solo questa) viene riportata alle impostazioni predefinite. Con questa operazione vengono eliminate tutte le route vocali definite, pertanto è stato aggiunto il parametro Confirm al fine di visualizzare un prompt che richiede di confermare l'operazione prima che abbia luogo la rimozione.

    Remove-CsRoutingConfiguration -Identity Global -Confirm

## Descrizione dettagliata

Le route vocali includono istruzioni che comunicano a Lync Server come instradare le chiamate effettuate da utenti di VoIP aziendale ai numeri di telefono della rete PSTN (Public Switched Telephone Network) o di un centralino (PBX, Private Branch Exchange). Questo cmdlet rimuove solo la configurazione di routing globale, che è un contenitore per tutte le route vocali definite per una distribuzione di Lync Server. Con la "rimozione" la configurazione di routing non viene effettivamente rimossa perché l'istanza Global (e solo questa) è ancora presente. Vengono tuttavia ripristinate le impostazioni predefinite dell'elenco delle route vocali.

AVVISO: con la rimozione della configurazione di routing, ovvero con l'impostazione dell'elenco delle route vocali sui valori predefiniti, vengono eliminate tutte le route vocali definite per una distribuzione di Lync Server, che vengono sostituite da una singola route con impostazioni predefinite.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Remove-CsRoutingConfiguration** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsRoutingConfiguration"}

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
<td><p>L'ambito della configurazione di routing da rimuovere. Questo valore deve essere Global.</p></td>
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

Oggetto Microsoft.Rtc.Management.Policy.Voice.PSTNRoutingSettings. Consente di accettare l'input da pipeline di un oggetto configurazione di routing.

## Tipi restituiti

Questo cmdlet consente di rimuovere (o reimpostare) un oggetto di tipo Microsoft.Rtc.Management.Policy.Voice.PSTNRoutingSettings.

## Vedere anche

#### Ulteriori risorse

[New-CsRoutingConfiguration](new-csroutingconfiguration.md)  
[Set-CsRoutingConfiguration](set-csroutingconfiguration.md)  
[Get-CsRoutingConfiguration](get-csroutingconfiguration.md)  
[Remove-CsVoiceRoute](remove-csvoiceroute.md)  
[Get-CsVoiceRoute](get-csvoiceroute.md)

