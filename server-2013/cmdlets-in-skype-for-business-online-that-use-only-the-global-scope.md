---
title: Cmdlet che usano solo l'ambito globale
TOCTitle: Cmdlet che usano solo l'ambito globale
ms:assetid: 0ffd3bc9-a6a1-4c2e-8d52-e599acc49d2d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362771(v=OCS.15)
ms:contentKeyID: 56269883
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlet che usano solo l'ambito globale

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Alcune impostazioni di Skype for Business online sono disponibili solo nell'*ambito globale*. Ciò significa che esiste una singola raccolta di impostazioni applicabili a tutti gli utenti assegnati a tale tenant. Ogni tenant ha infatti una propria raccolta univoca di impostazioni globali. Quando si usano cmdlet limitati all'ambito globale, il parametro Identity è facoltativo. Per recuperare ad esempio le impostazioni di configurazione delle riunioni, è possibile usare questo comando:

    Get-CsMeetingConfiguration -Identity "global"

In alternativa, si può omettere il parametro Identity e usare invece questo comando più semplice:

    Get-CsMeetingConfiguration

Essendo disponibile una sola raccolta globale di impostazioni di configurazione delle riunioni, i due comandi restituiscono esattamente le stesse informazioni. Il parametro Identity può essere omesso anche quando si usa uno dei cmdlet **Set-Cs**. Questi due comandi sono identici:

    Set-CsMeetingConfiguration -Identity "global" -AdmitAnonymousUsersByDefault $False
    Set-CsMeetingConfiguration -AdmitAnonymousUsersByDefault $False

I due comandi sono identici perché, per impostazione predefinita, se non si include il parametro Identity Windows PowerShell modifica la raccolta globale.

I cmdlet seguenti funzionano solo nell'ambito globale:

  - [Get-CsImFilterConfiguration](get-csimfilterconfiguration.md)

  - [Get-CsMeetingConfiguration](get-csmeetingconfiguration.md)

  - [Get-CsPrivacyConfiguration](get-csprivacyconfiguration.md)

  - [Get-CsTenantFederationConfiguration](get-cstenantfederationconfiguration.md)

  - [Get-CsTenantHybridConfiguration](get-cstenanthybridconfiguration.md)

  - [Get-CsTenantLicensingConfiguration](get-cstenantlicensingconfiguration.md)

  - [Get-CsTenantPublicProvider](get-cstenantpublicprovider.md)

  - [Remove-CsVoicePolicy](remove-csvoicepolicy.md)

  - [Set-CsMeetingConfiguration](set-csmeetingconfiguration.md)

  - [Set-CsPrivacyConfiguration](set-csprivacyconfiguration.md)

Si noti che il cmdlet **Remove-CsVoicePolicy** costituisce un'anomalia. Prima di tutto non richiede l'inclusione del parametro Identity:

    Remove-CsVoicePolicy -Identity "global"

Inoltre, il cmdlet **Remove-CsVoicePolicy** non elimina in effetti i criteri vocali globali. Skype for Business online non consente infatti di eliminare i criteri globali o le impostazioni di configurazione. Il cmdlet consente semplicemente di reimpostare i valori predefiniti di tutte le proprietà dei criteri vocali globali. Ad esempio, per impostazione predefinita, la proprietà AllowCallForwarding è impostata su False, ma potrebbe essere stata modificata e il valore essere impostato su True. Quando si esegue il cmdlet **Remove-CsVoicePolicy**, la proprietà AllowCallForwarding verrà reimpostata sul valore predefinito False. Questo scenario è riepilogato nella tabella seguente:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valore di AllowCallForwarding</th>
<th>Scenario</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>False</p></td>
<td><p>Valore predefinito</p></td>
</tr>
<tr class="even">
<td><p>True</p></td>
<td><p>Dopo la modifica dei criteri globali</p></td>
</tr>
<tr class="odd">
<td><p>False</p></td>
<td><p>Dopo l'esecuzione del cmdlet <strong>Remove-CsVoicePolicy</strong></p></td>
</tr>
</tbody>
</table>


## Vedere anche

#### Concetti

[Identità, ambiti e tenant](identities-scopes-and-tenants-in-skype-for-business-online.md)  
[Cmdlet di Lync Online](the-skype-for-business-online-cmdlets.md)

