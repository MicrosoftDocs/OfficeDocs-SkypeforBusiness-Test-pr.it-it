---
title: Abilitazione del bypass multimediale della rete
TOCTitle: Abilitazione del bypass multimediale della rete
ms:assetid: 95c4fa06-49d3-41ac-acdc-7dcda66e5508
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182552(v=OCS.15)
ms:contentKeyID: 49301371
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitazione del bypass multimediale della rete

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Le impostazioni di bypass multimediale si applicano globalmente in una distribuzione di Microsoft Lync Server 2013. Il bypass multimediale consente alle chiamate di ignorare il Mediation Server. Per informazioni dettagliate su quando utilizzare il bypass multimediale, vedere [Pianificazione del bypass multimediale in Lync Server 2013](lync-server-2013-planning-for-media-bypass.md) nella sezione relativa alla pianificazione.

È possibile abilitare e configurare il bypass multimediale dal Pannello di controllo di Lync Server.

## Per abilitare e configurare il bypass multimediale

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Globale**.

4.  Nella pagina **Globale** fare clic sulla scheda della configurazione **Globale**. Esiste sempre una sola configurazione ed è sempre denominata Globale.

5.  Scegliere **Mostra dettagli** dal menu **Modifica**.

6.  Nella pagina **Modifica impostazioni globali** selezionare la casella di controllo **Abilita bypass multimediale**.

7.  Selezionare una delle opzioni seguenti:
    
      - **Ignora sempre**   Selezionare questa opzione per tentare il bypass multimediale per tutte le chiamate. Se è abilitato il controllo di ammissione di chiamata, questa opzione non sarà disponibile. Se non è abilitato, selezionare questa opzione nelle situazioni seguenti:
        
          - Non è necessario il controllo della larghezza di banda.
        
          - Non è necessaria una configurazione con granularità fine per determinare quando dovrebbe avvenire il bypass.
        
          - Esiste la piena connettività tra gateway e client.
    
      - **Utilizza configurazione siti e aree**   Se è abilitato il controllo di ammissione di chiamata, questa opzione è selezionata per impostazione predefinita e non è possibile modificarla. Quando è selezionata questa opzione, i siti e le aree della configurazione di rete verranno utilizzati per determinare quando è possibile il bypass multimediale. Selezionando questa opzione si sceglie di abilitare il bypass per i siti non mappati. Selezionare la casella di controllo **Abilita bypass per siti non mappati** solo se si dispone di uno o più siti di grandi dimensioni associati alla stessa area e non soggetti a vincoli di larghezza di banda (ad esempio un sito centrale di grandi dimensioni), ma si dispone anche di alcuni siti di succursale associati alla stessa area e soggetti a vincoli di larghezza di banda. Se si abilita il bypass per i siti non mappati, la configurazione viene semplificata in quanto è sufficiente specificare solo le subnet associate ai siti di succursale anziché specificare tutte le subnet associate a tutti i siti. È consigliabile non selezionare la casella di controllo **Abilita bypass per siti non mappati** se è abilitato il controllo di ammissione di chiamata.

8.  Fare clic su **Commit** per salvare le modifiche.

## Vedere anche

#### Attività

[Disabilitazione del bypass multimediale della rete](lync-server-2013-disabling-network-media-bypass.md)  

#### Concetti

[Opzioni globali di bypass multimediale in Lync Server 2013](lync-server-2013-global-media-bypass-options.md)  

#### Ulteriori risorse

[Pianificazione del bypass multimediale in Lync Server 2013](lync-server-2013-planning-for-media-bypass.md)

