---
title: Get-CsClientCertificate
TOCTitle: Get-CsClientCertificate
ms:assetid: 0949288e-9df2-42c4-8297-0dc4cb40d544
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398143(v=OCS.15)
ms:contentKeyID: 49299613
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Get-CsClientCertificate

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Restituisce informazioni sui certificati client che sono stati emessi per un utente. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Get-CsClientCertificate -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 restituisce tutti i certificati client rilasciati a Ken Myer.

    Get-CsClientCertificate -Identity "Ken Myer"

## ESEMPIO 2

Nell'esempio 2 vengono restituiti tutti i certificati client rilasciati a Ken Myer con scadenza anteriore al 1° settembre 2011. A tale scopo, nel comando viene innanzitutto utilizzato il cmdlet **Get-CsClientCertificate** per restituire una raccolta di tutti i certificati client rilasciati a Ken Myer. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i certificati con la proprietà ExpirationTime impostata su un valore anteriore al 1° settembre 2011 (9/1/2011). Per la data specificata in questo esempio (9/1/2011) viene utilizzato il formato statunitense dei valori di data e ora. Le date devono essere specificate utilizzando un formato compatibile con le impostazioni definite in Opzioni internazionali e della lingua.

    Get-CsClientCertificate -Identity "Ken Myer" | Where-Object {$_.ExpirationTime -lt "9/1/2011"}

## ESEMPIO 3

Nell'esempio 3 vengono restituiti tutti i certificati client emessi per Ken Myer a partire dal 1° gennaio 2010. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsClientCertificate** per restituire una raccolta di tutti i certificati client emessi per Ken Myer. Questa raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo i certificati con la proprietà PublicationTime impostata su un valore successivo al 1° gennaio 2010 (1/1/2010).

    Get-CsClientCertificate -Identity "Ken Myer" | Where-Object {$_.PublicationTime -gt "1/1/2010"}

## ESEMPIO 4

Il comando riportato nell'esempio 4 restituisce i certificati client di tutti gli utenti abilitati per Lync Server e assegnati a un pool di registrazione. Se si tenta di recuperare informazioni relative ai certificati per un utente che non è stato assegnato a un pool di registrazione, verrà restituito un errore. A tale scopo, il comando chiama innanzitutto il cmdlet **Get-CsUser** senza alcun parametro. La raccolta viene quindi inviata tramite pipe al cmdlet **Where-Object**, che seleziona solo gli utenti con la proprietà RegistrarPool diversa da un valore Null. Questa raccolta filtrata viene quindi inviata tramite pipe al cmdlet **Get-CsClientCertificate**, che restituisce i certificati assegnati a ogni utente della raccolta.

    Get-CsUser | Where-Object {$_.RegistrarPool -ne $Null} | Get-CsClientCertificate

## Descrizione dettagliata

I certificati client costituiscono un'alternativa per gli utenti per essere autenticati da Lync Server. Anziché specificare un nome utente e una password, gli utenti presentano al sistema un certificato X.509. Questo certificato deve essere dotato di un nome soggetto o di un nome alternativo del soggetto che identifichi l'utente. Ai fini dell'autenticazione, gli utenti devono digitare unicamente un codice PIN. Agli utenti di telefoni cellulari risulta in genere più semplice digitare un PIN piuttosto che un nome utente e/o una password alfanumerica.

Il cmdlet **Get-CsClientCertificate** consente agli amministratori di recuperare informazioni sui certificati client di Lync Server rilasciati ai propri utenti. Tra queste informazioni sono incluse la data e l'ora di rilascio e di scadenza del certificato.

Per impostazione predefinita, le eccezioni del firewall per SQL Server Express non sono abilitate quando si installa Lync Server Standard Edition. Questo significa che non sarà possibile eseguire il cmdlet **Get-CsClientCertificate** da un'istanza remota di Windows PowerShell, dal momento che il comando non sarà in grado di attraversare il firewall e accedere al database di SQL Server Express. Sarà comunque possibile eseguire il cmdlet localmente nel server Standard Edition. Per poter eseguire il cmdlet **Get-CsClientCertificate** in remoto in un server Standard Edition, sarà necessario abilitare manualmente le eccezioni del firewall per SQL Server Express.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Get-CsClientCertificate** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsClientCertificate"}

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
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Indica l'identità dell'account utente di cui si desidera recuperare le informazioni sul certificato. Le identità utente possono essere specificate con uno dei quattro formati riportati di seguito: 1) l'indirizzo SIP (Session Initiation Protocol) dell'utente, 2) il nome dell'entità utente (UPN, User Principal Name), 3) il nome di dominio e il nome di accesso dell'utente nel formato dominio\accesso (ad esempio, litwareinc\kenmyer) e 4) il nome visualizzato Active Directory dell'utente (ad esempio, Ken Myer). È inoltre possibile fare riferimento a un account utente utilizzando il nome distinto Active Directory dell'utente.</p>
<p>Non è possibile utilizzare caratteri jolly quando si specifica l'identità dell'utente.</p>
<p></p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Viene visualizzata una richiesta di conferma prima di eseguire il comando.</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Valore stringa oppure oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Il cmdlet **Get-CsClientCertificate** accetta l'input da pipeline di valori stringa che rappresentano l'identità di un account utente. Il cmdlet accetta inoltre l'input da pipeline di oggetti utente.

## Tipi restituiti

Il cmdlet **Get-CsClientCertificate** restituisce istanze dell'oggetto Microsoft.Rtc.Management.UserPinService.CertInfoDetails.

## Vedere anche

#### Ulteriori risorse

[Revoke-CsClientCertificate](revoke-csclientcertificate.md)

