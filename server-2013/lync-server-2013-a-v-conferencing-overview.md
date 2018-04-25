---
title: Panoramica di A/V Conferencing
TOCTitle: Panoramica di A/V Conferencing
ms:assetid: 9583de87-4618-4a99-a47a-45e8cc4cc221
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ619186(v=OCS.15)
ms:contentKeyID: 49301380
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Panoramica di A/V Conferencing

 

_**Ultima modifica dell'argomento:** 2012-10-13_

A/V Conferencing rende possibili le comunicazioni audio e video in tempo reale tra gli utenti. Quando si distribuiscono i servizi per conferenze, è possibile scegliere di abilitare e usare sia Web Conferencing sia A/V Conferencing oppure solo Web Conferencing.

Per la pianificazione di A/V Conferencing è necessario conoscere i requisiti di larghezza di banda di rete dei vari tipi di supporti per le conferenze richiesti dall'organizzazione. Ciò include audio, video e video panoramico.

Prima di abilitare gli utenti per A/V Conferencing, accertarsi che la rete sia in grado di gestire il carico risultante. Senza una larghezza di banda di rete sufficiente, l'esperienza degli utenti potrebbe risultare piuttosto insoddisfacente. È possibile usare il controllo di ammissione di chiamata per gestire la larghezza di banda della rete usata da A/V Conferencing. Questo aspetto è importante per le reti con restrizioni, ad esempio collegamenti con larghezza di banda limitata tra siti centrali e succursali. Per informazioni dettagliate, vedere [Panoramica del controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-overview-of-call-admission-control.md). Per informazioni dettagliate sui requisiti di larghezza di banda per i contenuti multimediali, vedere [Requisiti di larghezza di banda di rete per il traffico multimediale in Lync Server 2013](lync-server-2013-network-bandwidth-requirements-for-media-traffic.md).

Se si distribuiscono funzionalità di audioconferenza nella rete, gli utenti dovranno utilizzare dispositivi audio come gli auricolari per partecipare. Se si distribuiscono servizi per videoconferenze, è necessario distribuire dispositivi video quali webcam per gli utenti. È consigliabile usare dispositivi per le comunicazioni unificate certificati da Microsoft per tutti i tipi di dispositivi in modo da assicurare un'esperienza utente ottimale. Per dettagli sui dispositivi certificati per le comunicazioni unificate, vedere l'articolo sui telefoni e i dispositivi per Lync all'indirizzo [http://go.microsoft.com/fwlink/?linkid=263861\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=263861%26clcid=0x410). Per i dispositivi audio o video, la distribuzione e la formazione degli utenti sono passaggi importanti da considerare e pianificare.

Nelle sezioni seguenti vengono descritte le funzionalità per le conferenze audio e video, incluse le informazioni sulla gestione della larghezza di banda e la selezione dei client appropriati.

## Funzionalità di audioconferenza

Lync Server 2013 offre diverse funzionalità utilizzabili per configurare l'esperienza di audioconferenza per l'utente, incluse quelle seguenti:

  - **Disattivazione audio dei partecipanti**   Il relatore può usare questa impostazione per disattivare l'audio di tutti i partecipanti alla conferenza e mettere quest'ultima in uno stato in cui i non relatori non possono disattivare l'audio autonomamente.

  - **Annunci di ingresso/uscita in conferenza**   Se sono state abilitate le conferenze telefoniche con accesso esterno, i relatori possono usare questa impostazione per abilitare o disabilitare gli annunci di ingresso e uscita nelle conferenze in modo da ridurre al minimo le distrazioni mentre è in corso una conferenza.

  - **Aggiunta di un utente tramite chiamata in uscita**   I relatori e i partecipanti a cui è stata concessa l'autorizzazione possono aggiungere numeri di rete PSTN alle conferenze ed effettuare chiamate in uscita a tali numeri.

## Funzionalità di videoconferenza

Lync Server 2013 offre diverse funzionalità che è possibile usare per configurare l'esperienza di videoconferenza per l'utente, incluse le seguenti:

  - **Visualizzazione Raccolta**   Nelle videoconferenze con più di due utenti, questi possono vedere automaticamente tutti i partecipanti alla conferenza. Se la conferenza presenta più di cinque partecipanti, il video di quelli più attivi appare nella riga superiore mentre per gli altri vengono visualizzate solo le foto. Il video con più utenti è abilitato per impostazione predefinita. Per dettagli sulla configurazione o la disabilitazione del video a più utenti, vedere [Configurazione della larghezza di banda video in Lync Server 2013](lync-server-2013-configuring-video-bandwidth.md).

  - **Panoramica**   Se è installato un dispositivo per videoconferenze RoundTable, questa funzionalità offre una visione completa a 360 gradi della sala conferenza. La striscia panoramica è disponibile solo con dispositivi RoundTable.

  - **Modalità video solo relatore**   I relatori possono configurare la riunione in modo che venga mostrato solo il proprio video. Ciò evita distrazioni nelle riunioni di grandi dimensioni con più flussi video disponibili bloccando diverse origini. Questa modalità si applica anche ai video acquisiti e forniti dai dispositivi RoundTable.

  - **Video HD**   Gli utenti possono provare risoluzioni fino a 1080P HD in chiamate a due utenti e conferenze a più utenti.

  - **Video in evidenza**   I relatori possono configurare la riunione in modo il video di un partecipante selezionato che rappresenta un'origine video possa essere visto dagli altri partecipanti alla conferenza. Questa modalità si applica anche ai video acquisiti e forniti dai dispositivi RoundTable per il video panoramico.

