---
title: Creare route tra aree di rete
TOCTitle: Creare route tra aree di rete
ms:assetid: 5555262a-a502-4b01-9593-836dd30064f5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398368(v=OCS.15)
ms:contentKeyID: 49300605
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare route tra aree di rete

 

_**Ultima modifica dell'argomento:** 2012-10-20_

Una *route tra aree di rete* definisce la route tra una coppia di aree di rete. Ogni coppia di aree di rete nella distribuzione del servizio Controllo di ammissione di chiamata richiede una route di questo tipo. In tal modo ogni area di rete della distribuzione può accedere a tutte le altre aree.

Se i collegamenti di area impostano limitazioni della larghezza di banda per le connessioni tra le aree, una route tra aree determina il percorso collegato attraversato dalla connessione per passare da un'area all'altra.

Per informazioni dettagliate sull'utilizzo delle route tra aree di rete, vedere la documentazione di Lync Server Management Shell per i cmdlet seguenti:

  - [New-CsNetworkInterRegionRoute](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkInterRegionRoute)

  - [Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)

  - [Set-CsNetworkInterRegionRoute](set-csnetworkinterregionroute.md)

  - [Remove-CsNetworkInterRegionRoute](remove-csnetworkinterregionroute.md)

Nella topologia di esempio, le route tra aree di rete devono essere definite per ognuna delle tre coppie di aree, ovvero Nord America/EMEA, EMEA/APAC e Nord America/APAC.

## Per creare route tra aree di rete tramite Lync Server Management Shell

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il cmdlet **New-CsNetworkInterRegionRoute** per definire le route richieste. Ad esempio, eseguire:
    
        New-CsNetworkInterRegionRoute -Identity NorthAmerica_EMEA_Route -NetworkRegionID1 NorthAmerica -NetworkRegionID2 EMEA -NetworkRegionLinkIDs "NA-EMEA-LINK"
    
        New-CsNetworkInterRegionRoute -Identity NorthAmerica_APAC_Route -NetworkRegionID1 NorthAmerica -NetworkRegionID2 APAC -NetworkRegionLinkIDs "NA-EMEA-LINK, EMEA-APAC-LINK"
    
        New-CsNetworkInterRegionRoute -Identity EMEA_APAC_Route -NetworkRegionID1 EMEA -NetworkRegionID2 APAC -NetworkRegionLinkIDs "EMEA-APAC-LINK"
    

    > [!NOTE]
    > La route tra aree di rete Nord America/APAC richiede due collegamenti tra aree di rete perché non esiste un collegamento diretto tra le due aree.



## Per creare route tra aree di rete tramite Pannello di controllo di Lync Server

1.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

2.  Sulla barra di spostamento sinistra fare clic su **Configurazione di rete**.

3.  Fare clic sul pulsante di spostamento **Route area**.

4.  Fare clic su **Nuovo**.

5.  Nella pagina **Nuova route aree di rete** fare clic su **Nome** e quindi digitare un nome per la route tra aree di rete.

6.  Fare clic su **Area di rete 1** e quindi fare clic su un'area di rete nell'elenco per il routing all'area di rete 2.

7.  Fare clic su **Area di rete 2** e quindi fare clic su un'area di rete nell'elenco per il routing all'area di rete 1.

8.  Fare clic su **Aggiungi** accanto al campo **Collegamenti aree di rete** e quindi aggiungere un collegamento all'area di rete che verrà usato come route tra aree di rete.
    

    > [!NOTE]
    > Se si crea una route per due aree di rete tra le quali non esiste un collegamento diretto, è necessario aggiungere tutti i collegamenti necessari per completare la route. Ad esempio, la route tra le aree di rete Nord America/APAC richiede due collegamenti tra aree di rete perché non esiste un collegamento diretto tra le due aree.



9.  Fare clic su **Commit**.

10. Per completare la creazione delle route tra aree di rete per la topologia, ripetere i passaggi da 4 a 9 con le impostazioni per le altre route.

