---
title: Get-CsVoicePolicy
TOCTitle: Get-CsVoicePolicy
ms:assetid: 05096aec-321c-4a50-99be-6e9fbbbe17fa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398101(v=OCS.15)
ms:contentKeyID: 49299540
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsVoicePolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni su uno o più criteri vocali configurati per l'organizzazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsVoicePolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsVoicePolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Tenant <Guid>]

## Esempi

## ESEMPIO 1

Con questo esempio vengono visualizzati tutti i criteri vocali definiti per un'organizzazione inscieme alle relative impostazioni di ognuno.

    Get-CsVoicePolicy

## ESEMPIO 2

Con questo esempio viene utilizzato il parametro Identity per recuperare le impostazioni dei criteri vocali per il criterio per utente denominato UserPolicy1.

    Get-CsVoicePolicy -Identity UserPolicy1

## ESEMPIO 3

In questo esempio viene utilizzato il parametro Filter per recuperare tutte le impostazioni dei criteri vocali che possono essere assegnate agli utenti. Tutti i criteri vocali per utente dispongono di un parametro Identity nel formato **tag:\<UserVoicePolicy\>**, pertanto è possibile filtrare i dati in base al tag per recuperare tutti i criteri vocali utente.

    Get-CsVoicePolicy -Filter tag*

## Descrizione dettagliata

Questo cmdlet recupera informazioni sui criteri vocali. I criteri vocali sono utilizzati per gestire funzionalità di VoIP aziendale quali, ad esempio, lo squillo simultaneo (vale a dire la capacità di far squillare un secondo telefono ogni volta che si riceve una chiamata sul telefono dell'ufficio) e l'inoltro di chiamata. Utilizzare questo cmdlet per recuperare le impostazioni che permettono di abilitare e disabilitare molte di queste funzionalità.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Get-CsVoicePolicy** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsVoicePolicy"}

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
<td><p>Questo parametro accetta una stringa di caratteri jolly e restituisce tutti i criteri vocali con identità corrispondenti a tale stringa. Ad esempio, con un valore site:* per Filter vengono restituiti tutti i criteri vocali definiti a livello di sito.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Un identificatore univoco che specifica l'ambito, e in alcuni casi il nome, del criterio. Se questo parametro viene omesso, vengono restituiti tutti i criteri vocali per l'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i criteri vocali dalla replica locale del archivio di gestione centrale anziché dal archivio di gestione centrale stesso.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di Skype for Business online di cui deve essere recuperato il criterio vocale. Ad esempio:</p>
<p>–Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>È possibile restituire l'ID di ogni tenant eseguendo questo comando:</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Se si usa una sessione remota di Windows PowerShell e si è connessi solo a Skype for Business online non è necessario includere il parametro Tenant. L'ID del tenant verrà infatti compilato automaticamente in base alle informazioni di connessione. Il parametro Tenant è destinato principalmente all'uso in ambienti ibridi.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno.

## Tipi restituiti

Il cmdlet restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Policy.Voice.VoicePolicy.

## Vedere anche

#### Ulteriori risorse

[New-CsVoicePolicy](new-csvoicepolicy.md)  
[Remove-CsVoicePolicy](remove-csvoicepolicy.md)  
[Set-CsVoicePolicy](set-csvoicepolicy.md)  
[Grant-CsVoicePolicy](grant-csvoicepolicy.md)  
[Test-CsVoicePolicy](test-csvoicepolicy.md)

