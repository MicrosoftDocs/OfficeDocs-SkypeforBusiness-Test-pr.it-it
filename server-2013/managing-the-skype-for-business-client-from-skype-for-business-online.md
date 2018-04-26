---
title: Gestione del client Lync
TOCTitle: Gestione del client Lync
ms:assetid: d1ccc7b6-99ff-4ffd-bd29-9088fb8fe837
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362847(v=OCS.15)
ms:contentKeyID: 56269980
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestione del client Lync

 

_**Ultima modifica dell'argomento:** 2015-06-22_

I cmdlet descritti di seguito consentono di gestire il client Lync:


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
<td><p><a href="get-csimfilterconfiguration.md">Get-CsImFilterConfiguration</a></p></td>
<td><p>Recupera informazioni relative alle restrizioni sugli URI in uso nell'organizzazione.</p>
<p>Quando inviano un messaggio istantaneo, gli utenti possono incorporare nel testo del messaggio un URI che rimanda a una determinata condivisione o sito Web gli altri partecipanti alla conversazione. È possibile configurare Skype for Business online in modo che i collegamenti ipertestuali con determinati prefissi vengano bloccati o non risultino attivi. Questo impedisce ai partecipanti di accedere al sito a cui fa riferimento l'URI facendo clic sul collegamento, costringendoli a copiare e incollare manualmente il collegamento in un browser.</p></td>
</tr>
<tr class="even">
<td><p><a href="get-cspresencepolicy.md">Get-CsPresencePolicy</a></p></td>
<td><p>Restituisce informazioni su due aspetti importanti delle sottoscrizioni relative alla presenza: richieste di sottoscrizione e sottoscrizioni di categoria.</p>
<p>Quando si viene aggiunti all'elenco contatti di un'altra persona, il comportamento predefinito prevede la ricezione di una notifica popup in cui si viene informati di essere stati aggiunti al suddetto elenco. Finché non viene chiusa la finestra popup visualizzata, ogni notifica viene considerata una richiesta di sottoscrizione</p>
<p>Le sottoscrizioni di categoria rappresentano una richiesta per una specifica categoria di informazioni, ad esempio un'applicazione che richiede dati del calendario.</p></td>
</tr>
<tr class="odd">
<td><p><a href="get-csprivacyconfiguration.md">Get-CsPrivacyConfiguration</a><br />
<a href="set-csprivacyconfiguration.md">Set-CsPrivacyConfiguration</a></p></td>
<td><p>Configura i valori di privacy predefiniti in Skype for Business online, lasciando però agli utenti la possibilità di modificarli.</p>
<p>Skype for Business online consente agli utenti di condividere con altre persone un'elevata quantità di informazioni sulla presenza, grazie alla possibilità di pubblicare foto personali, fornire informazioni dettagliate sulla posizione e rendere automaticamente disponibili le informazioni sulla presenza a chiunque nell'organizzazione e non solo alle persone presenti nell'elenco contatti personale. i cmdlet <strong>CsPrivacyConfiguration</strong> consentono agli amministratori di configurare i valori di privacy predefiniti in Skype for Business online, lasciando però agli utenti la possibilità di modificarli.</p></td>
</tr>
</tbody>
</table>


È inoltre possibile gestire un sottoinsieme di impostazioni di configurazione della privacy mediante l'interfaccia di amministrazione di Skype for Business online:

![Impostazioni della modalità privata della presenza dell'Interfaccia di amministrazione di Lync](images/Dn362847.eb206b74-844d-4a7b-b1b3-0cfcb6e3614b(OCS.15).png "Impostazioni della modalità privata della presenza dell'Interfaccia di amministrazione di Lync")

## Vedere anche

#### Concetti

[Cmdlet di Lync Online](the-skype-for-business-online-cmdlets.md)  
[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

