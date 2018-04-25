---
title: Revoke-CsClientCertificate
TOCTitle: Revoke-CsClientCertificate
ms:assetid: 27d6d4d9-f8ed-4942-b7cf-dd308dafb5bc
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425748(v=OCS.15)
ms:contentKeyID: 49299989
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Revoke-CsClientCertificate

 

_**Ultima modifica dell'argomento:** 2015-03-09_

I certificati client consentono di autenticare gli utenti quando eseguono l'accesso a Lync Server. I certificati sono particolarmente utili per i telefoni e altri dispositivi che eseguono Lync Mobile dove è problematico immettere un nome utente e/o una password. Il cmdlet **Revoke-CsClientCertificate** consente agli amministratori di revocare i certificati client emessi per un utente. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Revoke-CsClientCertificate -Identity <UserIdParameter> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## Esempi

## ESEMPIO 1

Il comando riportato nell'esempio 1 revoca tutti i certificati client attualmente assegnati a Ken Myer. A tale scopo, viene chiamato il cmdlet **Revoke-CsClientCertificate** seguito dall'identità dell'utente i cui certificati devono essere revocati.

    Revoke-CsClientCertificate -Identity "Ken Myer"

## ESEMPIO 2

Nell'esempio 2 vengono revocati tutti i certificati client emessi nell'organizzazione. A tale scopo, viene innanzitutto chiamato il cmdlet **Get-CsUser** per restituire una raccolta di tutti gli utenti dell'organizzazione che sono stati abilitati per Lync Server. Questa raccolta viene inviata tramite pipe al cmdlet **Revoke-CsClientCertificate**, che elimina i certificati di ogni utente incluso nella raccolta.

    Get-CsUser | Revoke-CsClientCertificate

## Descrizione dettagliata

I certificati client costituiscono un'alternativa per gli utenti per essere autenticati da Lync Server. Anziché fornire nome utente e password, gli utenti forniscono al sistema un certificato X.509. Questo certificato deve avere un nome soggetto o un nome alternativo del soggetto che identifica l'utente. Ai fini dell'autenticazione, gli utenti devono digitare unicamente un PIN. Per gli utenti di telefoni cellulari in genere è più semplice digitare un PIN anziché un nome utente e/o una password alfanumerici.

In qualunque momento gli amministratori possono revocare i certificati client emessi per un utente utilizzando il cmdlet **Revoke-CsClientCertificate**. Il cmdlet **Revoke-CsClientCertificate** revoca tutti i certificati client emessi dal server per quell'utente.

Il cmdlet **Revoke-CsClientCertificate** non elimina i certificati dal dispositivo client. I certificati vengono solo eliminati dal server. Questo è tuttavia sufficiente a impedire a un client di utilizzare i certificati per farsi autenticare. Se infatti un certificato non viene trovato nel server, la richiesta di autenticazione viene rifiutata.

Si noti che, per impostazione predefinita, le eccezioni del firewall per SQL Server Express non sono abilitate quando si installa Lync Server Standard Edition. Ciò significa che non sarà possibile eseguire il cmdlet **Revoke-CsClientCertificate** da un'istanza remota di Windows PowerShell perché il comando non è in grado di attraversare il firewall e accedere al database di SQL Server Express. È tuttavia possibile eseguire il cmdlet localmente, ovvero nel server Standard Edition stesso. Se si sta utilizzando la versione Standard Edition ed è necessario eseguire il cmdlet **Revoke-CsClientCertificate** da postazione remota, abilitare manualmente le eccezioni del firewall per SQL Server Express.

Utenti autorizzati a utilizzare questo cmdlet: per impostazione predefinita, il cmdlet **Revoke-CsClientCertificate** può essere utilizzato localmente dai membri dei seguenti gruppi: RTCUniversalServerAdmins. Per ottenere un elenco di tutti i ruoli RBAC (controllo dell'accesso basato sui ruoli) a cui è stato assegnato questo cmdlet (inclusi eventuali ruoli RBAC personalizzati), utilizzare il seguente comando dal prompt di Windows PowerShell:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Revoke-CsClientCertificate"}

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
<td><p>Indica l'identità dell'account utente i cui certificati devono essere revocati. Le identità utente possono essere specificate con uno dei quattro formati riportati di seguito: 1) l'indirizzo SIP (Session Initiation Protocol) dell'utente; 2) il nome dell'entità utente (UPN); 3) il nome del dominio e il nome di accesso dell'utente nel formato dominio\accesso (ad esempio, litwareinc\kenmyer); 4) il nome visualizzato Active Directory dell'utente (ad esempio, Ken Myer). Alle identità utente è anche possibile fare riferimento utilizzando il nome distinto Active Directory dell'utente.</p>
<p></p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Descrive ciò che accadrebbe se si eseguisse il comando senza eseguirlo realmente.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Valore stringa oppure oggetto Microsoft.Rtc.Management.ADConnect.Schema.ADUser. Il cmdlet **Revoke-CsClientCertificate** accetta l'input da pipeline di valori stringa che rappresentano l'identità di un account utente. Il cmdlet accetta inoltre l'input da pipeline di oggetti utente.

## Tipi restituiti

Nessuno. Il cmdlet **Revoke-CsClientCertificate** revoca le istanze dell'oggetto Microsoft.Rtc.Management.UserPinService.CertInfoDetails.

## Vedere anche

#### Ulteriori risorse

[Get-CsClientCertificate](get-csclientcertificate.md)

