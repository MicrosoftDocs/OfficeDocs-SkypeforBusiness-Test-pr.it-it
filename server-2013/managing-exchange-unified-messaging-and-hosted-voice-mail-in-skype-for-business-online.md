---
title: Gestione della messaggistica unificata di Exchange e della segreteria telefonica ospitata
TOCTitle: Gestione della messaggistica unificata di Exchange e della segreteria telefonica ospitata
ms:assetid: 844bf8d5-e093-4dcd-abcf-48dc70e8c73c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362822(v=OCS.15)
ms:contentKeyID: 56269932
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestione della messaggistica unificata di Exchange e della segreteria telefonica ospitata

 

_**Ultima modifica dell'argomento:** 2015-06-22_

I cmdlet seguenti possono essere usati per gestire il servizio Messaggistica unificata di Exchange e i criteri della segreteria telefonica ospitata:


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
<td><p><a href="get-csexumcontact.md">Get-CsExUmContact</a></p>
<p><a href="new-csexumcontact.md">New-CsExUmContact</a></p>
<p><a href="remove-csexumcontact.md">Remove-CsExUmContact</a></p>
<p><a href="set-csexumcontact.md">Set-CsExUmContact</a></p></td>
<td><p>Crea e gestisce gli oggetti contatto usati per i servizi Operatore automatico e Accesso sottoscrittore, quando Messaggistica unificata di Exchange è un servizio ospitato.</p>
<p>Skype for Business online collabora con la messaggistica unificata di Exchange per fornire diverse funzionalità vocali, tra cui Operatore automatico e Accesso sottoscrittore. Operatore automatico consente di rispondere automaticamente alle chiamate e instradarle all'utente corretto. Accesso sottoscrittore consente agli utenti di connettersi al servizio Messaggistica unificata di Exchange e recuperare posta elettronica, messaggi vocali, contatti e informazioni di calendario.</p>
<p>Quando la messaggistica unificata di Exchange è fornita come servizio ospitato, gli oggetti contatto usati per i servizi Operatore automatico e Accesso sottoscrittore vanno creati usando Windows PowerShell. Per creare e gestire questi oggetti si utilizzano i cmdlet CsExUmContact.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-cshostedvoicemailpolicy.md">Get-CsHostedVoicemailPolicy</a></p>
<p><a href="grant-cshostedvoicemailpolicy.md">Grant-CsHostedVoicemailPolicy</a></p></td>
<td><p>Gestisce i criteri della segreteria telefonica ospitata in uso nell'organizzazione. I criteri della segreteria telefonica ospitata specificano in modo in cui le chiamate senza risposta vengono instradate al servizio Messaggistica unificata di Exchange. Questi criteri hanno effetto solo sugli utenti abilitati per la segreteria telefonica ospitata della messaggistica unificata di Exchange. Per verificare se un utente è abilitato per la segreteria telefonica ospitata, eseguire un comando simile al seguente dal prompt di Windows PowerShell:</p>
<pre><code>Get-CsOnlineUser -Identity &quot;kenmyer@litwareinc.com&quot; | Select-Object HostedVoiceMail</code></pre></td>
</tr>
</tbody>
</table>


Non è possibile gestire le impostazioni della messaggistica unificata di Exchange e dei criteri della segreteria telefonica ospitata usando l'interfaccia di amministrazione di Skype for Business online.

## Vedere anche

#### Concetti

[Cmdlet di Lync Online](the-skype-for-business-online-cmdlets.md)  
[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

