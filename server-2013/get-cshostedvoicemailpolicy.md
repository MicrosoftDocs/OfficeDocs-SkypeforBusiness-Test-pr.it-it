---
title: Get-CsHostedVoicemailPolicy
TOCTitle: Get-CsHostedVoicemailPolicy
ms:assetid: 52dd4397-b1c5-44a5-a744-75d715a4511b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398348(v=OCS.15)
ms:contentKeyID: 49300536
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsHostedVoicemailPolicy

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Recupera un criterio di segreteria telefonica ospitata. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsHostedVoicemailPolicy [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsHostedVoicemailPolicy [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>] [-Tenant <Guid>]

## Esempi

## ESEMPIO 1

Questo restituisce tutti i criteri di segreteria telefonica ospitata definiti per l'implementazione di Lync Server.

    Get-CsHostedVoicemailPolicy

## ESEMPIO 2

Con questo comando vengono restituite le impostazioni dei criteri per il criterio di segreteria telefonica ospitata per utente ExRedmond.

    Get-CsHostedVoicemailPolicy -Identity ExRedmond

## ESEMPIO 3

Con questo comando vengono restituite le impostazioni dei criteri per tutti i criteri di segreteria telefonica ospitata per utente (ovvero i criteri che iniziano con l'ambito tag).

    Get-CsHostedVoicemailPolicy -Filter tag:*

## ESEMPIO 4

Questo comando restituisce i criteri segreteria telefonica ospitata per il tenant Lync Online con l'ID tenant 73d355dd-ce5d-4ab9-bf49-7b822c18dd98.

    Get-CsHostedVoicemailPolicy -Tenant "73d355dd-ce5d-4ab9-bf49-7b822c18dd98"

## Descrizione dettagliata

Questo cmdlet consente di recuperare un criterio che specifica come instradare le chiamate senza risposta a un servizio Messaggistica unificata di Exchange ospitato.

Affinché il criterio abbia effetto deve esistere un utente abilitato per la segreteria telefonica ospitata di Messaggistica unificata di Exchange. È possibile utilizzare il cmdlet **Get-CsUser** e controllare la proprietà HostedVoiceMail per stabilire se esiste un utente abilitato per la segreteria telefonica ospitata. Il valore True indica che l'utente è abilitato.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsHostedVoicemailPolicy** i membri dei seguenti gruppi: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsHostedVoicemailPolicy"}

``` 
```

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
<td><p>Questo parametro consente di eseguire una ricerca con caratteri jolly dell'identità del criterio di segreteria telefonica ospitata. Vengono recuperate tutte le istanze di un criterio di segreteria telefonica ospitata per cui Identity corrisponde al modello di caratteri jolly specificato nel valore Filter.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>L'identificatore univoco per il criterio di segreteria telefonica ospitata che si desidera recuperare. L'identità include l'ambito (nel caso di un ambito globale), l'ambito e il sito (per un criterio di sito, ad esempio site:Redmond) oppure il nome del criterio (nel caso di un criterio per utente, ad esempio HVUserPolicy).</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare il criterio di segreteria telefonica ospitata dalla copia locale di archivio di gestione centrale invece che da archivio di gestione centrale.</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Guid</p></td>
<td><p>Identificatore univoco globale (GUID) dell'account tenant di Skype for Business online di cui deve essere recuperato il criterio di segreteria telefonica.</p>
<p>Ad esempio:</p>
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

Questo cmdlet restituisce un oggetto di tipo Microsoft.Rtc.Management.WritableConfig.Policy.Voice.HostedVoicemailPolicy.

## Vedere anche

#### Ulteriori risorse

[New-CsHostedVoicemailPolicy](new-cshostedvoicemailpolicy.md)  
[Remove-CsHostedVoicemailPolicy](remove-cshostedvoicemailpolicy.md)  
[Set-CsHostedVoicemailPolicy](set-cshostedvoicemailpolicy.md)  
[Grant-CsHostedVoicemailPolicy](grant-cshostedvoicemailpolicy.md)

