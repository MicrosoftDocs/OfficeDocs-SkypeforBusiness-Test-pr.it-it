---
title: Set-CsKerberosAccountAssignment
TOCTitle: Set-CsKerberosAccountAssignment
ms:assetid: 16a964d2-2515-4a37-9686-3e377de58b14
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398232(v=OCS.15)
ms:contentKeyID: 49299798
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsKerberosAccountAssignment

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Associa a un sito un account Kerberos, che viene utilizzato per l'autenticazione Internet Information Services (IIS). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsKerberosAccountAssignment [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsKerberosAccountAssignment [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-UserAccount <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

I comandi riportati nell'esempio 1 associano un account Kerberos esistente (litwareinc\\keberostest) al sito Redmond e quindi abilitano la nuova associazione utilizzando il cmdlet **Enable-CsTopology**. A tale scopo, il primo comando dell'esempio utilizza il cmdlet **Set-CsKerberosAccountAssignment** per associare l'account litwareinc\\keberostest al sito Redmond. Il secondo comando quindi chiama il cmdlet **Enable-CsTopology** per creare il nome dell'entità servizio (SPN, Service Principal Name) necessario in Active Directory e abilitare l'assegnazione dell'account modificata.

    Set-CsKerberosAccountAssignment -UserAccount "litwareinc\keberostest" -Identity "site:Redmond"
    Enable-CsTopology

## Descrizione dettagliata

In Microsoft Office Communications Server 2007 e Microsoft Office Communications Server 2007 R2 IIS viene eseguito con un account utente standard. Questo processo può causare problemi: se scade la password, è possibile che vengano persi i servizi Web, un evento spesso difficile da diagnosticare. Per evitare che si verifichi questo problema di scadenza delle password, Lync Server consente di creare un account computer (per un computer che in effetti non esiste) che può servire come entità di autenticazione per tutti i computer di un sito che eseguono IIS. Poiché questi account utilizzano il protocollo di autenticazione Kerberos, vengono denominati account Kerberos e il nuovo processo di autenticazione è noto come autenticazione Web Kerberos. In questo modo è possibile gestire tutti i server IIS utilizzando un singolo account.

Per eseguire i propri server con questa nuova entità di autenticazione, è necessario innanzitutto creare un account computer utilizzando il cmdlet **New-CsKerberosAccount**. Questo account viene quindi assegnato a uno o più siti. Dopo l'assegnazione, viene abilitata l'associazione tra l'account e il sito di Lync Server eseguendo il cmdlet **Enable-CsTopology**. Tra l'altro, ciò determina la creazione del nome dell'entità servizio (SPN, Service Principal Name) necessario in Servizi di dominio Active Directory. I nomi SPN consentono alle applicazioni client di reperire un particolare servizio.

Il cmdlet **Set-CsKerberosAccountAssignment** consente di cambiare l'account Kerberos assegnato a un determinato sito. Questo cmdlet viene utilizzato per i siti che sono già associati a un account. Per assegnare un account a un sito che non è associato ad alcun account Kerberos, utilizzare il cmdlet **New-CsKerberosAccountAssignment**.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Set-CsKerberosAccountAssignment** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsKerberosAccountAssignment"}

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
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>Identificatore univoco del sito a cui è stato assegnato l'account Kerberos. Si tratta dell'identità del sito, non dell'account di computer. Ad esempio: -Identity &quot;site:Redmond&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>Oggetto KerberosAccountAssignment</p></td>
<td><p>Consente di passare al cmdlet un riferimento a un oggetto anziché impostare singoli valori di parametro.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserAccount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome dell'account da assegnare, nel formato nome_dominio\nome_utente. Ad esempio: -UserAccount &quot;litwareinc\kerberostest&quot;. La parte dell'account relativa al nome utente (kerberostest) è un nome NETBIOS e può essere composta da un massimo di 15 caratteri.</p>
<p>Si noti che, nonostante il nome UserAccount, l'account è in realtà un account computer, non un account utente.</p></td>
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

Oggetto Microsoft.Rtc.Management.WritableConfig.Settings.KerberosAccount.KerberosAccountAssignment. Il cmdlet **Set-CsKerberosAccountAssignment** accetta le istanze dell'oggetto assegnazione dell'account Kerberos inviate tramite pipeline.

## Tipi restituiti

Il cmdlet **Set-CsKerberosAccountAssignment** non restituisce oggetti o valori. Il cmdlet invece modifica le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.KerberosAccount.KerberosAccountAssignment.

## Vedere anche

#### Ulteriori risorse

[Get-CsKerberosAccountAssignment](get-cskerberosaccountassignment.md)  
[New-CsKerberosAccount](new-cskerberosaccount.md)  
[New-CsKerberosAccountAssignment](new-cskerberosaccountassignment.md)  
[Remove-CsKerberosAccountAssignment](remove-cskerberosaccountassignment.md)

