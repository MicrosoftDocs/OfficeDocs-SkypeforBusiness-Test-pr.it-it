---
title: "Lync Server 2013: Configura criteri vocali, registri d'uso PSTN, route vocali"
TOCTitle: Configurazione di criteri vocali, record di utilizzo PSTN e route vocali
ms:assetid: 1e5a15f9-6f42-4dc6-baaa-24daf54afc4d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398272(v=OCS.15)
ms:contentKeyID: 49299874
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione di criteri vocali, record di utilizzo PSTN e route vocali in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-10_

I criteri vocali, i record di utilizzo PSTN e le route vocali sono strettamente correlati. È infatti possibile configurare i criteri vocali selezionando un insieme di funzionalità di chiamata e quindi assegnando al criterio un insieme di record di utilizzo PSTN, che specificano quali diritti sono autorizzati per gli utenti o i gruppi a cui viene assegnato il criterio. Anche alle route vocali vengono assegnati record di utilizzo PSTN, allo scopo di trovare una corrispondenza tra le route e gli utenti che sono autorizzati a utilizzarle. In altri termini, gli utenti possono effettuare esclusivamente chiamate che utilizzino le route per cui dispongono di un record di utilizzo PSTN corrispondente.

Il flusso di lavoro consigliato per una nuova distribuzione di VoIP aziendale consiste nel configurare innanzitutto un criterio vocale contenente i record di utilizzo PSTN appropriati e quindi nell'associare le route appropriate a ogni record di utilizzo PSTN.


> [!NOTE]
> È inoltre possibile creare criteri vocali con ambito <EM>utente</EM> e assegnarli a singoli utenti o gruppi.



Per i passaggi dettagliati per l'esecuzione di ognuna di queste attività, vedere le procedure descritte in questa sezione.

## Argomenti della sezione

  - [Configurazione di criteri vocali e record utilizzo PSTN per autorizzare privilegi e funzionalità di chiamata in Lync Server 2013](lync-server-2013-configuring-voice-policies-and-pstn-usage-records-to-authorize-calling-features-and-privileges.md)

  - [Visualizzare record utilizzo PSTN in Lync Server 2013](lync-server-2013-view-pstn-usage-records.md)

  - [Configurazione di route vocali per le chiamate in uscita in Lync Server 2013](lync-server-2013-configuring-voice-routes-for-outbound-calls.md)

  - [Esportazione e importazione della configurazione di route vocali in Lync Server 2013](lync-server-2013-exporting-and-importing-voice-routing-configuration.md)

  - [Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)

  - [Testare il routing vocale in Lync Server 2013](lync-server-2013-test-voice-routing.md)

