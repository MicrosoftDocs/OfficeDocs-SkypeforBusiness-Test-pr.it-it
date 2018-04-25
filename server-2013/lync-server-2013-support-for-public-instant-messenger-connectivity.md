---
title: Supporto della connettività per messaggistica istantanea pubblica in Lync Server 2013
TOCTitle: Supporto della connettività per messaggistica istantanea pubblica in Lync Server 2013
ms:assetid: 9c6eb500-647b-4ccd-a00e-2b8dd7c44a76
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn458579(v=OCS.15)
ms:contentKeyID: 59602743
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Supporto della connettività per messaggistica istantanea pubblica in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

## Supporto della connettività per messaggistica istantanea pubblica

Questo articolo fornisce informazioni sul supporto di Public IM Connectivity (PIC), una funzionalità di Microsoft Lync grazie alla quale le organizzazioni possono consentire ai propri utenti di Lync di connettersi con utenti di determinati servizi di messaggistica istantanea pubblica tramite i relativi client e identità Lync.

Questa funzionalità offre agli utenti finali il vantaggio di potersi connettere con clienti, partner e fornitori in base alle proprie esigenze e all'IT il vantaggio di supportare un unico client di comunicazione in tempo reale mantenendo le funzionalità di controllo, conformità e archiviazione offerte da Lync. La connettività Lync-Skype, [disponibile al pubblico a partire da maggio 2013](http://blogs.technet.com/b/lync/archive/2013/05/23/lync-skype-connectivity-available-today.aspx), si basa sui principi stabiliti da Lync, Office Communications Server (OCS) e Live Communications Server (LCS) con PIC per la connessione a MSN/Windows Live, AOL e Yahoo. Per maggiori informazioni, vedere la pagina relativa alla [connettività Lync-Skype](http://office.microsoft.com/it-it/lync/lync-skype-connectivity-fx103789635.aspx). La federazione con Windows Live, AOL e Yahoo sta per terminare. In questa pagina è documentato lo stato di ogni servizio.

Per usare PIC, gli utenti devono attivare il servizio per ogni provider di servizi di messaggistica istantanea pubblica. I requisiti e i dettagli dell'attivazione dipendono dal provider e dal programma di licenza dell'utente.

## Windows Live Messenger

Microsoft ha unito Windows Live Messenger e Skype. In aprile 2013 gli utenti di Messenger sono stati migrati a Skype al momento dell'accesso. Gli utenti di Lync per cui la federazione con Messenger è importante saranno ancora in grado di comunicare con i contatti di Messenger, anche dopo il passaggio di questi contatti a Skype. Gli amministratori o gli utenti finali di Lync non devono fare niente per mantenere la continuità del servizio e questa funzionalità può essere gestita in Lync allo stesso modo con cui si gestivano le comunicazioni con Messenger. 

Quando gli utenti di Messenger accedono a Skype con i propri account Microsoft (le stesse credenziali usate per Messenger), tutti i contatti di Messenger, inclusi i contatti federati di Lync, li seguono in Skype. Per questi contatti sono disponibili la condivisione delle informazioni sulla presenza e la messaggistica istantanea. 

Per tutti gli utenti di Lync sono ora disponibili anche le funzionalità di connettività Lync-Skype, aggiunta di contatti, condivisione delle informazioni sulla presenza, messaggistica istantanea e chiamate audio fra utenti di Lync e Skype.

## Yahoo\! e AOL Instant Messenger

La federazione con Yahoo\! e AOL sta per essere terminata per gli utenti di Lync (e di Office Communications Server). La capacità di Microsoft di fornire questi servizi è sempre stata subordinata al supporto offerto da Yahoo\! e AOL, che sono entrambi in fase di risoluzione del contratto. Sia per Yahoo\! che per AOL il servizio continuerà fino a giugno 2014.

  - **Yahoo** - Il servizio continuerà fino a giugno 2014 e gli utenti dovranno sempre disporre di una licenza di sottoscrizione utenti per Microsoft Lync Public IM Connectivity (“PIC USL”). Dal 1 settembre 2012 questa licenza non è più disponibile per l'acquisto per i nuovi contratti o quelli in fase di rinnovo. Gli utenti con licenze acquistate prima di questa data potranno continuare a usufruire della federazione con Yahoo\! fino alla data di chiusura del servizio o alla scadenza del contratto di licenza. Leggere l'[annuncio](http://blogs.technet.com/b/lync/archive/2012/11/26/lync-and-yahoo-federation-end-of-life.aspx) sul blog del team di Lync. Gli utenti con contratti di licenza PIC che si estendono oltre il 30 giugno 2014 riceveranno un credito proporzionato all'importo dei pagamenti relativi al periodo di tempo successivo al 30 giugno 2014.

  - **AOL** - A partire dal 30 giugno 2014, il servizio di connettività per messaggistica istantanea pubblica ("PIC") di Lync non sarà più disponibile. Per limitare i disagi causati del termine del servizio, Microsoft ha interrotto il provisioning di domini utente aggiuntivi. Fino al 30 giugno 2014 gli utenti possono continuare a supportare le comunicazioni federate con AIM senza variazioni. Oltre quella data (o per gli utenti che hanno bisogno di eseguire il provisioning di domini aggiuntivi nel frattempo), sarà disponibile un servizio sostitutivo direttamente da AOL. Per altre informazioni sul nuovo servizio di AOL, vedere l'articolo che spiega come [stabilire una federazione diretta con AIM](http://aimenterprise.aol.com/pic.php)  (apre una nuova pagina su AOL.com).  

## Riepilogo dei provider di servizi di messaggistica istantanea pubblica

La tabella seguente fornisce un riepilogo dei provider di servizi di messaggistica istantanea pubblica, delle capacità di federazione con Lync e dei requisiti di licenza.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Provider di servizi di messaggistica istantanea pubblica</th>
<th>Capacità di federazione</th>
<th>Requisiti di licenza</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Skype</p></td>
<td><p>Messaggistica istantanea, presenza, audio</p></td>
<td><p>Licenze CAL per Lync Server, Lync Online Piano 1/2/3</p></td>
</tr>
<tr class="even">
<td><p>Windows Live Messenger</p></td>
<td><p>Messaggistica istantanea, presenza, audio/video</p></td>
<td><p>Licenze CAL per Lync Server (supportate finché Windows Live Messenger è sul mercato)</p></td>
</tr>
<tr class="odd">
<td><p>AOL</p></td>
<td><p>Messaggistica istantanea, presenza</p></td>
<td><p>Licenze CAL per Lync Server (supportate fino a giugno 2014 per gli utenti esistenti)</p></td>
</tr>
<tr class="even">
<td><p>Yahoo!</p></td>
<td><p>Messaggistica istantanea, presenza</p></td>
<td><p>Richiede licenze di sottoscrizione utenti per la connettività di messaggistica istantanea pubblica di Microsoft Lync (“PIC USL”) in aggiunta alle licenze CAL per Lync Server. In base al listino prezzi di settembre 2012, la licenza PIC USL non è più disponibile per l'acquisto. Gli utenti con licenze attive potranno continuare a usufruire della federazione con Yahoo! Messenger fino alla data di chiusura del servizio, il 30 giugno 2014.</p></td>
</tr>
</tbody>
</table>

