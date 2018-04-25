---
title: New-CsKerberosAccount
TOCTitle: New-CsKerberosAccount
ms:assetid: 67ffa1b1-0ca5-410b-81f7-2375b9dbef3c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398485(v=OCS.15)
ms:contentKeyID: 49300841
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsKerberosAccount

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Crea un nuovo account Kerberos utilizzato per l'autenticazione IIS (Internet Information Service). Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    New-CsKerberosAccount -UserAccount <String> [-Confirm [<SwitchParameter>]] [-ContainerDN <String>] [-Force <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

I comandi riportati nell'esempio 1 creano un nuovo account Kerberos (litwareinc\\kerberostest) e assegnano quindi tale account al sito Redmond. A tale scopo, il primo comando nell'esempio crea un account con nome "litwareinc\\kerberostest". Questo account verrà creato nel contenitore dei computer nel dominio Litwareinc.com. Dopo la creazione dell'account, il secondo comando utilizza il cmdlet **New-CsKerberosAccountAssignment** per assegnare l'account Kerberos al sito Redmond.

Dopo che è stato assegnato il nuovo account, il comando finale chiama il cmdlet **Enable-CsTopology** per abilitare le modifiche.

    New-CsKerberosAccount -UserAccount "litwareinc\kerberostest" -ContainerDN "cn=Computers,dc=litwareinc,dc=com"
    
    New-CsKerberosAccountAssignment -UserAccount "litwareinc\kerberostest" -Identity "site:Redmond"
    Enable-CsTopology

## Descrizione dettagliata

In Microsoft Office Communications Server 2007 e Microsoft Office Communications Server 2007 R2 IIS viene eseguito con un account utente standard. Questo processo può causare problemi: se scade la password, è possibile che vengano persi i servizi Web, un evento spesso difficile da diagnosticare. Per evitare che si verifichi questo problema di scadenza delle password, Lync Server consente di creare un account computer (per un computer che in effetti non esiste) che può servire come entità di autenticazione per tutti i computer di un sito che eseguono IIS. Poiché questi account utilizzano il protocollo di autenticazione Kerberos, vengono denominati account Kerberos e il nuovo processo di autenticazione è noto come autenticazione Web Kerberos. In questo modo è possibile gestire tutti i server IIS utilizzando un singolo account.

Per eseguire i server con questa entità di autenticazione, è necessario innanzitutto creare un account computer utilizzando il cmdlet **New-CsKerberosAccount**. Questo account viene quindi assegnato a uno o più siti. Dopo l'assegnazione, l'associazione tra l'account e il sito di Lync Server viene abilitata con l'esecuzione del cmdlet **Enable-CsTopology**. Tra l'altro, questo cmdlet crea il nome dell'entità servizio (SPN, Service Principal Name) obbligatorio in Servizi di dominio Active Directory. I nomi SPN offrono alle applicazioni client un mezzo per individuare un particolare servizio.

Utenti autorizzati a utilizzare questo cmdlet: È necessario essere amministratori di dominio per poter utilizzare localmente il cmdlet **New-CsKerberosAccount**. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsKerberosAccount\\b"}

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
<td><p><em>UserAccount</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome account del nuovo account, utilizzare il formato nome_dominio\nome_utente. Ad esempio: -UserAccount &quot;litwareinc\kerberostest&quot;. Si noti che il comando avrà esito negativo, se l'account specificato già esiste.</p>
<p>Si noti che nonostante il nome (UserAccount), l'account creato con l'esecuzione del cmdlet <strong>New-CsKerberosAccount</strong> è in realtà un account computer e non un account utente.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>ContainerDN</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Nome distinto del contenitore di Active Directory in cui deve essere creato il nuovo account, ad esempio: -ContainerDN &quot;ou=Finance,dc=litwareinc,dc=com&quot;. Se questo parametro non viene specificato, il cmdlet <strong>New-CsKerberosAccount</strong> creerà il nuovo account nel contenitore dei computer in Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di evitare la visualizzazione di qualunque messaggio di errore non grave che potrebbe essere generato nel corso dell'esecuzione del comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\KerberosAccount.html&quot;.</p></td>
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

Nessuno. Il cmdlet **New-CsKerberosAccount** non accetta input tramite pipeline.

## Tipi restituiti

Il cmdlet **New-CsKerberosAccount** crea nuove istanze dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.KerberosAccount.KerberosAccount.

## Vedere anche

#### Ulteriori risorse

[New-CsKerberosAccountAssignment](new-cskerberosaccountassignment.md)

