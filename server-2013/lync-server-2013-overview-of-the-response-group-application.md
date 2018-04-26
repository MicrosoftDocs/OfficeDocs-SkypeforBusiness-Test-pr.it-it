---
title: "Lync Server 2013: Panoramica dell'applicazione Response Group"
TOCTitle: Panoramica dell'applicazione Response Group
ms:assetid: 6cc333e7-4029-4372-86b2-016040c415fb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398513(v=OCS.15)
ms:contentKeyID: 49300894
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Panoramica dell'applicazione Response Group in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Quando un chiamante chiama un Response Group, viene eseguito il routing della chiamata a un agente in base a un gruppo di risposta o alle risposte del chiamante alle domande di un sistema IVR (Interactive Voice Response). L'applicazione applicazione Response Group utilizza metodi di routing standard per eseguire il routing della chiamata al successivo agente disponibile. I metodi di routing delle chiamate includono routing seriale, verso l'agente inattivo più a lungo, round robin e il nuovo routing operatore, in cui vengono chiamati tutti gli agenti contemporaneamente per ogni chiamata in arrivo, indipendentemente dalla loro effettiva presenza. Se non è disponibile alcun agente, la chiamata viene mantenuta in una coda fino a quando non è disponibile un agente. Mentre la chiamata è nella coda, il chiamante ascolta un brano musicale fino a quando un agente disponibile non accetta la chiamata. Se la coda è piena o si verifica il timeout della chiamata mentre questa è in coda, il chiamante potrebbe ascoltare un messaggio e quindi venire disconnesso o trasferito a una destinazione diversa. Quando un agente accetta la chiamata, il chiamante può o meno visualizzare l'identità dell'agente, a seconda del modo in cui l'amministratore ha configurato Response Group. Gli agenti possono essere agenti formali, ovvero devono accedere al gruppo prima di poter accettare le chiamate di cui viene eseguito il routing al gruppo, oppure agenti informali, ovvero non accedono al gruppo né si disconnettono per accettare le chiamate.


> [!NOTE]
> Solo gli utenti locali possono essere agenti. Se un agente passa da locale a online, le chiamate del Response Group non saranno più indirizzate a lui.




> [!NOTE]
> L'applicazione applicazione Response Group utilizza un servizio interno, denominato servizio di ricerca corrispondenze, per accodare le chiamate e trovare agenti disponibili. Ogni computer che esegue l'applicazione applicazione Response Group esegue il servizio di ricerca corrispondenze, ma è attivo un solo servizio di ricerca corrispondenze per pool di Lync Server per volta, mentre gli altri sono passivi. Se il servizio di ricerca corrispondenze diventa non disponibile durante un guasto non pianificato, viene attivato uno dei servizi di ricerca corrispondenze passivi. L'applicazione applicazione Response Group garantisce quanto più possibile la continuazione senza interruzioni del routing e dell'accodamento delle chiamate. Quando si verifica una transizione a un servizio di ricerca corrispondenze, tutte le chiamate in trasferimento durante la transizione vengono perdute. Se, ad esempio, la transizione è dovuta all'inattività del Front End Server , vengono perdute tutte le chiamate attualmente gestite dal servizio di ricerca corrispondenze attivo nel Front End Server.



In Lync Server 2013 sono disponibili due ruoli di gestione per i Response Group: Gestore del Response Group e Amministratore del Response Group. Gli Amministratori del Response Group possono gestire tutti gli aspetti di qualunque Response Group. I Gestori del Response Group possono gestire soltanto determinati aspetti, e solo in relazione ai Response Group che possiedono. Il nuovo ruolo di Gestore aiuta a ridurre i costi di amministrazione, poiché consente di delegare responsabilità limitate in relazione a Response Group specifici a qualunque utente abilitato per VoIP aziendale.

Per adattare il nuovo ruolo di Gestore, Lync Server 2013applicazione Response Group include un **Tipo di workflow** Gestito o Non gestito. Nella tabella riportata di seguito vengono descritti i Response Group gestiti e non gestiti.

### Response Group gestiti e non gestiti

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo di Response Group</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Non gestito</p></td>
<td><ul>
<li><p>Ai Response Group non gestiti non è assegnato alcun Gestore. Questi Response Group possono essere configurati soltanto dagli Amministratori di Response Group.</p></li>
<li><p>Response group multipli non gestiti possono condividere una coda o gruppo di agenti.</p></li>
<li><p>Quando si migrano Response Group da una versione precedente a Lync Server 2013, il tipo impostato è Non gestito.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Gestito</p></td>
<td><ul>
<li><p>Gli amministratori del Response Group possono configurare tutti gli aspetti dei Response group gestiti.</p></li>
<li><p>I manager del Response Group non possono visualizzare o modificare Response group non espressamente assegnati a loro.</p></li>
<li><p>I manager del Response Group possono configurare solo alcuni aspetti dei Response group espressamente assegnati a loro.</p></li>
<li><p>I Response group gestiti non possono condividere code o gruppi di agenti con altri Response group gestiti o non gestiti.</p></li>
</ul></td>
</tr>
</tbody>
</table>


Nella seguente tabella sono illustrate le azioni che i manager del Response Group possono o non possono eseguire sui Response group a loro assegnati.

### Capacità del manager del Response group

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Possono configurare:</th>
<th>Possono creare, eliminare o configurare:</th>
<th>Non possono:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Agenti</p></li>
<li><p>Messaggio di benvenuto</p></li>
<li><p>Nome del Response Group</p></li>
<li><p>Descrizione</p></li>
<li><p>Numero visualizzato</p></li>
<li><p>Ore lavorative</p></li>
<li><p>Musica di attesa</p></li>
<li><p>Stato (attivo/inattivo)</p></li>
<li><p>Workflow del gruppo di risposta o Interactive voice response (IVR)</p></li>
</ul></td>
<td><ul>
<li><p>Gestione di gruppi di agenti</p></li>
<li><p>Code</p></li>
<li><p>Insiemi di festività</p></li>
</ul></td>
<td><ul>
<li><p>Creare o eliminare qualsiasi tipo di workflow</p></li>
<li><p>Modificare le impostazioni fondamentali dei Response Group, quali: <strong>URI SIP</strong> , <strong>Numero di telefono</strong> o <strong>Tipo di workflow</strong> .</p></li>
</ul></td>
</tr>
</tbody>
</table>


I manager del Response Group possono utilizzare i seguenti strumenti per la gestione dei Response Group a loro assegnati.

  - Pannello di controllo di Lync Server
    

    > [!NOTE]
    > Attraverso questi strumenti, i manager del Response Group possono soltanto gestire le impostazioni del Response Group. Per i manager non sono disponibili altre impostazioni di Lync Server.



  - Strumento di configurazione di Response Group

  - Lync Server Management Shell

Response Group ha la scalabilità appropriata per ambienti di reparto o gruppo di lavoro (per informazioni dettagliate, vedere [Pianificazione della capacità per Response Group in Lync Server 2013](lync-server-2013-capacity-planning-for-response-group.md)) e può essere distribuito in installazioni telefoniche interamente nuove. Questa applicazione supporta le chiamate in arrivo dalla distribuzione di VoIP aziendale e dalla rete telefonica locale. Gli agenti possono utilizzare Lync 2013, Lync 2010, Lync 2010 Attendant o Lync Phone Edition per rispondere alle chiamate di cui viene eseguito il routing.

L'applicazione applicazione Response Group è un componente di VoIP aziendale. Quando si distribuisce VoIP aziendale, l'applicazione applicazione Response Group viene installata e attivata automaticamente.

