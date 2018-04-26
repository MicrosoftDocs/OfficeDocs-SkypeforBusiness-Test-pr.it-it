---
title: Set-CsPstnUsage
TOCTitle: Set-CsPstnUsage
ms:assetid: ecba9ed6-4845-4035-933e-0c540d530b72
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399069(v=OCS.15)
ms:contentKeyID: 49302363
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsPstnUsage

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Modifica un insieme di stringhe che identificano gli utilizzi PSTN (Public Switched Telephone Network) consentiti. Questo cmdlet può essere utilizzato per aggiungere utilizzi all'elenco degli utilizzi PSTN o per rimuovere utilizzi da tale elenco. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsPstnUsage [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsPstnUsage [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Usage <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Con questo comando viene aggiunta la stringa "International" all'elenco corrente di utilizzi PSTN disponibili.

    Set-CsPstnUsage -Identity global -Usage @{add="International"}

## ESEMPIO 2

Questo comando consente la rimozione della stringa "Local" dall'elenco di utilizzi PSTN disponibili.

    Set-CsPstnUsage -Identity global -Usage @{remove="Local"}

## ESEMPIO 3

Il comando riportato in questo esempio esegue la stessa azione del comando dell'esempio 2: rimuove l'utilizzo PSTN "Local". In questo esempio viene mostrato il comando senza che venga specificato il parametro Identity. L'unico valore Identity disponibile per il cmdlet **Set-CsPstnUsage** è Global. Omettendo il parametro Identity, verrà pertanto utilizzato Global per impostazione predefinita.

    Set-CsPstnUsage -Usage @{remove="Local"}

## ESEMPIO 4

Con questo comando vengono sostituiti tutti gli elementi nell'elenco di utilizzi con i valori International e Restricted. Tutti gli utilizzi esistenti in precedenza vengono rimossi.

    Set-CsPstnUsage -Usage @{replace="International","Restricted"}

## Descrizione dettagliata

Gli utilizzi di PSTN sono valori stringa utilizzati per l'autorizzazione delle chiamate. Un utilizzo di PSTN collega un criterio vocale a una route. Il cmdlet **Set-CsPstnUsage** consente di aggiungere utilizzi telefono all'elenco degli utilizzi o di rimuoverli dallo stesso. Questo elenco è globale, quindi può essere utilizzato dai criteri e dalle route nella distribuzione di Lync Server.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsPstnUsage** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsPstnUsage"}

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
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Elimina qualsiasi richiesta di conferma che, in caso contrario, sarebbe visualizzata prima di effettuare le modifiche.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>L'ambito di applicazione di queste impostazioni. L'identità di questo cmdlet è sempre Global.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>PstnUsages</p></td>
<td><p>Un riferimento all'oggetto utilizzo PSTN. L'oggetto deve essere di tipo PstnUsages e può essere recuperato chiamando il cmdlet <strong>Get-CsPstnUsage</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><em>Usage</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>Contiene un elenco di stringhe di utilizzo ammesse. Queste voci possono corrispondere a qualsiasi valore stringa.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PstnUsages. Accetta l'input da pipeline di oggetti utilizzo PSTN.

## Tipi restituiti

Questo cmdlet non restituisce un valore o un oggetto. Configura piuttosto le istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.PstnUsages.

## Vedere anche

#### Ulteriori risorse

[Get-CsPstnUsage](get-cspstnusage.md)

