---
title: 'Lync Server 2013: Definizione dei requisiti per le conferenze'
TOCTitle: Definizione dei requisiti per le conferenze
ms:assetid: 5c83e268-22bf-42b2-bac3-3237b5e02e03
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204935(v=OCS.15)
ms:contentKeyID: 49300688
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definizione dei requisiti per le conferenze in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-30_

Per determinare le funzionalità di conferenza da distribuire, è necessario considerare le funzionalità che si desidera rendere disponibili agli utenti e le caratteristiche di larghezza di banda della rete. L'elenco di domande seguenti rappresenta una guida per il processo di pianificazione allo scopo di determinare le funzionalità di conferenza da distribuire, in base ai requisiti dell'organizzazione.

  - **Si desiderano abilitare le conferenze Web, che includono funzionalità di collaborazione sui documenti e condivisione di applicazioni?**
    
    In caso affermativo, è necessario abilitare le conferenze per il pool Front End in Microsoft Lync Server 2013, Strumento di pianificazione o in Generatore di topologie. L'abilitazione delle conferenze consente di abilitare sia le conferenze Web che le conferenze audio/video.
    
    Per la condivisione di applicazioni è richiesta e viene utilizzata più larghezza di banda di rete rispetto alla collaborazione sui documenti. In Lync Server 2013 è disponibile un meccanismo di limitazione per controllare ogni sessione di condivisione di applicazioni. Per impostazione predefinita, il limite è impostato su 1,5 Kb/secondo per ogni sessione.
    
    Se non si desidera abilitare la condivisione di applicazioni, ma si desidera utilizzare la collaborazione sui documenti, è possibile abilitare le conferenze e utilizzare i criteri relativi alle riunioni per disabilitare la condivisione di applicazioni. Per informazioni dettagliate sulla configurazione dei criteri per le riunioni, vedere [Criteri conferenza in Lync Server 2013](lync-server-2013-conferencing-policies.md).
    
    Per consentire agli utenti di condividere presentazioni di PowerPoint, è necessario configurare Server Office Web Apps. Per informazioni dettagliate sulla configurazione di Server Office Web Apps, vedere [Configurazione dell'integrazione con Office Web Apps Server e Lync Server 2013](lync-server-2013-enabling-office-web-apps-server-and-lync-server-2013.md).

  - **Si desidera abilitare le conferenze audio/video?**
    
    In caso affermativo, è necessario abilitare le conferenze per il pool Front End in Lync Server 2013, Strumento di pianificazione o in Generatore di topologie. L'abilitazione delle conferenze consente di abilitare sia le conferenze Web che le conferenze audio/video.
    
    Per le conferenze audio/video è richiesta e viene utilizzata maggiore larghezza di banda di rete rispetto alle conferenze Web (che includono le funzionalità di collaborazione sui documenti e condivisione di applicazioni). Se non si desidera abilitare le conferenze audio/video, ma si desidera abilitare le conferenze Web, è possibile abilitare le conferenze e utilizzare i criteri relativi alle riunioni per disabilitare le conferenze audio/video.
    
    Se si desidera abilitare le conferenze audio, ma non le conferenze video, è possibile abilitare le conferenze audio/video e utilizzare i criteri relativi alle riunioni per impedire le conferenze video. In alternativa, è possibile abilitare le conferenze audio/video e consentire solo a particolari utenti audio di avviare o partecipare a conferenze audio/video.
    

    > [!NOTE]
    > La funzionalità VoIP aziendale non è necessaria per le conferenze audio/video. Se si abilitano le conferenze audio/video, gli utenti possono aggiungere l'audio alle conferenze nel caso dispongano di dispositivi audio, anche se si utilizza una soluzione telefonica PBX.



  - **Si desidera consentire agli utenti di partecipare alla parte audio delle conferenze quando si utilizza un telefono PSTN?**
    
    In caso affermativo, distribuire e abilitare le conferenze telefoniche con accesso esterno. Gli utenti invitati, sia all'interno che all'esterno dell'organizzazione, potranno quindi partecipare alla parte audio delle conferenze tramite un telefono PSTN.

  - **Si desidera consentire agli utenti esterni con client Lync Server 2013 di partecipare ai tipi di conferenza abilitati?**
    
    In caso affermativo, è consigliabile distribuire server perimetrali. Consentire la partecipazione esterna alle riunioni ottimizza l'investimento in Lync Server 2013. Gli utenti con laptop con Lync Server 2013, ad esempio, potranno partecipare alle conferenze ovunque si trovino: a casa, in aeroporto o presso i clienti.
    
    Con la distribuzione di server perimetrali, inoltre, è possibile creare relazioni federate con altre organizzazioni, ad esempio clienti o fornitori, e gli utenti di tali organizzazioni possono collaborare più facilmente con gli utenti della propria organizzazione.
    
    Per informazioni dettagliate sulla distribuzione di server perimetrali, vedere [Pianificazione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-planning-for-external-user-access.md) e [Distribuzione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-deploying-external-user-access.md). Per informazioni dettagliate sull'abilitazione dell'accesso esterno per Server Office Web Apps, vedere [Pubblicazione di Office Web Apps Server in Lync Server 2013 tramite un server proxy inverso](lync-server-2013-publishing-office-web-apps-server-using-a-reverse-proxy-server.md).

  - **Si desidera stabilire quali client possono partecipare alle riunioni Lync Server 2013?**
    
    In caso affermativo, è consigliabile configurare la pagina di partecipazione alle riunioni in modo che siano disponibili solo le opzioni per i client che si desidera supportare. Ogni volta che un utente fa clic su un collegamento per partecipare a una riunione pianificata, Lync Server 2013 rileva se nel computer è già installato un client, quindi avvia il client predefinito e apre la pagina di partecipazione alle riunioni che contiene collegamenti per client alternativi. La pagina di partecipazione alle riunioni contiene sempre l'opzione per l'utilizzo di Microsoft Lync Web App. Oltre a questa opzione, è possibile decidere se includere collegamenti per Attendee e versioni precedenti di Communicator. Per informazioni dettagliate, vedere [Configurazione della pagina di partecipazione alle riunioni in Lync Server 2013](lync-server-2013-configuring-the-meeting-join-page.md).

## Argomenti della sezione

  - [Requisiti di Web Conferencing di Lync Server 2013](lync-server-2013-web-conferencing-requirements.md)

  - [Requisiti di A/V Conferencing di Lync Server 2013](lync-server-2013-a-v-conferencing-requirements.md)

  - [Requisiti delle conferenze telefoniche con accesso esterno in Lync Server 2013](lync-server-2013-dial-in-conferencing-requirements.md)

## Vedere anche

#### Ulteriori risorse

[Pianificazione dei servizi di conferenza in Lync Server 2013](lync-server-2013-planning-for-conferencing.md)  
[Elenco di controllo di distribuzione per le conferenze in Lync Server 2013](lync-server-2013-deployment-checklist-for-conferencing.md)

