---
title: Visualizzazione delle informazioni sui collegamenti delle aree di rete
TOCTitle: Visualizzazione delle informazioni sui collegamenti delle aree di rete
ms:assetid: 7b6b2ea2-83d8-4376-afb2-70e5d2cf6444
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688102(v=OCS.15)
ms:contentKeyID: 49887620
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzazione delle informazioni sui collegamenti delle aree di rete

 

_**Ultima modifica dell'argomento:** 2013-02-23_

È possibile visualizzare i collegamenti tra due aree di rete nell'ambito del servizio Controllo di ammissione di chiamata. Le aree di una rete sono collegate mediante una connettività WAN fisica. È possibile utilizzare Pannello di controllo di Lync Server per visualizzare un collegamento esistente tra due aree di rete. Per informazioni dettagliate sulla creazione e la modifica di collegamenti tra aree di rete, vedere [Configurazione di collegamenti delle aree di rete](lync-server-2013-configuring-network-region-links.md)

## Per visualizzare un collegamento area di rete in Pannello di controllo di Lync Server

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Collegamento area**.

4.  Nella pagina **Collegamento area** fare clic sul collegamento area che si desidera visualizzare.
    

    > [!NOTE]
    > È possibile visualizzare informazioni su un collegamento aree alla volta.



5.  Scegliere **Elimina** dal menu **Mostra dettagli**.

## Visualizzare le informazioni sulle aree di rete utilizzando i cmdlet Lync Server Management Shell

È inoltre collegamenti aree di rete utilizzando i cmdlet Lync Server Management Shell e **Get-CsNetworkRegionLink**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per visualizzare informazioni su un collegamento area di rete

  - Per visualizzare le informazioni relative a tutti i collegamenti aree di rete, digitare il seguente comando in Lync Server Management Shell e premere INVIO:
    
        Get-CsNetworkRegionLink
    
    Il comando restituisce informazioni simili a questa:
    
        Identity            : NorthwestToCalifornia
        BWPolicyProfileID   :
        NetworkRegionLinkID : NorthwestToCalifornia
        NetworkRegionID1    : Pacific Northwest
        NetworkRegionID2    : California

Per informazioni dettagliate, vedere [Get-CsNetworkRegionLink](get-csnetworkregionlink.md).

## Vedere anche

#### Attività

[Configurazione dei collegamenti di siti di rete](lync-server-2013-configuring-network-site-links.md)

