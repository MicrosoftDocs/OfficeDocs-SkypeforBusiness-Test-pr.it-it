---
title: Set-CsKerberosAccountPassword
TOCTitle: Set-CsKerberosAccountPassword
ms:assetid: 837292b9-3c08-4c3c-a49d-3f9492518ddd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398659(v=OCS.15)
ms:contentKeyID: 49301174
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsKerberosAccountPassword

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Individua tutti i server che eseguono i servizi Web in un sito a cui è stato assegnato un account Kerberos e quindi aggiorna le impostazioni di configurazione di Internet Information Services (IIS) in ognuno di questi server. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Set-CsKerberosAccountPassword -UserAccount <String> <COMMON PARAMETERS>

    Set-CsKerberosAccountPassword -FromComputer <Fqdn> -ToComputer <Fqdn> <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-Report <String>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 imposta la password dell'account Kerberos litwareinc\\kerberostest.

    Set-CsKerberosAccountPassword -UserAccount "litwareinc\kerberostest"

## ESEMPIO 2

Nell'esempio 2 la password dell'account Kerberos viene copiata dal computer atl-cs-001.litwareinc.com nel computer dublin-cs-001.litwareinc.com.

    Set-CsKerberosAccountPassword -FromComputer "atl-cs-001.litwareinc.com" -ToComputer "dublin-cs-001.litwareinc.com"

## Descrizione dettagliata

In Microsoft Office Communications Server 2007 e Microsoft Office Communications Server 2007 R2 IIS viene eseguito con un account utente standard. Questo comportamento può causare alcuni problemi. Se la password scade, esiste il rischio di perdere i servizi Web, un problema spesso difficile da diagnosticare. Per ovviare al problema della scadenza delle password, Lync Server consente di creare un account computer (per un computer che in effetti non esiste) da utilizzare come entità di autenticazione per tutti i computer di un sito che eseguono IIS. Poiché utilizzano il protocollo di autenticazione Kerberos, questi account sono indicati come account Kerberos e il nuovo processo di autenticazione è noto come autenticazione Web Kerberos. In questo modo è possibile gestire tutti i server IIS utilizzando un unico account.

Per eseguire i server con questa nuova entità di autenticazione, è necessario innanzitutto creare un account computer utilizzando il cmdlet **New-CsKerberosAccount**. Questo account viene quindi assegnato a uno o più siti. Dopo l'assegnazione, l'associazione tra l'account e il sito di Lync Server viene abilitata con l'esecuzione del cmdlet **Enable-CsTopology**. Tra l'altro, questo cmdlet crea il nome dell'entità servizio (SPN, Service Principal Name) obbligatorio in Servizi di dominio Active Directory. I nomi SPN offrono alle applicazioni client un mezzo per individuare un particolare servizio.

Una volta creata una nuova associazione, il cmdlet **Set-CsKerberosAccountPassword** consente di modificare la password assegnata all'account e, operazione altrettanto importante, di aggiornare la password in ogni computer in cui viene utilizzato l'account di test Kerberos specificato per l'autenticazione Web Kerberos.

Il cmdlet può inoltre utilizzare i parametri ToComputer e FromComputer per copiare queste informazioni di configurazione da un computer a un altro.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Set-CsKerberosAccountPassword** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsKerberosAccountPassword"}

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
<td><p><em>FromComputer</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome di dominio completo (FQDN) del computer contenente la password dell'account Kerberos che verrà copiata in un altro computer. Non è possibile utilizzare questo parametro se si utilizza il parametro UserAccount.</p></td>
</tr>
<tr class="even">
<td><p><em>ToComputer</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>Microsoft.Rtc.Management.Deploy.Fqdn</p></td>
<td><p>Nome FQDN del computer in cui verrà copiata la password dell'account Kerberos. Non è possibile utilizzare questo parametro se si utilizza il parametro UserAccount.</p></td>
</tr>
<tr class="odd">
<td><p><em>UserAccount</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>Nome dell'account di cui deve essere cambiata la password. Per questo nome di account deve essere utilizzato il formato nome_dominio\nome_utente, ad esempio -UserAccount &quot;litwareinc\kerberostest&quot;.</p>
<p>Nonostante il nome UserAccount, l'account in realtà è un account computer e non un account utente.</p></td>
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
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\SetKerberosPassword.html&quot;.</p></td>
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

Nessuno.

## Tipi restituiti

Il cmdlet **Set-CsKerberosAccountPassword** non restituisce alcun oggetto o valore. Modifica invece le istanze esistenti dell'oggetto Microsoft.Rtc.Management.WritableConfig.Settings.KerberosAccount.KerberosAccount.

