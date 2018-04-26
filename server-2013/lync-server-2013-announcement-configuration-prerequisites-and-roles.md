---
title: 'Lync Server 2013: Prerequisiti e ruoli per la configurazione degli annunci'
TOCTitle: Prerequisiti e ruoli per la configurazione degli annunci
ms:assetid: 82f2dfe9-4c5e-4d65-96a1-96495d506ea4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398658(v=OCS.15)
ms:contentKeyID: 49301166
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Prerequisiti e ruoli per la configurazione degli annunci in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-25_

Gli annunci rappresentano una funzionalità di gestione delle chiamate di VoIP aziendale. In questo argomento vengono descritti i requisiti per la configurazione degli annunci e le assegnazioni dei ruoli necessarie per eseguire le attività di configurazione.

Per questa sezione si presuppone che sia già stata letta la documentazione relativa alla pianificazione degli annunci (vedere [Pianificazione delle funzionalità di gestione delle chiamate in Lync Server 2013](lync-server-2013-planning-for-call-management-features.md)).

## Prerequisiti per la configurazione degli annunci

L' applicazione Annuncio richiede i componenti seguenti:

  - Servizio applicazione

  - applicazione Response Group

  - Archivio file, per la memorizzazione dei file audio

Tutti questi componenti vengono installati per impostazione predefinita quando si distribuisce VoIP aziendale.

## Ruoli di configurazione degli annunci

È possibile utilizzare gli strumenti di amministrazione seguenti per configurare gli annunci:

  - Pannello di controllo di Lync Server

  - Lync Server Management Shell

Per la configurazione dell' applicazione Annuncio è necessario uno dei ruoli amministrativi seguenti:

  - **CsVoiceAdministrator**   Questo ruolo di amministratore è autorizzato a creare, configurare e gestire tutti i criteri e le impostazioni correlati alle funzionalità vocali, tra cui le impostazioni degli annunci.

  - **CsServerAdministrator**   Questo ruolo di amministratore è autorizzato a gestire, monitorare e risolvere i problemi relativi a server e servizi, nonché configurare tutte le impostazioni degli annunci.

  - **CsAdministrator**   Questo ruolo di amministratore è autorizzato a eseguire tutte le attività di amministrazione e a modificare tutte le impostazioni.

  - **CsViewOnlyAdministrator**   Questo ruolo di amministratore è autorizzato a visualizzare la distribuzione per monitorarne l'integrità.


> [!NOTE]
> Per informazioni dettagliate sui diritti utente amministrativi, vedere <A href="lync-server-2013-planning-for-role-based-access-control.md">Pianificazione del controllo di accesso basato sui ruoli in Lync Server 2013</A> nella documentazione relativa alla pianificazione.



## Vedere anche

#### Concetti

[Distribuzione di VoIP aziendale in Lync Server 2013](lync-server-2013-deploying-enterprise-voice.md)  

#### Ulteriori risorse

[Pianificazione delle funzionalità di gestione delle chiamate in Lync Server 2013](lync-server-2013-planning-for-call-management-features.md)

