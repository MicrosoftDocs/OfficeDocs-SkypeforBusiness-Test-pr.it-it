---
title: 'Lync Server 2013: Pianificazione dei servizi di conferenza'
TOCTitle: Pianificazione dei servizi di conferenza
ms:assetid: 983a272a-e1b3-4d70-8f84-836b092fe526
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398781(v=OCS.15)
ms:contentKeyID: 49301403
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione dei servizi di conferenza in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-01-29_

In Lync Server 2013 è disponibile un'ampia gamma di funzionalità per conferenze:

  - Web Conferencing, che include collaborazione su documenti, condivisione di applicazioni e condivisione del desktop. Lync Server 2013 usa Office Web Apps e Server Office Web Apps per gestire la condivisione e il rendering di presentazioni di PowerPoint. Per informazioni dettagliate sull'installazione e la configurazione di Server Office Web Apps, vedere [Configurazione dell'integrazione con Office Web Apps Server e Lync Server 2013](lync-server-2013-enabling-office-web-apps-server-and-lync-server-2013.md).

  - A/V Conferencing, che consente agli utenti di partecipare a conferenze audio o video in tempo reale senza dover utilizzare servizi esterni, come il servizio Microsoft Live Meeting o un ponte audio di terze parti

  - Conferenza telefonica con accesso esterno (PSTN), che consente agli utenti di partecipare alla parte audio di una conferenza di Lync Server 2013 tramite un telefono PSTN senza dover utilizzare un provider di servizi di audioconferenza di terze parti.

  - IM Conferencing, per conferenza in cui più di due utenti comunicano in una singola sessione di messaggistica istantanea. Per informazioni dettagliate su IM Conferencing, vedere [Pianificazione di Front End Server, messaggistica istantanea e presenza in Lync Server 2013](lync-server-2013-planning-for-front-end-servers-instant-messaging-and-presence.md).

Lync Server 2013 supporta sia le conferenze sia pianificate che quelle estemporanee.

Quando si distribuisce Lync Server 2013,  Front End Server, è possibile scegliere se distribuire anche le funzionalità di Web Conferencing, A/V Conferencing e Conferenza telefonica con accesso esterno. Le funzionalità di IM Conferencing vengono sempre distribuite automaticamente con le funzionalità di conversazione istantanea nei Lync Server 2013  Front End Server.


> [!NOTE]
> Se la distribuzione include riunioni organizzate tramite client Office Communicator 2007 R2 (inclusa la console Live Meeting o il Componente aggiuntivo per conferenze per Microsoft Office Outlook), per le riunioni esisteranno le limitazioni seguenti dopo la migrazione a Lync Server 2013: 
> <UL>
> <LI>
> <P>Gli utenti nella riunione non potranno utilizzare le funzionalità per la collaborazione dati, incluse la collaborazione a documenti, la condivisione di applicazioni e la condivisione del desktop.</P>
> <LI>
> <P>Potrebbero verificarsi problemi di stabilità dato che i client Office Communicator 2007 R2 non sono supportati con Lync Server 2013.</P></LI></UL>Per evitare questi problemi, ripianificare qualsiasi riunione organizzata con client Office Communicator 2007 R2 con Outlook 2010 o Outlook 2013 tramite il Componente aggiuntivo per riunioni online per Lync 2010 o il componente aggiuntivo per riunioni online per Lync 2013.



Nelle sezioni che seguono vengono illustrati gli elementi necessari alla distribuzione dei vari tipi di funzionalità per conferenze, compresi il processo di pianificazione, i componenti, i requisiti hardware e software e il processo di distribuzione.

## Argomenti della sezione

  - [Panoramica delle conferenze in Lync Server 2013](lync-server-2013-overview-of-conferencing.md)

  - [Definizione dei requisiti per le conferenze in Lync Server 2013](lync-server-2013-defining-your-requirements-for-conferencing.md)

  - [Componenti e topologie per le conferenze in Lync Server 2013](lync-server-2013-components-and-topologies-for-conferencing.md)

  - [Requisiti tecnici per le conferenze in Lync Server 2013](lync-server-2013-technical-requirements-for-conferencing.md)

  - [Elenco di controllo di distribuzione per le conferenze in Lync Server 2013](lync-server-2013-deployment-checklist-for-conferencing.md)

  - [Supporto per le riunioni di grandi dimensioni in Lync Server 2013](lync-server-2013-support-for-large-meetings.md)

