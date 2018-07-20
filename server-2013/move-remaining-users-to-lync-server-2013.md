---
title: Spostare gli utenti rimanenti in Lync Server 2013
TOCTitle: Spostare gli utenti rimanenti in Lync Server 2013
ms:assetid: 72025e1b-97d1-40e9-8a98-28c018942b48
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688090(v=OCS.15)
ms:contentKeyID: 49887604
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Spostare gli utenti rimanenti in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-29_

È possibile spostare gli utenti nella nuova distribuzione di Lync Server 2013 mediante il Pannello di controllo di Lync Server o Lync Server Management Shell. Per garantire una transizione senza problemi in Lync Server 2013, devono essere soddisfatti alcuni requisiti. Per informazioni dettagliate sui prerequisiti per eseguire le procedure descritte in questo argomento, vedere [Configurare i client per la migrazione](configure-clients-for-migration.md). informazioni dettagliate sullo spostamento degli utenti, vedere [Fase 4: spostare gli utenti di prova nel pool pilota](phase-4-move-test-users-to-the-pilot-pool.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Non è possibile utilizzare lo snap-in Utenti e computer di Active Directory o gli strumenti di amministrazione di Lync Server 2010 per spostare gli utenti dall'ambiente legacy a Lync Server 2013.</td>
</tr>
</tbody>
</table>


Quando si sposta un utente in un pool di Lync Server 2013, i dati dell'utente vengono spostati nel database back-end associato al nuovo pool.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>In questi dati sono incluse le riunioni attive create dall'utente legacy. Se ad esempio un utente legacy ha configurato una conferenza <strong>riunione personale</strong> , tale conferenza sarà ancora disponibile nel nuovo pool di Lync Server 2013 dopo lo spostamento dell'utente. I dettagli per accedere alla riunione saranno lo stesso   URL e lo stesso ID conferenza. L'unica differenza è costituita dal fatto che la conferenza ora è ospitata nel pool di Lync Server 2013 e non nel pool di Lync Server 2010.</td>
</tr>
</tbody>
</table>



> [!NOTE]
> Lo spostamento degli utenti in Lync Server 2013 non rende necessario eseguire allo stesso tempo la distribuzione dei client aggiornati. Le nuove funzionalità saranno disponibili per gli utenti solo quando eseguiranno l'aggiornamento al nuovo software client.



## Attività di post-migrazione

1.  Dopo aver spostato gli utenti, verificare i criteri di conferenza loro assegnati.

2.  Per garantire il funzionamento delle riunioni organizzate da utenti situati in Lync Server 2013 con utenti federati contenuti in Lync Server 2010, il criterio di conferenza assegnato agli utenti sottoposti a migrazione deve accettare i partecipanti anonimi.

3.  I criteri di conferenza che consentono i partecipanti anonimi hanno l'impostazione **Consenti ai partecipanti di invitare utenti anonimi** selezionata nel Pannello di controllo di Lync Server 2013 e l'impostazione **AllowAnonymousParticipantsInMeetings** configurata su **True** nell'output del cmdlet **Get-CsConferencingPolicy** in Lync Server Management Shell.

4.  Per informazioni dettagliate sulla configurazione dei criteri di conferenza tramite Lync Server Management Shell, vedere [Set-CsConferencingPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsConferencingPolicy) nella documentazione di Lync Server Management Shell.

