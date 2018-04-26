---
title: Abilitazione o disabilitazione dell'integrazione con l'archiviazione di Exchange
TOCTitle: Abilitazione o disabilitazione dell'integrazione con l'archiviazione di Exchange
ms:assetid: c08b9ba5-04f6-452a-b44c-c130f1564a34
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205228(v=OCS.15)
ms:contentKeyID: 49301871
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitazione o disabilitazione dell'integrazione con l'archiviazione di Exchange

 

_**Ultima modifica dell'argomento:** 2012-10-09_

Nel Pannello di controllo di Lync Server 2013 è possibile utilizzare le configurazioni di archiviazione per abilitare e disabilitare l'integrazione con l'archivio di Exchange. Sono incluse le configurazioni di archiviazione seguenti:

  - Una configurazione globale che viene creata per impostazione predefinita quando si distribuisce Lync Server 2013.

  - Configurazioni a livello di sito e di pool facoltative che è possibile creare e utilizzare per specificare la modalità di implementazione dell'archiviazione per siti o pool specifici.

Per informazioni dettagliate sulla modalità di implementazione delle configurazioni di archiviazione, incluse le opzioni che è possibile specificare e la gerarchia di tali configurazioni, vedere [Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md) nella documentazione relativa alla pianificazione, alla distribuzione o alle operazioni.

## Per abilitare o disabilitare l'integrazione con l'archivio di Microsoft Exchange

1.  Da un account utente assegnato al ruolo CsArchivingAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di navigazione di sinistra fare clic su **Monitoraggio e archiviazione**, quindi scegliere **Configurazione archiviazione**.

4.  Fare clic sul nome della configurazione globale, del sito o del pool appropriata nell'elenco delle configurazioni di archiviazione, fare clic su **Modifica**, su **Mostra dettagli** e quindi eseguire le operazioni seguenti:
    
      - Per abilitare l'integrazione con l'archivio di Exchange 2013, selezionare la casella di controllo **Integrazione Microsoft Exchange**.
    
      - Per disabilitare l'integrazione con l'archivio di Exchange 2013, deselezionare la casella di controllo **Integrazione Microsoft Exchange**.

5.  Fare clic su **Commit**.

## Vedere anche

#### Concetti

[Funzionamento dell'archiviazione in Lync Server 2013](lync-server-2013-how-archiving-works.md)  

#### Ulteriori risorse

[Gestione delle opzioni di configurazione dell'archiviazione per l'organizzazione, i siti e i pool in Lync Server 2013](lync-server-2013-managing-archiving-configuration-options-for-your-organization-sites-and-pools.md)

