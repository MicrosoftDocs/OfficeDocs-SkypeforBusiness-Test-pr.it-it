---
title: Eliminazione delle aree di rete esistenti
TOCTitle: Eliminazione delle aree di rete esistenti
ms:assetid: c7293a2f-2b49-4c4a-903f-f7edcea2bc5f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721882(v=OCS.15)
ms:contentKeyID: 49887747
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminazione delle aree di rete esistenti

 

_**Ultima modifica dell'argomento:** 2013-02-21_

Un'area di rete collega diverse parti di una rete dislocate in diverse aree geografiche. Ogni area di rete deve essere associata a un sito centrale. Il sito centrale è il sito del data center in cui è in esecuzione il servizio dei criteri di larghezza di banda Controllo di ammissione di chiamata. È possibile utilizzare il Pannello di controllo di Lync Server per configurare le aree di rete. Le aree di rete includono impostazioni che determinano se abilitare percorsi alternativi Internet per le connessioni audio e video. Dal Pannello di controllo di Lync Server è possibile creare, modificare o eliminare un'area di rete. Per informazioni dettagliate sulla creazione o la modifica di aree di rete esistenti, vedere [Creazione o modifica delle aree di rete](lync-server-2013-creating-or-modifying-network-regions.md).

## Per eliminare un'area di rete

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Area**.

4.  Nella pagina **Area** fare clic sull'area che si desidera eliminare.
    

    > [!NOTE]
    > È possibile eliminare più aree contemporaneamente. A tale scopo, premere CTRL e selezionare più aree tenendo premuto CTRL. Per selezionare tutte le aree, scegliere <STRONG>Seleziona tutto</STRONG> dal menu <STRONG>Modifica</STRONG>.



5.  Scegliere **Elimina** dal menu **Modifica**.

6.  Fare clic su **OK**.
    

    > [!WARNING]
    > Non è possibile rimuovere un'area di rete se è associata a un sito di rete. Se si tenta di rimuovere un'area associata a un sito, verrà visualizzato un messaggio di errore. Per scoprire se un'area è associata a siti, selezionare l'area e quindi scegliere <STRONG>Mostra dettagli</STRONG> dal menu <STRONG>Modifica</STRONG>.



## Vedere anche

#### Attività

[Creazione o modifica delle aree di rete](lync-server-2013-creating-or-modifying-network-regions.md)

