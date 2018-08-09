---
title: "Lync Server 2013: Definisce i vostri requisiti per VoIP aziendale"
TOCTitle: Definizione dei requisiti dell'organizzazione per VoIP aziendale
ms:assetid: 3310f78e-c658-4557-95fa-159ce3c22953
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425826(v=OCS.15)
ms:contentKeyID: 49300116
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definizione dei requisiti dell'organizzazione per VoIP aziendale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-08-07_

In questo argomento viene fornita una panoramica delle considerazioni da fare sulle aree, sui siti e sui collegamenti tra siti della topologia e sull'importanza di tali elementi per la distribuzione di VoIP aziendale. Per informazioni dettagliate utili ai fini di queste decisioni, vedere [Impostazioni di rete per le funzionalità di VoIP aziendale avanzate in Lync Server 2013](lync-server-2013-network-settings-for-the-advanced-enterprise-voice-features.md) nella documentazione relativa alla pianificazione.

## Siti e aree

Identificare innanzitutto i siti della topologia in cui verrà distribuito VoIP aziendale e le aree di rete a cui appartengono tali siti. Valutare in particolare il modo in cui verrà fornita la connettività PSTN (Public Switched Telephone Network) a ogni sito. Per motivi logistici e di gestione, le aree a cui appartengono questi siti possono rappresentare un fattore decisivo. Decidere dove verranno distribuiti i gateway localmente, dove verrà distribuito Survivable Branch Appliance (SBA) e dove è possibile configurare trunk SIP (localmente o nel sito centrale) per un provider di servizi di telefonia Internet (ITSP).

## Collegamenti di rete tra siti

È inoltre necessario tenere conto dell'uso della larghezza di banda previsto nei collegamenti di rete tra il sito centrale e i relativi siti di succursale. Se si dispone di collegamenti WAN resilienti tra i siti o si prevede di distribuirli, è consigliabile distribuire un gateway in ogni sito di succursale per fornire la terminazione DID (Direct Inward Dial) locale per gli utenti presso tali siti. Se si dispone di collegamenti WAN resilienti, ma è probabile che la larghezza di banda di un collegamento WAN sia vincolata, configurare il servizio Controllo di ammissione di chiamata per il collegamento. Se invece non si dispone di collegamenti WAN resilienti, si ospitano meno di 1000 utenti nel sito di succursale e non sono disponibili amministratori di Lync Server locali con formazione specifica, è consigliabile distribuire un Survivable Branch Appliance nel sito di succursale. Se si ospita un numero di utenti compreso tra 1000 e 5000 nel sito di succursale, non si dispone di una connessione WAN resiliente e sono disponibili amministratori di Lync Server con formazione specifica, è consigliabile distribuire un Survivable Branch Server con un piccolo gateway nel sito di succursale. Prendere inoltre in considerazione l'eventualità di abilitare il bypass multimediale nei collegamenti vincolati se si dispone di un peer gateway che supporta il bypass multimediale.

## Vedere anche

#### Concetti

[Impostazioni di rete per le funzionalità di VoIP aziendale avanzate in Lync Server 2013](lync-server-2013-network-settings-for-the-advanced-enterprise-voice-features.md)

