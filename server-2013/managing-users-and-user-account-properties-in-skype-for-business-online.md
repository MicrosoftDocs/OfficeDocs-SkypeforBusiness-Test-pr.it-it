---
title: Gestione degli utenti e delle proprietà degli account utente
TOCTitle: Gestione degli utenti e delle proprietà degli account utente
ms:assetid: 5d13ab15-0e12-4bd0-a970-f130de980404
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362790(v=OCS.15)
ms:contentKeyID: 56269910
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestione degli utenti e delle proprietà degli account utente

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Il cmdlet seguenti consentono di gestire gli account utente di Skype for Business online.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="get-csonlineuser.md">Get-CsOnlineUser</a></p></td>
<td><p>Restituisce informazioni sugli utenti che dispongono di account ospitati nel proprio tenant Skype for Business online.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-csuseracp.md">Get-CsUserAcp</a><br />
<a href="remove-csuseracp.md">Remove-CsUserAcp</a><br />
<a href="set-csuseracp.md">Set-CsUserAcp</a></p></td>
<td><p>Consente di assegnare, modificare o rimuovere l'assegnazione di un provider di servizi di audioconferenza per singoli utenti.</p>
<p>Un provider di servizi di audioconferenza è una società di terze parti che offre servizi di conferenza alle organizzazioni, inclusi servizi avanzati quali traduzione immediata, trascrizione e assistenza diretta di un operatore durante la conferenza.</p>
<p>Questi cmdlet non restituiscono informazioni sui fornitori di servizi audio disponibili per l'assegnazione a tali utenti. Per ottenere queste informazioni, eseguire il comando seguente:</p>
<pre><code>Get-CsAudioConferencingProvider</code></pre></td>
</tr>
</tbody>
</table>



> [!WARNING]
> Il cmdlet Set-CsUser è incluso anche nel set di cmdlet disponibili per gli amministratori di Skype for Business online. Attualmente, tuttavia, non possibile utilizzare Set-CsUser per gestire Skype for Business online, tranne per l'impostazione del parametro AudioVideoDisabled. Se si tenta di eseguire il cmdlet con qualsiasi altro parametro, l'operazione avrà esito negativo e verrà visualizzato un messaggio di errore simile al seguente:<BR>Impossibile impostare “SipAddress”. Il parametro è limitato in PowerShell per il tenant remoto.



Per assegnare o annullare l'assegnazione di provider di servizi di audioconferenza agli account utente, è possibile usare anche l'interfaccia di amministrazione di Skype for Business online:

![Proprietà del servizio Conferenza telefonica con accesso esterno dell'Interfaccia di amministrazione di Lync](images/Dn362790.0c61f0c2-8aef-4020-a0a8-02580d43092a(OCS.15).png "Proprietà del servizio Conferenza telefonica con accesso esterno dell'Interfaccia di amministrazione di Lync")

## Vedere anche

#### Concetti

[Cmdlet di Lync Online](the-skype-for-business-online-cmdlets.md)  
[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

