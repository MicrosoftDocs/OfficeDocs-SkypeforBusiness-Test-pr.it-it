---
title: Remove-CsTrunkConfiguration
TOCTitle: Remove-CsTrunkConfiguration
ms:assetid: 45546534-1a18-4db2-be61-850bacf55a52
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425943(v=OCS.15)
ms:contentKeyID: 49300382
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsTrunkConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una configurazione trunk esistente che descrive le impostazioni di un'entità peer di trunking, ad esempio un gateway PSTN (Public Switched Telephone Network), un sistema IP-PBX (Public Branch Exchange) o un servizio SBC (Session Border Controller) nel provider di servizi. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsTrunkConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

In questo esempio viene rimossa la configurazione trunk con Identity site:Redmond.

    Remove-CsTrunkConfiguration -Identity site:Redmond

## ESEMPIO 2

Nell'esempio 2 vengono rimosse tutte le configurazioni trunk definite a livello di sito. Nella prima parte del comando viene chiamato il cmdlet **Get-CsTrunkConfiguration**, che utilizza il parametro Filter per recuperare tutte le configurazioni trunk con valore Identity che inizia con site:, ovvero tutte le configurazioni trunk definite a livello di sito. La raccolta di configurazioni viene quindi inviata tramite pipe al cmdlet **Remove-CsTrunkConfiguration**, che rimuove tutti gli oggetti della raccolta.

    Get-CsTrunkConfiguration -Filter site:* | Remove-CsTrunkConfiguration

## Descrizione dettagliata

Utilizzare questo cmdlet per rimuovere una configurazione di trunking valida per le entità gateway PSTN. Ogni configurazione contiene impostazioni specifiche di un'entità peer di trunking, ad esempio un gateway PSTN, un sistema IP-PBX o un servizio SBC nel provider di servizi. Tali impostazioni consentono di configurare diversi aspetti, ad esempio se abilitare o meno il bypass degli elementi multimediali in questo trunk, se inviare o meno i pacchetti RTCP (Real-Time Control Protocol) in determinate condizioni e se richiedere o meno la crittografia SRTP (Secure Real-Time Protocol).

Se si chiama il cmdlet **Remove-CsTrunkConfiguration** per la configurazione globale, questa configurazione trunk non verrà rimossa. La configurazione viene invece "reimpostata" e tutte le impostazioni personalizzate vengono sostituite dai valori predefiniti.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsTrunkConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsTrunkConfiguration"}

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
<td><p>L'identificatore univoco della configurazione trunk che si desidera rimuovere.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration. Accetta l'input da pipeline di oggetti configurazione trunk.

## Tipi restituiti

Questo cmdlet non restituisce un valore. Rimuove un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsTrunkConfiguration](new-cstrunkconfiguration.md)  
[Set-CsTrunkConfiguration](set-cstrunkconfiguration.md)  
[Get-CsTrunkConfiguration](get-cstrunkconfiguration.md)  
[Test-CsTrunkConfiguration](test-cstrunkconfiguration.md)

