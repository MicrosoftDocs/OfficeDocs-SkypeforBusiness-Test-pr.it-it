---
title: Configurazione di collegamenti delle aree di rete
TOCTitle: Configurazione di collegamenti delle aree di rete
ms:assetid: 952bc93e-e6aa-4539-85c7-2b15f14eb382
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182551(v=OCS.15)
ms:contentKeyID: 49301363
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione di collegamenti delle aree di rete

 

_**Ultima modifica dell'argomento:** 2012-11-01_

È possibile configurare i collegamenti tra due aree di rete nell'ambito del servizio Controllo di ammissione di chiamata. Le aree di una rete sono collegate mediante una connettività WAN fisica. È possibile utilizzare il Pannello di controllo di Lync Server per definire un collegamento tra due aree di rete e impostare limitazioni di larghezza di banda per le connessioni audio e video tra queste aree. Per informazioni dettagliate sull'eliminazione di un collegamento tra aree di rete esistenti, vedere [Eliminazione dei collegamenti delle aree di rete](lync-server-2013-deleting-network-region-links.md).

## Per creare un collegamento area di rete

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Collegamento area**.

4.  Nella pagina **Collegamento area** fare clic su **Nuovo**.

5.  In **Nuovo collegamento area di rete** digitare un valore nel campo **Nome**.
    

    > [!NOTE]
    > Questo valore deve essere univoco nella distribuzione di Lync Server 2013.



6.  Nell'elenco a discesa **Area di rete 1** selezionare una delle due aree da collegare.

7.  Nell'elenco a discesa **Area di rete 2** selezionare l'altra area da collegare. Quest'area deve essere diversa da quella selezionata in Area di rete 1.

8.  (Facoltativo) Se si desidera impostare limitazioni relative alla larghezza di banda delle chiamate audio o video tra le due aree, selezionare un profilo criteri larghezza di banda nell'elenco a discesa **Criteri larghezza di banda** .

9.  Fare clic su **Commit**.

## Per modificare un collegamento area di rete

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Collegamento area**.

4.  Nella pagina **Collegamento area** fare clic sul collegamento area che si desidera modificare.

5.  Scegliere **Mostra dettagli** dal menu **Modifica**.

6.  In **Modifica collegamento area** è possibile modificare le aree collegate o il profilo criteri larghezza di banda per il collegamento.

7.  Fare clic su **Commit**.

## Vedere anche

#### Attività

[Eliminazione dei collegamenti delle aree di rete](lync-server-2013-deleting-network-region-links.md)  

#### Ulteriori risorse

[New-CsNetworkRegionLink](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkRegionLink)  
[Set-CsNetworkRegionLink](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsNetworkRegionLink)  
[Remove-CsNetworkRegionLink](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsNetworkRegionLink)  
[Get-CsNetworkRegionLink](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkRegionLink)

