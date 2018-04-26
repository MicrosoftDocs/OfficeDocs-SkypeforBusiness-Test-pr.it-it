---
title: 'Lync Server 2013: Strumenti di amministrazione di Lync Server'
TOCTitle: Strumenti di amministrazione di Lync Server
ms:assetid: 9b006f93-4f3d-461d-89b8-e80a34fdb3c5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg195756(v=OCS.15)
ms:contentKeyID: 49301432
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Strumenti di amministrazione di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

In questo argomento vengono descritti gli strumenti di amministrazione per Lync Server 2013.

Gli strumenti di amministrazione vengono installati per impostazione predefinita in ogni server Lync Server. È inoltre possibile installarli in altri computer, ad esempio in console amministrative dedicate. Per le procedure di installazione degli strumenti di amministrazione, vedere [Installare gli strumenti di amministrazione di Lync Server 2013](lync-server-2013-install-lync-server-administrative-tools.md). Per le procedure di apertura degli strumenti per l'esecuzione di attività di gestione, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

Prima di installare o utilizzare gli strumenti di amministrazione di Lync Server, rivedere i requisiti relativi a infrastruttura, sistema operativo, software e diritti di amministratore. Per informazioni dettagliate sui requisiti di infrastruttura, vedere [Requisiti dell'infrastruttura degli Strumenti di amministrazione in Lync Server 2013](lync-server-2013-administrative-tools-infrastructure-requirements.md). Per informazioni dettagliate sui requisiti relativi a software e sistema operativo per l'installazione degli strumenti di amministrazione di Lync Server, vedere [Supporto del sistema operativo per server e strumenti in Lync Server 2013](lync-server-2013-server-and-tools-operating-system-support.md), [Requisiti software aggiuntivi per Lync Server 2013](lync-server-2013-additional-software-requirements.md) e [Requisiti e supporto per i server aggiuntivi in Lync Server 2013](lync-server-2013-additional-server-support-and-requirements.md). Le autorizzazioni e i diritti utente necessari per installare e utilizzare questi strumenti sono descritti in [Autorizzazioni e diritti di amministratore necessari per l'installazione e l'amministrazione di Lync Server 2013](lync-server-2013-administrator-rights-and-permissions-required-for-setup-and-administration.md).

Gli strumenti di amministrazione includono:

  - **Distribuzione guidata di Lync Server**   Consente di distribuire Lync Server e installare tutti gli strumenti di amministrazione.

  - **Lync ServerGeneratore di topologie**   Consente di definire i componenti della distribuzione.

  - **Pannello di controllo di Lync Server**   Consente la gestione continuativa della distribuzione mediante un'interfaccia Web.

  - **Lync Server Management Shell**   Consente la gestione continuativa della distribuzione mediante la riga di comando.

  - **Lync Server Strumento di registrazione**   Consente di risolvere i problemi della distribuzione.

  - **servizio di registrazione centralizzato**   Consente di raccogliere i file di log e di traccia da un computer, un pool, un sito o globalmente. È possibile selezionare e definire scenari contenenti provider, contrassegni e livelli di traccia. I dati di registrazione possono essere raccolti, aggregati e visualizzati con strumenti come Snooper.exe o qualsiasi strumento basato su testo.

È possibile gestire la distribuzione principalmente utilizzando il Generatore di topologie e il Pannello di controllo di Lync Server.

## Distribuzione guidata

È necessario utilizzare lo Distribuzione guidata di Lync Server, incluso nel supporto di installazione, per installare tutti gli strumenti di amministrazione in un computer in cui non è già installato Lync Server. Nel corso della procedura di installazione degli strumenti di amministrazione, la Distribuzione guidata di Lync Server viene installata localmente insieme agli altri strumenti, in modo che in seguito sia possibile installare i file per i componenti aggiuntivi o rimuovere i file per i componenti non necessari.

Per informazioni dettagliate su come eseguire per la prima volta la Distribuzione guidata di Lync Server dai supporti di installazione di Lync Server, vedere [Installare gli strumenti di amministrazione di Lync Server 2013](lync-server-2013-install-lync-server-administrative-tools.md).

## Generatore di topologie

Per informazioni dettagliate sulle attività di distribuzione che è possibile eseguire utilizzando il Generatore di topologie, vedere la documentazione relativa alla distribuzione per ogni ruolo server.

## Pannello di controllo di Lync Server

È possibile usare il Pannello di controllo di Lync Server 2013 per eseguire la maggior parte delle attività amministrative richieste per gestire Lync Server 2013. Pannello di controllo di Lync Server offre un'interfaccia utente grafica per gestire la configurazione dei server che eseguono Lync Server, oltre agli utenti, i client e i dispositivi nell'organizzazione. Lync Server Management Shell usa Pannello di controllo di Lync Server come meccanismo sottostante per eseguire la configurazione di Lync Server.

Il Pannello di controllo di Lync Server viene installato automaticamente su ogni Front End Server o server Standard Edition di Lync Server. In questa versione, i server perimetrali vengono amministrati in remoto. È inoltre possibile installare il Pannello di controllo di Lync Server su un altro computer, ad esempio una console di gestione da cui gestire in modo centralizzato Lync Server. Per informazioni dettagliate, vedere [Installare gli strumenti di amministrazione di Lync Server 2013](lync-server-2013-install-lync-server-administrative-tools.md).

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Per configurare le impostazioni mediante il Pannello di controllo di Lync Server, è necessario accedere con un account appartenente al ruolo CsAdministrator. Per informazioni dettagliate sui ruoli amministrativi predefiniti disponibili in Lync Server 2013, vedere <a href="lync-server-2013-planning-for-role-based-access-control.md">Pianificazione del controllo di accesso basato sui ruoli in Lync Server 2013</a>.</p></li>
<li><p>Per configurare le impostazioni mediante il Pannello di controllo di Lync Server, è anche necessario usare un computer con una risoluzione dello schermo minima pari a 1024x768.</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Lync Server Management Shell

In Lync Server, Lync Server Management Shell rappresenta un nuovo metodo di amministrazione e gestione. Lync Server Management Shell è una potente interfaccia di gestione basata sulla tecnologia interfaccia della riga di comando Windows PowerShell, che contiene un set completo di cmdlet specifici di Lync Server. Grazie a Lync Server Management Shell è possibile controllare in modo semplice la configurazione del sistema e l'automazione. Il Generatore di topologie e il Pannello di controllo di Lync Server implementano subset di tali cmdlet per il supporto della gestione di Lync Server. Lync Server Management Shell include cmdlet per tutte le attività di amministrazione di Lync Server ed è possibile utilizzare i cmdlet singolarmente per gestire la distribuzione. Per informazioni dettagliate, vedere la documentazione di [Lync Server Management Shell](lync-server-2013-lync-server-management-shell.md) o la guida relativa alla riga di comando per ogni cmdlet.

## Strumento di registrazione

Lo strumento di registrazione di Lync Server facilita la risoluzione dei problemi consentendo di acquisire informazioni di registrazione e traccia dal prodotto mentre è in esecuzione. È possibile utilizzarlo per eseguire sessioni di debug in qualsiasi ruolo server di Lync Server. Per informazioni dettagliate sullo strumento di registrazione, vedere la relativa documentazione nella libreria TechNet all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=199265](http://go.microsoft.com/fwlink/p/?linkid=199265).

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Il servizio di registrazione centralizzato è la soluzione consigliata per tutte le raccolte di dati di registrazione rispetto allo strumento di registrazione di Lync Server in tutti i casi. Lo strumento di registrazione di Lync Server funzionerà comunque, ma interferirà o risulterà in gran parte inutile se il servizio di registrazione centralizzato è già in esecuzione. È necessario utilizzare solo il servizio di registrazione centralizzato o lo strumento di registrazione di Lync Server, ma mai entrambi gli strumenti in contemporanea. Per ulteriori informazioni sul servizio di registrazione centralizzato e sui motivi per cui deve essere utilizzato in modo esclusivo, vedere <a href="lync-server-2013-using-the-centralized-logging-service.md">Utilizzo del servizio di registrazione centralizzato</a>.</td>
</tr>
</tbody>
</table>


## Contenuto della sezione

  - [Requisiti dell'infrastruttura degli Strumenti di amministrazione in Lync Server 2013](lync-server-2013-administrative-tools-infrastructure-requirements.md)

  - [Supporto del sistema operativo per server e strumenti in Lync Server 2013](lync-server-2013-server-and-tools-operating-system-support.md)

  - [Requisiti software degli strumenti di amministrazione in Lync Server 2013](lync-server-2013-administrative-tools-software-requirements.md)

  - [Autorizzazioni e diritti di amministratore necessari per l'installazione e l'amministrazione di Lync Server 2013](lync-server-2013-administrator-rights-and-permissions-required-for-setup-and-administration.md)

  - [Requisiti per la pubblicazione di una topologia Lync Server 2013](lync-server-2013-requirements-to-publish-a-topology.md)

  - [Installare gli strumenti di amministrazione di Lync Server 2013](lync-server-2013-install-lync-server-administrative-tools.md)

  - [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md)

  - [Risoluzione dei problemi relativi al Pannello di controllo di Lync Server 2013](lync-server-2013-troubleshooting-lync-server-2013-control-panel.md)

  - [Utilizzo del servizio di registrazione centralizzato](lync-server-2013-using-the-centralized-logging-service.md)

## Vedere anche

#### Ulteriori risorse

[Lync Server Management Shell](lync-server-2013-lync-server-management-shell.md)

