---
title: Remove-CsKerberosAccountAssignment
TOCTitle: Remove-CsKerberosAccountAssignment
ms:assetid: f878fed1-ee6d-4275-8f76-2bc134e465c2
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413052(v=OCS.15)
ms:contentKeyID: 49302518
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsKerberosAccountAssignment

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Rimuove una o più assegnazioni di account Kerberos. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Remove-CsKerberosAccountAssignment -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 rimuove l'assegnazione dell'account Kerberos dal sito Redmond, quindi esegue la chiamata al cmdlet **Enable-CsTopology** per completare la disabilitazione dell'autenticazione Web Kerberos.

    Remove-CsKerberosAccountAssignment -Identity "site:Redmond"
    Enable-CsTopology

## ESEMPIO 2

Nell'esempio 2 vengono eliminate tutte le assegnazioni dell'account Kerberos attualmente in uso. A questo scopo, il primo comando chiama il cmdlet **Get-CsKerberosAccountAssignment**, senza parametri, per restituire una raccolta di tutte le assegnazioni dell'account Kerberos. La raccolta viene quindi inviata tramite pipe al cmdlet **Remove-CsKerberosAccountAssignment**, che elimina tutte le assegnazioni della raccolta. Al termine di questa operazione, il secondo comando dell'esempio chiama il cmdlet **Enable-CsTopology** per completare la disabilitazione dell'autenticazione Web Kerberos.

    Get-CsKerberosAccountAssignment | Remove-CsKerberosAccountAssignment
    Enable-CsTopology

## Descrizione dettagliata

In Microsoft Office Communications Server 2007 e Microsoft Office Communications Server 2007 R2, viene eseguito con un account utente standard. Ciò può causare problemi: se la password scade è possibile che si perdano i servizi servizi Web, un problema spesso difficile da diagnosticare. Per evitare il problema della scadenza delle password, Lync Server consente di creare un account computer (per un computer che in effetti non esiste) da utilizzare come entità di autenticazione per tutti i computer in un sito che eseguono IIS. Poiché questi account utilizzano il protocollo di autenticazione Kerberos, vengono denominati account Kerberos e il nuovo processo di autenticazione è noto come autenticazione Web Kerberos. In questo modo è possibile gestire tutti i server IIS utilizzando un singolo account.

Per eseguire i server in uso con questa nuova entità di autenticazione, è necessario in primo luogo creare un account del computer (non collegato al computer effettivo) mediante il cmdlet **New-CsKerberosAccount**; tale account viene quindi assegnato a uno o più siti. Una volta effettuata l'assegnazione, l'associazione viene abilitata eseguendo il cmdlet **Enable-CsTopology**; ciò consente, fra le altre cose, di creare il nome SPN (Service Principal Name) richiesto in Servizi di dominio Active Directory. I nomi SPN offrono alle applicazioni client un mezzo per individuare un particolare servizio.

Ogni sito Lync Server può essere associato al massimo con un unico account Kerberos. Tuttavia, ogni account può essere associato a più siti. È possibile utilizzare il cmdlet **Remove-CsKerberosAccountAssignment** in qualsiasi momento per rimuovere l'associazione fra un sito e un account. Questo cmdlet non elimina l'account in questione, semplicemente, permette l'associazione fra l'account e il sito, disabilitando di fatto l'autenticazione Web Kerberos per quel sito.

Dopo aver eseguito il cmdlet **Remove-CsKerberosAccountAssignment**, è necessario eseguire il cmdlet **Enable-CsTopology**. In questo modo si rimuove il nome SPN dell'account da Active Directory e si disabilita completamente l'autenticazione Web Kerberos.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi seguenti sono autorizzati a eseguire il cmdlet **Remove-CsKerberosAccountAssignment** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli del controllo di accesso basato sui ruoli (RBAC) ai quali è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati creati dall'utente), eseguire il comando seguente dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsKerberosAccountAssignment"}

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
<td><p>Identificatore univoco del sito per cui si desidera rimuovere l'assegnazione dell'account Kerberos. Si tratta dell'identità del sito, non dell'account Kerberos. Ad esempio: -Identity &quot;site:Redmond&quot;.</p></td>
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
<td><p>Se presente, consente di ignorare tutti i messaggi di errore ad eccezione dei messaggi di errori irreversibili.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.KerberosAccount.KerberosAccountAssignment. Il cmdlet **Remove-CsKerberosAccountAssignment** accetta istanze inviate tramite pipe dell'oggetto di assegnazione account Kerberos.

## Tipi restituiti

Nessuno. Il cmdlet **Remove-CsKerberosAccountAssignment** non restituisce alcun valore o oggetto. In realtà il cmdlet elimina le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.KerberosAccount.KerberosAccountAssignment.

## Vedere anche

#### Ulteriori risorse

[Get-CsKerberosAccountAssignment](get-cskerberosaccountassignment.md)  
[New-CsKerberosAccountAssignment](new-cskerberosaccountassignment.md)  
[Set-CsKerberosAccountAssignment](set-cskerberosaccountassignment.md)

