---
title: New-CsKerberosAccountAssignment
TOCTitle: New-CsKerberosAccountAssignment
ms:assetid: 02145fe6-8b7a-4508-8b3c-b9671b5bfcff
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398074(v=OCS.15)
ms:contentKeyID: 49299491
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsKerberosAccountAssignment

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Assegna a un sito un account Kerberos, utilizzato per l'autenticazione IIS. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsKerberosAccountAssignment -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-UserAccount <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

I comandi riportati nell'esempio 1 assegnano un account Kerberos (litwareinc\\kerberostest) al sito Redmond e successivamente chiamano il cmdlet **Enable-CsTopology** per abilitare l'assegnazione. A tale scopo, il primo comando nell'esempio utilizza il cmdlet **New-CsKerberosAccountAssignment** per associare l'account "litwareinc\\kerberostest" al sito Redmond. Il secondo comando quindi chiama il cmdlet **Enable-CsTopology** per creare il nome dell'entità servizio necessario in Servizi di dominio Active Directory e abilitare la nuova assegnazione.

    New-CsKerberosAccountAssignment -UserAccount "litwareinc\kerberostest" -Identity "site:Redmond"
    Enable-CsTopology

## Descrizione dettagliata

In Microsoft Office Communications Server 2007 e Microsoft Office Communications Server 2007 R2 IIS viene eseguito con un account utente standard, con il rischio che possano verificarsi problemi. Se la password scade, è possibile perdere i servizi Web, un problema spesso difficile da diagnosticare. Per evitare il problema della scadenza delle password, Lync Server consente di creare un account computer (per un computer che in effetti non esiste) da utilizzare come entità di autenticazione per tutti i computer di un sito che eseguono IIS. Poiché questi account utilizzano il protocollo di autenticazione Kerberos, vengono denominati account Kerberos e il nuovo processo di autenticazione è noto come autenticazione Web Kerberos. In questo modo è possibile gestire tutti i server IIS utilizzando un singolo account.

Per eseguire i server con questa nuova entità di autenticazione, è necessario innanzitutto creare un account computer utilizzando il cmdlet **New-CsKerberosAccount**. Questo account viene quindi assegnato a uno o più siti. Dopo l'assegnazione, l'associazione tra l'account e il sito di Lync Server viene abilitata con l'esecuzione del cmdlet **Enable-CsTopology**. Questo cmdlet crea inoltre il nome dell'entità servizio (SPN) in Servizi di dominio Active Directory. I nomi SPN offrono alle applicazioni client la possibilità di individuare un particolare servizio.

Il cmdlet **New-CsKerberosAccountAssignment** consente di assegnare un account Kerberos a un sito attualmente non associato a un account. Per modificare un sito già associato a un account Kerberos è invece possibile utilizzare il cmdlet **Set-CsKerberosAccountAssignment**.

Utenti che possono eseguire questo cmdlet: per impostazione predefinita, i membri dei gruppi riportati di seguito sono autorizzati ad eseguire il cmdlet **New-CsKerberosAccountAssignment** in locale: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsKerberosAccountAssignment"}

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
<td><p>Identificatore univoco del sito a cui deve essere assegnato l'account Kerberos. Corrisponde all'identità del sito, non dell'account computer. Ad esempio: -Identity &quot;site:Redmond&quot;.</p></td>
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
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Crea un riferimento a un oggetto senza eseguire realmente il commit dell'oggetto come modifica permanente. Se si assegna l'output del cmdlet chiamato con questo parametro a una variabile, è possibile apportare modifiche alle proprietà del riferimento all'oggetto e quindi eseguire il commit di queste modifiche chiamando il cmdlet Set- corrispondente.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserAccount</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome dell'account da assegnare, nel formato nome_dominio\nome_utente. Ad esempio: -UserAccount &quot;litwareinc\kerberostest&quot;. La parte dell'account relativa al nome utente (kerberostest) è un nome NETBIOS e può essere composta da un massimo di 15 caratteri.</p>
<p>Nonostante il nome UserAccount, l'account è in effetti un account computer, non un account utente.</p></td>
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

Nessuno. Il cmdlet **New-CsKerberosAccountAssignment** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **New-CsKerberosAccountAssignment** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.KerberosAccount.KerberosAccountAssignment.

## Vedere anche

#### Ulteriori risorse

[Get-CsKerberosAccountAssignment](get-cskerberosaccountassignment.md)  
[New-CsKerberosAccount](new-cskerberosaccount.md)  
[Remove-CsKerberosAccountAssignment](remove-cskerberosaccountassignment.md)  
[Set-CsKerberosAccountAssignment](set-cskerberosaccountassignment.md)

