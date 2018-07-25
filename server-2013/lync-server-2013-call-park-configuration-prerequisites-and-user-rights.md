---
title: 'Lync Server 2013: Diritti utente e prerequisiti per la configurazione del parcheggio di chiamata'
TOCTitle: Diritti utente e prerequisiti per la configurazione del parcheggio di chiamata
ms:assetid: 25b8cfe0-e4e7-487c-9e78-8c040f629059
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425730(v=OCS.15)
ms:contentKeyID: 49299963
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Diritti utente e prerequisiti per la configurazione del parcheggio di chiamata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-10_

L' Parcheggio di chiamata è una funzionalità di gestione delle chiamate che viene installata per impostazione predefinita quando si distribuisce l' VoIP aziendale. In questo argomento vengono illustrati gli elementi di cui si deve disporre prima di poter configurare Parcheggio di chiamata e quali diritti utente sono necessari per eseguire le attività di configurazione.

> [!important]  
> Per i file di musica di attesa personalizzati per l' applicazione Parcheggio di chiamata non viene eseguito il backup come parte del processo di ripristino di emergenza di Lync Server 2013 e i file verranno persi se i file caricati nel pool vengono danneggiati o cancellati. Conservare sempre una copia di backup separata dei file di musica di attesa personalizzati caricati per l' Parcheggio di chiamata.

In questa sezione si presuppone che sia stata letta la documentazione relativa alla pianificazione per l' Parcheggio di chiamata (vedere [Pianificazione delle funzionalità di gestione delle chiamate in Lync Server 2013](lync-server-2013-planning-for-call-management-features.md)).

## Parcheggio di chiamata Prerequisiti di configurazione

Parcheggio di chiamata richiede i componenti seguenti:

  - Servizio applicazione

  - applicazione Parcheggio di chiamata

Questi componenti vengono installati automaticamente quando si distribuisce VoIP aziendale.

Se si desidera che i chiamanti ascoltino musica nell'intervallo di tempo in cui la chiamata è parcheggiata, sarà necessario inoltre un file di musica di attesa. Quando si distribuisce VoIP aziendale, viene installato automaticamente un file di musica di attesa predefinito. È possibile sostituire il file predefinito con un proprio file di musica di attesa. Il file audio per l' Parcheggio di chiamata è contenuto nell'archivio file.

## Diritti utente per la configurazione dell' Parcheggio di chiamata

È possibile utilizzare gli strumenti amministrativi seguenti per configurare Parcheggio di chiamata:

  - Pannello di controllo di Lync Server

  - Lync Server Management Shell

Questi strumenti consentono di configurare la tabella di codici orbit dell' Parcheggio di chiamata e altre impostazioni utilizzate dall' Parcheggio di chiamata.

Per la configurazione dell' Parcheggio di chiamata è richiesto uno dei ruoli amministrativi seguenti, a seconda dell'attività:

  - **CsVoiceAdministrator :** questo ruolo amministrativo consente di creare, configurare e gestire tutte le impostazioni e i criteri vocali.

  - **CsUserAdministrator :** questo ruolo amministrativo consente di abilitare l' Parcheggio di chiamata nel criterio vocale. Dispone inoltre dell'accesso per la visualizzazione di sola lettura di tutte le configurazioni vocali.

  - **CsServerAdministrator :** questo ruolo amministrativo consente di gestire e monitorare i server e i servizi, nonché di risolvere i relativi problemi.

  - **CsAdministrator :** questo ruolo amministrativo consente di eseguire tutte le attività di CsVoiceAdministrator, CsServerAdministrator e CsUserAdministrator.


> [!NOTE]
> Per informazioni dettagliate sui diritti amministrativi, vedere <A href="lync-server-2013-planning-for-role-based-access-control.md">Pianificazione del controllo di accesso basato sui ruoli in Lync Server 2013</A> nella documentazione relativa alla pianificazione.



## Vedere anche

#### Concetti

[Distribuzione di VoIP aziendale in Lync Server 2013](lync-server-2013-deploying-enterprise-voice.md)  

#### Ulteriori risorse

[Pianificazione delle funzionalità di gestione delle chiamate in Lync Server 2013](lync-server-2013-planning-for-call-management-features.md)

