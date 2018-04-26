---
title: Get-CsVoiceNormalizationRule
TOCTitle: Get-CsVoiceNormalizationRule
ms:assetid: 59fe1370-1cec-4cf9-8f65-029a7c2454d1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398393(v=OCS.15)
ms:contentKeyID: 49300672
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoiceNormalizationRule

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle regole di normalizzazione vocale in uso nell'organizzazione. Le regole di normalizzazione vocale sono utilizzate per convertire un requisito di composizione telefonica (ad esempio la composizione di 9 per l'accesso a una linea esterna) nel formato per numeri di telefono E.164 utilizzato da Lync Server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsVoiceNormalizationRule [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsVoiceNormalizationRule [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Con questo esempio vengono recuperate tutte le regole di normalizzazione vocale definite per l'organizzazione.

    Get-CsVoiceNormalizationRule

## ESEMPIO 2

Con l'esempio 2 vengono recuperate tutte le regole di normalizzazione vocale specificate per tutti i siti.

    Get-CsVoiceNormalizationRule -Filter site*

## ESEMPIO 3

L'Esempio 3 consente di recuperare le regole di normalizzazione vocale che contengono la lettera s in qualunque punto dell'ambito. Ad esempio, questo comando restituirà tutte le regole a livello di sito e servizio nonché tutte le regole per utente che contengono una s nel nome dell'ambito, come, ad esempio, RedmondEastUsers.

    Get-CsVoiceNormalizationRule -Filter *s*

## ESEMPIO 4

Il parametro Filter utilizzato negli esempi 2 e 3 consente la corrispondenza solo con la parte dell'ambito del parametro Identity. In questo esempio viene trovata una corrispondenza sulla parte del nome, in modo da restituire tutte le regole il cui nome contiene la stringa "seattle". A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsVoiceNormalizationRule** per recuperare tutte le regole di normalizzazione dell'organizzazione. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object** per trovare tutti gli elementi della raccolta la cui proprietà Name corrisponde alla stringa "seattle".

    Get-CsVoiceNormalizationRule | Where-Object {$_.Name -match "seattle"}

## Descrizione dettagliata

Questo cmdlet restituisce una regola di normalizzazione vocale o una raccolta di regole di normalizzazione vocale denominata. Queste regole sono una parte obbligatoria dell'autorizzazione telefonica e del routing delle chiamate. Definiscono i requisiti per la conversione dei numeri dal formato Lync Server interno a un formato standard (E.164). È utile conoscere l'utilizzo delle espressioni regolari per definire i formati numerici da convertire.

È possibile accedere alle stesse regole recuperate dal cmdlet attraverso la proprietà NormalizationRules restituita dall'utilizzo del cmdlet **Get-CsDialPlan**.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Get-CsVoiceNormalizationRule** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoiceNormalizationRule"}

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
<td><p><em>Filter</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di utilizzare stringhe con caratteri jolly per ottenere una raccolta di regole di normalizzazione basate sul parametro Identity. Filter è utilizzabile solamente sulla parte dell'ambito dell'identità, non sul nome. Ad esempio, il valore di filtro *lob* restituisce tutte le regole in ambito globale (gli ambiti che contengono le lettere lob), ma non una regola con identità site:Redmond/lobby, dove lob si trova solo nel nome dell'identità e non nell'ambito.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Un identificatore univoco per la regola. Se viene specificato un valore per questo parametro, il valore deve essere nel formato ambito/nome, come in site:co1/Rule1, dove site:co1 è l'ambito e Rule1 è il nome.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare la regola di normalizzazione vocale dalla replica locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Il cmdlet **Get-CsVoiceNormalizationRule** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.NormalizationRule.

## Vedere anche

#### Ulteriori risorse

[New-CsVoiceNormalizationRule](new-csvoicenormalizationrule.md)  
[Remove-CsVoiceNormalizationRule](remove-csvoicenormalizationrule.md)  
[Set-CsVoiceNormalizationRule](set-csvoicenormalizationrule.md)  
[Test-CsVoiceNormalizationRule](test-csvoicenormalizationrule.md)  
[Get-CsDialPlan](get-csdialplan.md)

