---
title: Get-CsKerberosAccountAssignment
TOCTitle: Get-CsKerberosAccountAssignment
ms:assetid: 6eaba274-1693-42a7-841d-513bc1153647
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398526(v=OCS.15)
ms:contentKeyID: 49300914
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsKerberosAccountAssignment

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sulle assegnazioni degli account Kerberos configurati per l'utilizzo nell'organizzazione. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsKerberosAccountAssignment [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsKerberosAccountAssignment [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 restituisce le informazioni su tutte le assegnazioni dell'account Kerberos utilizzate al momento nell'organizzazione.

    Get-CsKerberosAccountAssignment

## ESEMPIO 2

Con l'esempio 2 vengono restituite le informazioni su una singola assegnazione dell'account Kerberos: l'assegnazione dell'account per il sito Redmond.

    Get-CsKerberosAccountAssignment -Identity "site:Redmond"

## ESEMPIO 3

Con l'esempio 3 vengono restituite le informazioni per tutti gli account Kerberos assegnati ai siti con il valore stringa "Redmond" nell'identità del sito. Per ottenere questo risultato, viene incluso il parametro Filter insieme al valore di filtro "\*Redmond".

    Get-CsKerberosAccountAssignment -Filter "*Redmond*"

## ESEMPIO 4

Nell'esempio 4 vengono restituite informazioni su tutte le assegnazioni di account Kerberos in cui l'identità dell'account assegnato include il valore stringa "litwareinc". A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsKerberosAccountAssignment** senza alcun parametro aggiuntivo per restituire una raccolta di tutte le assegnazioni di account Kerberos attualmente in uso. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo le assegnazioni di account in cui l'identità dell'account include il valore stringa "litwareinc". Nonostante il nome del parametro UserAccount, l'account è in realtà un account computer.

    Get-CsKerberosAccountAssignment | Where-Object {$_.UserAccount -match "litwareinc"}

## Descrizione dettagliata

In Microsoft Office Communications Server 2007 e Microsoft Office Communications Server 2007 R2 IIS viene eseguito con un account utente standard. Questo processo può causare problemi: se scade la password, è possibile che vengano persi i servizi Web, un evento spesso difficile da diagnosticare. Per evitare che si verifichi questo problema di scadenza delle password, Lync Server consente di creare un account computer (per un computer che in effetti non esiste) che può servire come entità di autenticazione per tutti i computer di un sito che eseguono IIS. Poiché questi account utilizzano il protocollo di autenticazione Kerberos, vengono denominati account Kerberos e il nuovo processo di autenticazione è noto come autenticazione Web Kerberos. In questo modo è possibile gestire tutti i server IIS utilizzando un singolo account.

Per eseguire i propri server con questa nuova entità di autenticazione, è necessario innanzitutto creare un account computer utilizzando il cmdlet **New-CsKerberosAccount**. Questo account viene quindi assegnato a uno o più siti. Dopo l'assegnazione, viene abilitata l'associazione tra l'account e il sito di Lync Server eseguendo il cmdlet **Enable-CsTopology**. Tra l'altro, ciò determina la creazione del nome dell'entità servizio (SPN, Service Principal Name) necessario in Servizi di dominio Active Directory. I nomi SPN consentono alle applicazioni client di reperire un particolare servizio.

Il cmdlet **Get-CsKerberosAccountAssignment** restituisce informazioni sulle assegnazioni dell'account Kerberos attualmente in uso nella propria organizzazione.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **Get-CsKerberosAccountAssignment** in locale: RTCUniversalUserAdmins, RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsKerberosAccountAssignment"}

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
<td><p>Consente di utilizzare i caratteri jolly per specificare l'assegnazione (o le assegnazioni) dell'account Kerberos da restituire. Ad esempio, questa sintassi restituisce tutte le assegnazioni dell'account che includono il valore stringa &quot;Europe&quot;: -Filter &quot;*Europe*&quot;.</p>
<p>Non è possibile utilizzare i parametri Filter e Identity nello stesso comando.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco del sito a cui è stato assegnato l'account Kerberos, ad esempio: -Identity &quot;site:Redmond&quot;. Si tratta dell'identità del sito, non dell'account computer. Non è possibile utilizzare caratteri jolly quando si specifica l'identità del sito. Per utilizzare i caratteri jolly, occorre invece utilizzare il parametro Filter.</p>
<p>Se non sono inclusi né il parametro Identity né il parametro Filter, il cmdlet <strong>Get-CsKerberosAccountAssignment</strong> restituisce tutte le assegnazioni di account Kerberos configurate per l'utilizzo nell'organizzazione.</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di recuperare i dati dell'assegnazione Kerberos dalla replica locale dell'archivio di gestione centrale anziché dall'archivio di gestione centrale stesso.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Get-CsKerberosAccountAssignment** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **Get-CsKerberosAccountAssignment** restituisce istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.KerberosAccount.KerberosAccountAssignment.

## Vedere anche

#### Ulteriori risorse

[New-CsKerberosAccountAssignment](new-cskerberosaccountassignment.md)  
[Remove-CsKerberosAccountAssignment](remove-cskerberosaccountassignment.md)  
[Set-CsKerberosAccountAssignment](set-cskerberosaccountassignment.md)

