---
title: Remove-CsVoiceTestConfiguration
TOCTitle: Remove-CsVoiceTestConfiguration
ms:assetid: abe27005-8325-47d7-8c7c-12bb831b87c7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412813(v=OCS.15)
ms:contentKeyID: 49301630
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsVoiceTestConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una configurazione di test vocale utilizzata per verificare i numeri di telefono rispetto alle route e alle regole specificate. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsVoiceTestConfiguration -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con questo esempio vengono rimosse le impostazioni per la configurazione di test vocale con identità TestConfig1.

    Remove-CsVoiceTestConfiguration -Identity TestConfig1

## ESEMPIO 2

Con questo esempio vengono rimosse le impostazioni di configurazione di test vocale per qualsiasi configurazione la cui identità contiene la stringa test. Il comando chiama per prima cosa il cmdlet **Get-CsVoiceTestConfiguration** con il parametro Filter per recuperare tutte le configurazioni di test vocale la cui Identity contiene la stringa "test" nel suo valore. Il set di configurazioni risultante viene quindi inviato tramite pipe al cmdlet **Remove-CsVoiceTestConfiguration** e rimosso.

    Get-CsVoiceTestConfiguration -Filter *test* | Remove-CsVoiceTestConfiguration

## Descrizione dettagliata

Prima di implementare route vocali e criteri vocali, è opportuno testarli su diversi numeri di telefono per garantire che i risultati siano quelli previsti. Una volta terminati i test, se non sono più necessari è possibile rimuoverli utilizzando questo cmdlet.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Remove-CsVoiceTestConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsVoiceTestConfiguration"}

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
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Una stringa che identifica in modo univoco la configurazione di test da rimuovere.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration. Accetta l'input da pipeline di oggetti di configurazione di test vocale.

## Tipi restituiti

Consente di rimuovere un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Policy.Voice.TestConfiguration.

## Vedere anche

#### Ulteriori risorse

[New-CsVoiceTestConfiguration](new-csvoicetestconfiguration.md)  
[Set-CsVoiceTestConfiguration](set-csvoicetestconfiguration.md)  
[Get-CsVoiceTestConfiguration](get-csvoicetestconfiguration.md)  
[Test-CsVoiceTestConfiguration](test-csvoicetestconfiguration.md)

