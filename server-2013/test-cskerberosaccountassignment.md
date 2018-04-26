---
title: Test-CsKerberosAccountAssignment
TOCTitle: Test-CsKerberosAccountAssignment
ms:assetid: 442bbb32-7ad1-40c4-bf17-42ecde0a7286
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425938(v=OCS.15)
ms:contentKeyID: 49300358
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Test-CsKerberosAccountAssignment

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Verifica la configurazione dell'account Kerberos assegnato a un sito. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Test-CsKerberosAccountAssignment -Identity <XdsIdentity> [-Report <String>]

## Esempi

## ESEMPIO 1

Il comando riportato nell'Esempio 1 consente di verificare che l'account Kerberos assegnato al sito Redmond sia configurato correttamente e stia funzionando secondo le aspettative.

    Test-CsKerberosAccountAssignment -Identity site:Redmond

## Descrizione dettagliata

In Microsoft Office Communications Server 2007 e Microsoft Office Communications Server 2007 R2 IIS viene eseguito con un account utente standard. Questo processo può causare problemi: se scade la password, è possibile che vengano persi i servizi Web, un evento spesso difficile da diagnosticare. Per evitare che si verifichi questo problema di scadenza delle password, Lync Server consente di creare un account computer (per un computer che in effetti non esiste) che può servire come entità di autenticazione per tutti i computer di un sito che eseguono IIS. Poiché questi account utilizzano il protocollo di autenticazione Kerberos, vengono denominati account Kerberos e il nuovo processo di autenticazione è noto come autenticazione Web Kerberos. In questo modo è possibile gestire tutti i server IIS utilizzando un singolo account.

Il cmdlet **Test-CsKerberosAccountAssignment** consente di verificare che un account Kerberos sia stato associato ad un dato sito, che questo account sia correttamente configurato e che stia funzionando secondo le aspettative.

Utenti che possono eseguire questo cmdlet: Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control, controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (compresi eventuali ruoli RBAC personalizzati creati autonomamente), eseguire il cmdlet riportato di seguito dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsKerberosAccountAssignment"}

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
<td><p>Nome del sito a cui è stato assegnato l'account Kerberos. Ad esempio: -Identity &quot;site:Redmond&quot;.</p></td>
</tr>
<tr class="even">
<td><p><em>Report</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.String</p></td>
<td><p>Consente di specificare un percorso per il file di log creato durante l'esecuzione del cmdlet. Ad esempio: -Report &quot;C:\Logs\TestKerberos.html&quot;.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. Il cmdlet **Test-CsKerberosAccountAssignment** non accetta input da pipeline.

## Tipi restituiti

Il cmdlet **Test-CsKerberosAccountAssignment** non restituisce oggetti o valori.

## Vedere anche

#### Ulteriori risorse

[Get-CsKerberosAccountAssignment](get-cskerberosaccountassignment.md)  
[New-CsKerberosAccountAssignment](new-cskerberosaccountassignment.md)  
[Remove-CsKerberosAccountAssignment](remove-cskerberosaccountassignment.md)  
[Set-CsKerberosAccountAssignment](set-cskerberosaccountassignment.md)

