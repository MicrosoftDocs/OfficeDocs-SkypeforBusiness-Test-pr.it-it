---
title: Gestione di riunioni e conferenze di Lync Online
TOCTitle: Gestione di riunioni e conferenze di Lync Online
ms:assetid: a4d0c070-4df2-47df-a1e2-6ce62600a287
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362833(v=OCS.15)
ms:contentKeyID: 56269946
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestione di riunioni e conferenze di Lync Online

 

_**Ultima modifica dell'argomento:** 2015-06-22_

I cmdlet seguenti possono essere usati per gestire le impostazioni relative alle riunioni e alle conferenze:


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
<td><p><a href="disable-csmeetingroom.md">Disable-CsMeetingRoom</a><br />
<a href="enable-csmeetingroom.md">Enable-CsMeetingRoom</a><br />
<a href="get-csmeetingroom.md">Get-CsMeetingRoom</a><br />
<a href="set-csmeetingroom.md">Set-CsMeetingRoom</a></p></td>
<td><p>Gestisce i dispositivi endpoint per le sale riunioni.</p>
<p>In Skype for Business online le sale riunioni sono accessori autonomi per computer che vengono installati nelle sale conferenze e offrono funzionalità avanzate per riunioni. Per gestire questi nuovi dispositivi endpoint è necessario, tra le altre cose, creare e abilitare un account di cassetta postale delle risorse di Exchange per il dispositivo e quindi abilitare lo stesso account per Skype for Business online.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-csaudioconferencingprovider.md">Get-CsAudioConferencingProvider</a></p></td>
<td><p>Restituisce informazioni sui provider di servizi di audioconferenza con cui l'organizzazione ha stipulato un contratto.</p>
<p>Un provider di servizi di audioconferenza è una società di terze parti che offre servizi di conferenza alle organizzazioni, inclusi servizi avanzati quali traduzione immediata, trascrizione e assistenza diretta di un operatore durante la conferenza.</p></td>
</tr>
<tr class="odd">
<td><p><a href="get-csmeetingconfiguration.md">Get-CsMeetingConfiguration</a><br />
<a href="set-csmeetingconfiguration.md">Set-CsMeetingConfiguration</a></p></td>
<td><p>Controlla il tipo di riunioni che gli utenti possono creare e stabilisce la modalità di partecipazione alle riunioni da parte di utenti anonimi e utenti che usano conferenze telefoniche con accesso esterno.</p>
<p>Le riunioni, o conferenze, sono parte integrante di Skype for Business online. Con questi cmdlet, ad esempio, è possibile configurare le riunioni in modo che gli utenti remoti non vengano ammessi automaticamente alla riunione ma vengano instradati alla sala d'attesa riunione. Questi utenti rimangono nella sala d'attesa finché un relatore non li ammette alla riunione.</p></td>
</tr>
</tbody>
</table>


È inoltre possibile gestire un piccolo sottoinsieme di proprietà di configurazione delle riunioni mediante l'interfaccia di amministrazione di Skype for Business online:

![Proprietà delle opzioni generali dell'Interfaccia di amministrazione di Lync](images/Dn362833.acf90793-7ee4-4faf-b791-f149dd5df2a5(OCS.15).png "Proprietà delle opzioni generali dell'Interfaccia di amministrazione di Lync")

## Vedere anche

#### Concetti

[Cmdlet di Lync Online](the-skype-for-business-online-cmdlets.md)  
[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

