---
title: Creazione o modifica delle route delle aree di rete
TOCTitle: Creazione o modifica delle route delle aree di rete
ms:assetid: 76993daa-76c2-4cec-8363-de8aebef0145
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg521016(v=OCS.15)
ms:contentKeyID: 49301019
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creazione o modifica delle route delle aree di rete

 

_**Ultima modifica dell'argomento:** 2012-10-08_

Ogni area di una configurazione di controllo di ammissione di chiamata deve in qualche modo poter accedere a tutte le altre aree. Mentre i collegamenti area impostano limitazioni della larghezza di banda nelle connessioni tra aree e rappresentano anche i collegamenti fisici, una route determina il percorso collegato che verrà attraversato dalla connessione per passare da un'area all'altra. È possibile utilizzare il Pannello di controllo di Lync Server per configurare le route aree di rete. Nel Pannello di controllo di Lync Server è possibile creare, modificare o eliminare una route area di rete. Utilizzare questo argomento per creare o modificare una nuova route area di rete. Per informazioni dettagliate sull'eliminazione di route area di rete esistenti, vedere [Eliminazione delle route delle aree di rete esistenti](lync-server-2013-deleting-existing-network-region-routes.md).

## Per creare una route area di rete

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Route area**.

4.  Nella pagina **Route area** fare clic su **Nuovo**.

5.  In **Nuova route area** digitare un valore nel campo **Nome**.
    

    > [!NOTE]
    > Questo valore deve essere univoco nella distribuzione di Microsoft Lync Server 2013.



6.  Nell'elenco a discesa **Area di rete 1** selezionare una delle due aree da connettere tramite la route.

7.  Nell'elenco a discesa **Area di rete 2** selezionare l'altra area per la route. Questa area deve essere diversa da quella selezionata in Area di rete 1.

8.  Utilizzare la casella di riepilogo **Collegamenti aree di rete** per aggiungere collegamenti area di rete alla route. Fare clic sul pulsante **Aggiungi** per visualizzare la pagina **Collegamento area**. Fare clic su un collegamento area da aggiungere alla route e quindi fare clic su **OK**.
    

    > [!NOTE]
    > Continuare a fare clic sul pulsante <STRONG>Aggiungi</STRONG> per aggiungere altri collegamenti oppure selezionare un collegamento e fare clic su <STRONG>Rimuovi</STRONG> per rimuoverlo.



9.  Fare clic su **Commit**.

## Per modificare una route area di rete

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Route area**.

4.  Nella pagina **Route area** fare clic sulla route area che si desidera modificare.

5.  Scegliere **Mostra dettagli** dal menu **Modifica**.

6.  In **Modifica route area** è possibile modificare le aree unite dalla route e i collegamenti area associati alla route.

7.  Fare clic su **Commit**.

## Vedere anche

#### Attività

[Eliminazione delle route delle aree di rete esistenti](lync-server-2013-deleting-existing-network-region-routes.md)

