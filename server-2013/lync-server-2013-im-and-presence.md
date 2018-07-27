---
title: 'Lync Server 2013: Messaggistica istantanea e presenza'
TOCTitle: Messaggistica istantanea e presenza
ms:assetid: 6a93ae95-3b64-410b-ab72-74dea232f065
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg417162(v=OCS.15)
ms:contentKeyID: 49300864
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Messaggistica istantanea e presenza in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-10-07_

La messaggistica istantanea e la presenza vengono installate automaticamente in qualsiasi distribuzione di Lync Server.

Le informazioni sulla *presenza* consentono agli utenti di contattare i colleghi nel momento più appropriato con la corretta forma di comunicazione, per garantire un ambiente di lavoro più produttivo. La presenza di un utente è una raccolta di informazioni che includono la disponibilità, la disposizione a comunicare, note aggiuntive (come posizione e stato) e le modalità in cui può essere contattato un utente. È possibile migliorare le informazioni sulla presenza in Lync Server tramite immagini, informazioni sulla posizione e un ricco insieme di stati presenza, quali "Non al lavoro", "Non disturbare" e "Torno subito", oltre agli stati di base come "Disponibile", "Non disponibile" e "In conferenza". Gli amministratori possono inoltre definire stati presenza specifici dell'organizzazione e personalizzati.

Opzioni di gestione dei contatti e di accesso utente consentono agli utenti di controllare le informazioni visualizzate dagli altri. Gli utenti possono impostare livelli diversi di contatti, ciascuno dei quali può visualizzare livelli diversi di informazioni sulla presenza.

Semplicemente osservando un elenco di contatti, gli utenti possono trovare immediatamente tutte le informazioni necessarie. Icone colorate intuitive indicano lo stato di presenza di altri utenti. Vengono visualizzate anche un'immagine e la posizione.

Grazie all'integrazione tra Lync Server e altri prodotti, quali Outlook e SharePoint, ogni volta che viene visualizzato il nome di un contatto, ad esempio in un messaggio di posta elettronica o nel sito Web di un team, vengono visualizzati anche lo stato e le informazioni di contatto. Se si distribuisce Exchange 2013, Lync Server e Exchange 2013, inoltre, è possibile condividere un archivio contatti unificato accessibile dai client di tutti i prodotti.

Tramite la messaggistica istantanea in Lync Server gli utenti possono scambiarsi rapidamente messaggi con informazioni tempestive. Se lo si desidera, è possibile consentire agli utenti di comunicare con utenti di reti di messaggistica istantanea pubbliche come MSN/Windows Live, Yahoo\! e AOL. Si noti che potrebbe essere necessaria una licenza separata per la connettività di messaggistica istantanea pubblica con Windows Live, Yahoo\! e AOL. Lync Server è inoltre compatibile con XMPP (Extensible Messaging and Presence Protocol), in modo che gli utenti possano scambiare messaggi istantanei e informazioni sulla presenza con utenti di servizi XMPP come Google Talk.

> [!IMPORTANT]  
> <ul>
> <li><p>Dal 1 settembre 2012, la licenza di sottoscrizione utenti per la connettività di messaggistica istantanea pubblica di Microsoft Lync (“PIC USL”) non è più disponibile per l'acquisto per i nuovi contratti o quelli in fase di rinnovo. I clienti con licenze attive potranno continuare a eseguire la federazione con Yahoo! Messenger fino alla data di chiusura del servizio. Giugno 2014 è la data di fine servizio annunciata per Yahoo! e AOL. Per informazioni dettagliate, vedere <a href="lync-server-2013-support-for-public-instant-messenger-connectivity.md">Supporto della connettività per messaggistica istantanea pubblica in Lync Server 2013</a>.</p></li>
> 
> <li><p>La licenza PIC USL è una licenza di sottoscrizione di tipo mensile per utente, richiesta per la federazione di Lync Server o Office Communications Server con Yahoo! Messenger. La capacità di Microsoft di fornire questo servizio dipende dal supporto offerto da Yahoo! e il contratto sottostante è in fase di chiusura.</p></li>
> 
> 
> <li><p>Oggi più che mai, Lync è un potente strumento per la connessione tra diverse organizzazioni e con utenti di tutto il mondo. La federazione con Windows Live Messenger non richiede ulteriori licenze per utente/dispositivo in aggiunta alla licenza CAL Standard per Lync. La federazione con Skype verrà aggiunta a questo elenco, consentendo agli utenti di Lync di raggiungere centinaia di milioni di persone tramite messaggistica istantanea e comunicazioni vocali.</p></li></ul>


La cronologia conversazioni consente agli utenti di tenere traccia di vecchie conversazioni di messaggistica istantanea e di recuperare informazioni che potrebbero essere state comunicate di messaggistica istantanea anche diversi mesi prima.

La funzionalità Chat persistente consente di partecipare a conversazioni tra più partecipanti basate su argomenti e permanenti nel tempo. I messaggi inseriti nelle chat room (forum di discussione) possono essere permanenti, ovvero possono rimanere disponibili nel tempo, in modo da consentire la partecipazione di persone dislocate in sedi e reparti diversi, anche quando non sono tutte online contemporaneamente.

Se l'organizzazione è soggetta a regolamentazioni di conformità, è possibile distribuire una caratteristica di archiviazione dei messaggi che consente di archiviare il contenuto dei messaggi istantanei per tutti gli utenti dell'organizzazione o solo per alcuni utenti specificati. Se si include anche Exchange 2013 nella distribuzione, l'archivio della messaggistica istantanea può essere integrato con la funzionalità di archiviazione sul posto di Exchange, in modo da ottenere una singola esperienza di amministrazione per la conformità.

