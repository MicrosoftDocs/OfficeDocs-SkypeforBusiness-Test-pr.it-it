---
title: Configurare la telefonia per un utente
TOCTitle: Configurare la telefonia per un utente
ms:assetid: 4546432e-c839-4517-a2c5-bc0d4d8c6a03
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520988(v=OCS.15)
ms:contentKeyID: 49300374
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare la telefonia per un utente

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Le impostazioni di telefonia sono tra le impostazioni di un account utente che possono essere configurate nel Pannello di controllo di Lync Server per l'utente, ovvero se questo è stato abilitato per Lync Server 2013 e l'organizzazione supporta la telefonia.

Tra le opzioni di telefonia per gli utenti di Lync Server sono incluse le seguenti:

  - **Audio/video disabilitati**   L'utente non può effettuare chiamate con funzionalità audio e video.

  - **Solo da PC a PC**   L'utente può effettuare solo chiamate audio o videochiamate da PC a PC.

  - **VoIP aziendale**   L'utente può utilizzare l'infrastruttura di Lync Server 2013 per instradare tutte le chiamate in arrivo e in uscita. Può inoltre effettuare chiamate da PC a PC.

  - **Controllo delle chiamate remote**   L'utente può utilizzare Lync Server 2013 per controllare il telefono da scrivania e può inoltre effettuare chiamate da PC a PC.

Per informazioni dettagliate sulla configurazione della telefonia per un'organizzazione, vedere [Configurare la telefonia per un utente](lync-server-2013-configure-telephony-for-a-user.md) e [Distribuzione di VoIP aziendale in Lync Server 2013](lync-server-2013-deploying-enterprise-voice.md) nella documentazione relativa alla distribuzione.

## Per configurare la telefonia per un account utente specifico

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Utenti**.

4.  Nella casella **Ricerca utenti** digitare interamente o parzialmente il nome visualizzato, il nome, il cognome, il nome account del sistema degli account di sicurezza (SAM), l'indirizzo SIP o l'URI (Uniform Resource Identifier) linea dell'account utente desiderato e quindi fare clic su **Trova**.

5.  Nella tabella fare clic sull'account utente che si desidera modificare.

6.  Scegliere **Modifica** dal menu **Modifica**.

7.  In **Telefonia** eseguire le operazioni seguenti:
    
      - Per disabilitare le chiamate audio e le videochiamate per l'utente, fare clic su **Audio/video disabilitati**.
    
      - Per abilitare le comunicazioni audio da PC a PC per l'utente, ma non il controllo delle chiamate remote o VoIP aziendale, fare clic su **Solo da PC a PC**. Specificare un valore per **URI linea** per il telefono utilizzato dall'utente per le comunicazioni audio da PC a PC.
    
      - Per instradare le chiamate telefoniche dell'utente utilizzando l'infrastruttura di Lync Server 2010 in conformità con il tipo di criterio di servizio, incluse comunicazioni audio da PC a PC, fare clic su **VoIP aziendale**. In **URI linea** specificare il numero di telefono per VoIP aziendale. In **Criteri dial plan** e **Criteri vocali** specificare i criteri appropriati per l'utente. Per specificare le regole di normalizzazione per la conversione dei numeri di telefono composti dall'utente nel formato E.164, selezionare il profilo località appropriato in **Criteri percorso**.
    
      - Per abilitare il controllo delle chiamate remote, che consente agli utenti di controllare la linea del telefono da scrivania da Lync Server 2013 per effettuare chiamate da PC a PC e da PC a telefono, fare clic su **Controllo delle chiamate remote**. In **URI linea** specificare il numero di telefono per il controllo delle chiamate remote. L'utente deve disporre di un telefono da scrivania e di una connessione PBX per il routing delle chiamate.

## Vedere anche

#### Ulteriori risorse

[Modifica delle proprietà degli account utente](lync-server-2013-modifying-user-account-properties.md)

