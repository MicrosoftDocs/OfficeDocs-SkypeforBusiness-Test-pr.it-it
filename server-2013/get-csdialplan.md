---
title: Get-CsDialPlan
TOCTitle: Get-CsDialPlan
ms:assetid: f77df510-ea43-4352-84c1-13f69eda252e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413043(v=OCS.15)
ms:contentKeyID: 49302502
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsDialPlan

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui dial plan utilizzati nell'organizzazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsDialPlan [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsDialPlan [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Nell'esempio 1 viene restituita una raccolta di tutti i dial plan configurati per essere utilizzati nell'organizzazione richiamando il cmdlet **Get-CsDialPlan** senza parametri aggiuntivi.

    Get-CsDialPlan

## ESEMPIO 2

Nell'esempio 2 il parametro Identity viene utilizzato per limitare i dati recuperati ai dial plan che dispongono di un dial plan per utente con Identity RedmondDialPlan. Poiché le identità devono essere univoche, il comando restituirà solo il dial plan specificato.

    Get-CsDialPlan -Identity RedmondDialPlan

## ESEMPIO 3

L'esempio 3 è identico all'esempio 2, tranne per il fatto che, invece di recuperare un dial plan per utente, recupera un dial plan assegnato a un sito. Per fare ciò, si utilizza il valore site: seguito dal nome del sito (in questo caso Redmond) da recuperare.

    Get-CsDialPlan -Identity site:Redmond

## ESEMPIO 4

In questo esempio viene utilizzato il parametro Filter per restituire una raccolta di tutti i dial plan che sono stati configurati con ambito per utente. (Le impostazioni configurate con ambito per utente o tag possono essere assegnate direttamente agli utenti e ai gruppi). La stringa con carattere jolly tag:\* istruisce il cmdlet affinché restituisca solo i dial plan con identità che inizia con il valore stringa tag:, che identifica un dial plan come dial plan per utente.

    Get-CsDialPlan -Filter tag:*

## ESEMPIO 5

Nell'esempio vengono visualizzate le regole di normalizzazione utilizzate dai dial plan configurati per l'utilizzo nell'organizzazione. Poiché la proprietà NormalizationRules si compone di un array di oggetti, di solito l'insieme completo delle regole di normalizzazione non viene visualizzato sullo schermo. Per vedere tutte le regole, questo comando utilizza come prima cosa il cmdlet **Get-CsDialPlan** per recuperare una raccolta di tutti i dial plan. La raccolta viene quindi inviata tramite pipe al cmdlet **Select-Object**, al contrario il parametro ExpandProperty del cmdlet **Select-Object** viene utilizzato per espandere i valori trovati nella proprietà NormalizationRules. Espandendo i valori, tutte le regole di normalizzazione verranno visualizzate sullo schermo, lo stesso risultato che si otterrebbe chiamando il cmdlet **Get-CsVoiceNormalizationRule**.

    Get-CsDialPlan | Select-Object -ExpandProperty NormalizationRules

## ESEMPIO 6

Nell'esempio 6, il cmdlet **Get-CsDialPlan** e il cmdlet **Where-Object** vengono utilizzati per recuperare una raccolta di tutti i dial plan che includono la parola Redmond nella loro descrizione. A tale scopo, per prima cosa il comando utilizza il cmdlet **Get-CsDialPlan** per recuperare tutti i dial plan. La raccolta verrà quindi inviata tramite pipe al cmdlet **Where-Object**, che applica un filtro che limita i dati restituiti ai profili che contengono la parola Redmond all'interno della descrizione.

    Get-CsDialPlan | Where-Object {$_.Description -match "Redmond"}

## Descrizione dettagliata

Questo cmdlet restituisce informazioni su uno o più dial plan (conosciuti anche come profili di numerazione locale) in un'organizzazione. I dial plan forniscono informazioni necessarie per consentire agli utenti di VoIP aziendale di effettuare telefonate. I dial plan sono utilizzati anche da applicazione Operatore Conferenza per le conferenze telefoniche con accesso esterno. Un dial plan determina le regole di normalizzazione applicate e se è necessario comporre un prefisso per le chiamate esterne.

Nota: è possibile utilizzare il cmdlet **Get-CsDialPlan** per recuperare informazioni specifiche sulle regole di normalizzazione di un dial plan, ma se questa è l'unica informazione che si desidera recuperare, è possibile anche utilizzare il cmdlet **Get-CsVoiceNormalizationRule**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Get-CsDialPlan** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsDialPlan"}

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
<td><p>Esegue una ricerca con caratteri jolly che consente di restringere i risultati ai dial plan con identità che corrispondono alla stringa con carattere jolly data.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>L'identificatore univoco che designa l'ambito, l'ambito per utente e un nome per identificare il dial plan che si desidera recuperare.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Recupera le informazioni sui dial plan dalla replica locale del archivio di gestione centrale, anziché dal archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Questo cmdlet restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.LocationProfile.

## Vedere anche

#### Ulteriori risorse

[New-CsDialPlan](new-csdialplan.md)  
[Remove-CsDialPlan](remove-csdialplan.md)  
[Set-CsDialPlan](set-csdialplan.md)  
[Grant-CsDialPlan](grant-csdialplan.md)  
[Test-CsDialPlan](test-csdialplan.md)  
[Get-CsVoiceNormalizationRule](get-csvoicenormalizationrule.md)

