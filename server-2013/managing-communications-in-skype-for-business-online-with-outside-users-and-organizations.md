---
title: Gestione delle comunicazioni con utenti e organizzazioni esterne
TOCTitle: Gestione delle comunicazioni con utenti e organizzazioni esterne
ms:assetid: 8a64f0fe-1e79-47d8-835e-548d7ac0757e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362813(v=OCS.15)
ms:contentKeyID: 56269934
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestione delle comunicazioni con utenti e organizzazioni esterne

 

_**Ultima modifica dell'argomento:** 2015-06-22_

I cmdlet seguenti consentono di gestire la federazione con i domini esterni e i provider di messaggistica istantanea pubblici:


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
<td><p><a href="new-csedgeallowallknowndomains.md">New-CsEdgeAllowAllKnownDomains</a></p></td>
<td><p>Consente agli utenti di comunicare con tutti i domini ad eccezione di quelli specificati nell'elenco dei domini bloccati.</p>
<p>Il servizio di federazione consente agli utenti di scambiarsi informazioni di messaggistica istantanea e sulla presenza con utenti di altri domini. In genere gli amministratori usano elenchi di domini consentiti e bloccati per specificare i domini esterni con cui gli utenti possono comunicare:</p></td>
</tr>
<tr class="even">
<td><p><a href="new-csedgeallowlist.md">New-CsEdgeAllowList</a></p></td>
<td><p>Limita le comunicazioni degli utenti a una raccolta di domini specificata.</p>
<p>Gli utenti potranno comunicare solo con i domini che compaiono nell'elenco dei domini consentiti.</p></td>
</tr>
<tr class="odd">
<td><p><a href="new-csedgedomainpattern.md">New-CsEdgeDomainPattern</a></p></td>
<td><p>Modifica gli elenchi dei domini bloccati o consentiti.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-cstenantfederationconfiguration.md">Get-CsTenantFederationConfiguration</a><br />
<a href="set-cstenantfederationconfiguration.md">Set-CsTenantFederationConfiguration</a></p></td>
<td><p>Abilita e disabilita la federazione con gli altri domini e con i provider pubblici.</p></td>
</tr>
<tr class="odd">
<td><p><a href="get-cstenanthybridconfiguration.md">Get-CsTenantHybridConfiguration</a><br />
<a href="set-cstenanthybridconfiguration.md">Set-CsTenantHybridConfiguration</a></p></td>
<td><p>Assegna i valori appropriati alle impostazioni di configurazione ibrida.</p>
<p>In una distribuzione ibrida, o di dominio condiviso, in un'organizzazione sono presenti sia utenti ospitati in Skype for Business online, sia utenti con account ospitati in Lync Server 2013. Per impostazione predefinita, gli utenti ospitati in Skype for Business online non hanno accesso all'intera gamma di funzionalità offerte da VoIP aziendale. Per fornire accesso a tali funzionalità agli utenti di Skype for Business online, gli amministratori devono assegnare i valori appropriati alle impostazioni di configurazione ibrida. Questi valori possono essere gestiti solo usando i cmdlet <strong>CsTenantHybridConfiguration</strong>.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-cstenantpublicprovider.md">Get-CsTenantPublicProvider</a><br />
<a href="set-cstenantpublicprovider.md">Set-CsTenantPublicProvider</a></p></td>
<td><p>Gestisce la federazione con i provider pubblici.</p>
<p>I provider pubblici sono organizzazioni che forniscono servizi di comunicazione SIP al pubblico. Quando si stabilisce una relazione di federazione con un provider pubblico, in realtà si stabilisce una federazione con qualsiasi utente che disponga di un account ospitato da tale provider.</p></td>
</tr>
</tbody>
</table>


È anche possibile gestire le impostazioni di federazione, sia per i domini federati che per i provider pubblici, tramite l'interfaccia di amministrazione di Skype for Business online:

![Impostazioni dell'organizzazione dell'Interfaccia di amministrazione di Lync Online](images/Dn362813.f860d03f-5906-49b0-bcc7-7634afe7005e(OCS.15).png "Impostazioni dell'organizzazione dell'Interfaccia di amministrazione di Lync Online")

## Vedere anche

#### Concetti

[Cmdlet di Lync Online](the-skype-for-business-online-cmdlets.md)  
[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

