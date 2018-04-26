---
title: Prerequisiti di configurazione e diritti utente per la risposta alle chiamate di gruppo
TOCTitle: Prerequisiti di configurazione e diritti utente per la risposta alle chiamate di gruppo
ms:assetid: 8757b1d3-751d-49c3-b1b8-b678f663f18e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ945641(v=OCS.15)
ms:contentKeyID: 52062201
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Prerequisiti di configurazione e diritti utente per la risposta alle chiamate di gruppo

 

_**Ultima modifica dell'argomento:** 2013-01-30_

La risposta alle chiamate di gruppo è una funzionalità di gestione delle chiamate installata per impostazione predefinita quando si distribuisce VoIP aziendale. In questo argomento vengono illustrati gli elementi di cui si deve disporre prima di poter configurare la risposta alle chiamate di gruppo e quali diritti utente sono necessari per eseguire le attività di configurazione.

Per questa sezione si presuppone che sia già stata letta la documentazione sulla pianificazione relativa alla risposta alle chiamate di gruppo (vedere [Pianificazione della risposta alle chiamate di gruppo in Lync Server 2013](lync-server-2013-planning-for-group-call-pickup.md)).

## Prerequisiti per la configurazione della risposta alle chiamate di gruppo

Per la risposta alle chiamate di gruppo sono necessari i componenti seguenti:

  - Servizio applicazione

  - applicazione Parcheggio di chiamata

Questi componenti vengono installati automaticamente quando si distribuisce VoIP aziendale.

## Diritti utente per la configurazione della risposta alle chiamate di gruppo

È possibile utilizzare gli strumenti amministrativi seguenti per configurare la risposta alle chiamate di gruppo:

  - Lync Server Management Shell

  - Strumento del Resource Kit SEFAUtil

Utilizzare Lync Server Management Shell per creare e gestire i gruppi per la risposta alle chiamate di gruppo nella tabella dei codici orbit di Parcheggio di chiamata. Utilizzare lo strumento del Resource Kit SEFAUtil per assegnare un gruppo per la risposta alle chiamate di gruppo e abilitare o disabilitare la funzionalità per gli utenti.

Per la configurazione della risposta alle chiamate di gruppo è richiesto uno dei ruoli amministrativi seguenti, a seconda dell'attività:

  - **CsVoiceAdministrator:** questo ruolo amministrativo consente di creare, configurare e gestire tutte le impostazioni e i criteri vocali.

  - **CsUserAdministrator:** questo ruolo amministrativo consente di abilitare la risposta alle chiamate di gruppo per gli utenti. Dispone inoltre dell'accesso per la visualizzazione in sola lettura di tutte le configurazioni vocali.

  - **CsServerAdministrator:** questo ruolo amministrativo consente di gestire e monitorare i server e i servizi, nonché di risolvere i relativi problemi.

  - **CsAdministrator:** questo ruolo amministrativo consente di eseguire tutte le attività di CsVoiceAdministrator, CsServerAdministrator e CsUserAdministrator.


> [!NOTE]
> Per informazioni dettagliate sui diritti amministrativi, vedere <A href="lync-server-2013-planning-for-role-based-access-control.md">Pianificazione del controllo di accesso basato sui ruoli in Lync Server 2013</A> nella documentazione relativa alla pianificazione.



## Vedere anche

#### Concetti

[Distribuzione di VoIP aziendale in Lync Server 2013](lync-server-2013-deploying-enterprise-voice.md)  

#### Ulteriori risorse

[Pianificazione delle funzionalità di gestione delle chiamate in Lync Server 2013](lync-server-2013-planning-for-call-management-features.md)

