---
title: Unlock-CsClientPin
TOCTitle: Unlock-CsClientPin
ms:assetid: eef7877c-0302-4ce7-84f5-06968d0623b9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412982(v=OCS.15)
ms:contentKeyID: 49302406
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Unlock-CsClientPin

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente a un amministratore di sbloccare il PIN per un determinato utente. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Unlock-CsClientPin -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Nell'esempio 1, il cmdlet **Unlock-CsClientPin** viene utilizzato per sbloccare il codice PIN appartenente all'utente litwareinc\\davidegarghentini.

    Unlock-CsClientPin -Identity "litwareinc\kenmyer"

## ESEMPIO 2

Nell'esempio 2, il cmdlet **Unlock-CsClientPin** viene utilizzato per sbloccare tutti i codici PIN attualmente bloccati. A tale scopo, il cmdlet **Get-CsUser** viene innanzitutto utilizzato per restituire una raccolta di tutti gli utenti abilitati per Lync Server. La raccolta viene quindi inviata tramite pipe al cmdlet **Get-CsClientPinInfo** che viene utilizzato con il cmdlet **Where-Object** per selezionare solo gli utenti la cui proprietà IsLockedOut è uguale (-eq) a True ($True).

La raccolta filtrata risultante viene quindi inviata tramite pipe al cmdlet **Unlock-CsClientPin**, che sblocca il codice PIN dei singoli utenti con PIN precedentemente bloccato.

    Get-CsUser | Get-CsClientPinInfo | Where-Object {$_.IsLockedOut -eq $True} | Unlock-CsClientPin 

## Descrizione dettagliata

Lync Server consente agli utenti di connettersi al sistema o di partecipare a conferenze PSTN (Public Switched Telephone Network) tramite telefono. Per accedere al sistema o partecipare a una conferenza, l'utente in genere deve immettere un nome utente e una password. L'immissione del nome utente e della password può tuttavia costituire un problema se il telefono in uso non dispone di una tastiera alfanumerica. Per questo motivo, con Lync Server è possibile fornire agli utenti codici PIN solo numerici. Quando richiesto, gli utenti possono quindi accedere al sistema o partecipare a una conferenza immettendo il codice PIN anziché il nome utente e la password.

Ciò è tuttavia possibile solo se il codice PIN dell'utente è sbloccato. Se un codice PIN è stato bloccato perché l'utente non è riuscito più volte a eseguire l'accesso o perché un amministratore ha esplicitamente applicato un blocco, l'utente non potrà accedere al sistema o partecipare a una conferenza utilizzando l'autenticazione tramite PIN. L'utente tuttavia potrà comunque utilizzare un'applicazione come Lync per accedere al sistema fornendo un nome utente e una password. Se un codice PIN è stato bloccato, esiste un solo modo per consentire di nuovo all'utente di accedere al sistema con l'autenticazione tramite PIN: il codice PIN bloccato deve essere sbloccato da un amministratore. Questa operazione può essere eseguita utilizzando il cmdlet **Unlock-CsClientPin**.

Per impostazione predefinita, le eccezioni del firewall per SQL Server Express non sono abilitate quando si installa Lync Server Standard Edition. Questo significa che non sarà possibile eseguire il cmdlet **Unlock-CsClientPin** da un'istanza remota di Windows PowerShell, dal momento che il comando non sarà in grado di attraversare il firewall e accedere al database di SQL Server Express. Sarà comunque possibile eseguire il cmdlet localmente sul server Standard Edition. Per poter eseguire il cmdlet **Unlock-CsClientPin** in remoto su un server Standard Edition, sarà necessario abilitare manualmente le eccezioni del firewall per SQL Server Express.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Unlock-CsClientPin** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Unlock-CsClientPin"}

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
<td><p>Identità dell'account utente per cui deve essere sbloccato il codice PIN. Le identità utente possono essere specificate con uno dei quattro formati riportati di seguito: 1) l'indirizzo SIP dell'utente, 2) il nome dell'entità utente (UPN, User Principal Name), 3) il nome di dominio e il nome di accesso dell'utente nel formato dominio\accesso (ad esempio, litwareinc\davidegarghentini), 4) il nome visualizzato Active Directory dell'utente (ad esempio, Davide Garghentini). È possibile fare riferimento alle identità utente anche utilizzando il nome distinto Active Directory dell'utente.</p>
<p>È inoltre possibile utilizzare il carattere jolly asterisco (*) quando si utilizza il valore di Display Name come parametro Identity dell'utente. Ad esempio, l'identità &quot;* Smith&quot; restituisce tutti gli utenti il cui nome visualizzato termina con il valore stringa &quot; Smith&quot;.</p></td>
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
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
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

Valore stringa o oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Il cmdlet **Unlock-CsClientPin** accetta l'input da pipeline dei valori stringa che rappresentano l'identità di un account utente. Il cmdlet accetta inoltre l'input da pipeline di oggetti utente.

## Tipi restituiti

Il cmdlet **Unlock-CsClientPin** non restituisce un oggetto o un valore. In realtà il cmdlet configura una o più istanze dell'oggetto Microsoft.Rtc.Management.UserPinService.PinInfoDetails.

## Vedere anche

#### Ulteriori risorse

[Get-CsClientPinInfo](get-csclientpininfo.md)  
[Lock-CsClientPin](lock-csclientpin.md)  
[Set-CsClientPin](set-csclientpin.md)

