---
title: Gestione dei criteri
TOCTitle: Gestione dei criteri
ms:assetid: 91372888-a96e-44db-a0dc-d08facbfce87
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362826(v=OCS.15)
ms:contentKeyID: 56269944
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestione dei criteri

 

_**Ultima modifica dell'argomento:** 2015-06-22_

I cmdlet seguenti vengono usati per gestire i criteri di Skype for Business online. I criteri consentono di stabilire le funzionalità di Skype for Business online disponibili per gli utenti e per l'organizzazione nel suo complesso.


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
<td><p><a href="get-csclientpolicy.md">Get-CsClientPolicy</a><br />
<a href="grant-csclientpolicy.md">Grant-CsClientPolicy</a></p></td>
<td><p>I criteri client consentono di stabilire le funzionalità di Lync disponibili per gli utenti. Ad esempio, è possibile permettere ad alcuni utenti di trasferire i file, ma non ad altri.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-csconferencingpolicy.md">Get-CsConferencingPolicy</a><br />
<a href="grant-csconferencingpolicy.md">Grant-CsConferencingPolicy</a></p></td>
<td><p>I criteri di conferenza determinano le caratteristiche e le funzionalità che possono essere usate in una conferenza, ad esempio se includere o meno nella conferenza le funzionalità audio e video IP e il numero massimo di persone che possono partecipare a una riunione.</p></td>
</tr>
<tr class="odd">
<td><p><a href="get-csexternalaccesspolicy.md">Get-CsExternalAccessPolicy</a><br />
<a href="grant-csexternalaccesspolicy.md">Grant-CsExternalAccessPolicy</a></p></td>
<td><p>I criteri di accesso esterno consentono di stabilire se gli utenti interni possono comunicare con gli utenti dei domini federati e/o se possono comunicare con utenti che dispongono di account presso provider di servizi di messaggistica istantanea pubblici, come AOL o Windows Live.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-csvoicepolicy.md">Get-CsVoicePolicy</a><br />
<a href="grant-csvoicepolicy.md">Grant-CsVoicePolicy</a><br />
<a href="remove-csvoicepolicy.md">Remove-CsVoicePolicy</a></p></td>
<td><p>I criteri vocali sono usati per gestire le funzionalità di VoIP aziendale, ad esempio lo squillo simultaneo (vale a dire la capacità di far squillare un secondo telefono ogni volta che si riceve una chiamata sul telefono dell'ufficio) e l'inoltro di chiamata.</p></td>
</tr>
</tbody>
</table>


Alcune impostazioni dei criteri relativi alle conferenze possono essere gestite anche mediante l'interfaccia di amministrazione di Skype for Business online:

![Proprietà delle opzioni generali dell'Interfaccia di amministrazione di Lync](images/Dn362833.acf90793-7ee4-4faf-b791-f149dd5df2a5(OCS.15).png "Proprietà delle opzioni generali dell'Interfaccia di amministrazione di Lync")

Le impostazioni dei criteri di accesso esterno possono essere gestite anche mediante l'interfaccia di amministrazione di Skype for Business online:

![Opzioni per le comunicazioni esterne dell'Interfaccia di amministrazione](images/Dn362826.e5cfb159-b096-463e-b1ef-2b42eb29168a(OCS.15).png "Opzioni per le comunicazioni esterne dell'Interfaccia di amministrazione")

## Vedere anche

#### Concetti

[Cmdlet di Lync Online](the-skype-for-business-online-cmdlets.md)  
[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

