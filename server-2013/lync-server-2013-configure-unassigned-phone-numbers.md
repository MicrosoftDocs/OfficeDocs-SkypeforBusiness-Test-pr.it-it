---
title: Configurare i numeri di telefono non assegnati
TOCTitle: Configurare i numeri di telefono non assegnati
ms:assetid: a0650659-dce7-455f-8977-02454bbfa400
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182559(v=OCS.15)
ms:contentKeyID: 49301496
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare i numeri di telefono non assegnati

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Lync Server consente di configurare il comportamento per le chiamate in arrivo verso numeri di telefono validi per l'organizzazione, ma non assegnati a un utente o a un telefono. Per configurare la gestione di tali chiamate, è possibile impostare una tabella dei numeri non assegnati. È possibile utilizzare la tabella per instradare le chiamate a un'applicazione Annuncio o a un server di Messaggistica unificata di Exchange.

La configurazione della tabella dei numeri non assegnati dipende dall'utilizzo previsto di questa. È possibile configurare la tabella con tutti gli interni validi dell'organizzazione, solo con gli interni non assegnati o con una combinazione di numeri di entrambi i tipi. La tabella dei numeri non assegnati può includere sia numeri assegnati che numeri non assegnati ma viene chiamata solo se un chiamante compone un numero non assegnato. Se nella tabella dei numeri non assegnati si inseriscono tutti gli interni validi, è possibile specificare l'azione da eseguire quando un utente lascia l'organizzazione, senza alcuna necessità di riconfigurare la tabella. Se nella tabella si inseriscono interni non assegnati, è possibile personalizzare l'azione da eseguire per numeri specifici. Se ad esempio si modifica l'interno del servizio di assistenza clienti, è possibile inserire il vecchio numero nella tabella e assegnarlo a un annuncio in cui viene indicato il nuovo numero.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Prima di configurare la tabella dei numeri non assegnati, è necessario che sia definito almeno un annuncio o che sia impostato un Operatore automatico Messaggistica unificata di Exchange. Per informazioni dettagliate sulla creazione di annunci, vedere <a href="lync-server-2013-create-an-announcement.md">Creare un annuncio in Lync Server 2013</a>. Per verificare se le impostazioni della Messaggistica unificata di Exchange sono state configurate, eseguire il cmdlet <strong>Get-CsExUmContact</strong>. Per informazioni dettagliate, <a href="get-csexumcontact.md">Get-CsExUmContact</a>.</td>
</tr>
</tbody>
</table>


## Argomenti della sezione

  - [Creare o modificare un intervallo di numeri non assegnati in Lync Server 2013](lync-server-2013-create-or-modify-an-unassigned-number-range.md)

  - [Eliminare un intervallo di numeri non assegnati](lync-server-2013-delete-an-unassigned-number-range.md)

