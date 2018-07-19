---
title: Creare collegamenti di aree di rete
TOCTitle: Creare collegamenti di aree di rete
ms:assetid: f8163910-8935-475d-88a2-3aa44feb9dbe
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413047(v=OCS.15)
ms:contentKeyID: 49302525
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare collegamenti di aree di rete

 

_**Ultima modifica dell'argomento:** 2012-10-19_

Le aree all'interno di una rete sono collegate tramite connettività fisica WAN. Un *collegamento di aree di rete* crea un collegamento tra due aree configurate per Controllo di ammissione di chiamata e imposta i limiti di larghezza di banda per il traffico audio e video tra tali aree.

Per informazioni dettagliate sull'utilizzo di collegamenti area di rete, vedere la documentazione di Lync Server Management Shell per i cmdlet seguenti:

  - [New-CsNetworkRegionLink](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkRegionLink)

  - [Get-CsNetworkRegionLink](get-csnetworkregionlink.md)

  - [Set-CsNetworkRegionLink](set-csnetworkregionlink.md)

  - [Remove-CsNetworkRegionLink](remove-csnetworkregionlink.md)

Nella topologia di esempio è presente un collegamento tra il Nord America e le aree APAC e un collegamento tra le aree EMEA e APAC. Ognuno di questi collegamenti area è vincolato dalla larghezza di banda WAN, come descritto nella tabella di informazioni sulla larghezza di banda dei collegamenti area nella sezione [Esempio: raccolta dei requisiti dell'organizzazione per il controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-example-of-gathering-your-requirements-for-call-admission-control.md) della documentazione relativa alla pianificazione.

## Per creare collegamenti area di rete utilizzando Lync Server Management Shell

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il cmdlet New-CsNetworkRegionLink per creare i collegamenti area di rete e applicare i profili di criteri di larghezza di banda appropriati. Ad esempio, eseguire:
    
        New-CsNetworkRegionLink -NetworkRegionLinkID NA-EMEA-LINK -NetworkRegionID1 NorthAmerica -NetworkRegionID2 EMEA -BWPolicyProfileID 50Mb_Link
    
        New-CsNetworkRegionLink -NetworkRegionLinkID EMEA-APAC-LINK -NetworkRegionID1 EMEA -NetworkRegionID2 APAC -BWPolicyProfileID 25Mb_Link

## Per creare collegamenti area di rete utilizzando il pannello di controllo Lync Server

1.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

2.  Sulla barra di spostamento sinistra fare clic su **Configurazione di rete**.

3.  Fare clic sul pulsante di spostamento **Collegamento area**.

4.  Fare clic su **Nuovo**.

5.  Nella pagina **Nuovo collegamento area di rete** fare clic su **Nome** e quindi digitare un nome per il collegamento area di rete.

6.  Fare clic su **Area di rete 1** e quindi fare clic sull'area di rete nell'elenco che si desidera collegare all'Area di rete 2.

7.  Fare clic su **Area di rete 2** e quindi fare clic su un'area di rete nell'elenco che si desidera collegare all'Area di rete 1.

8.  Facoltativamente, fare clic su **Criteri larghezza di banda** e selezionare il profilo di criteri di larghezza di banda che si desidera applicare al collegamento area di rete.
    

    > [!NOTE]
    > Applicare criteri di larghezza di banda solo se il collegamento area di rete è vincolato dalla larghezza di banda e si desidera utilizzare CAC per controllare il traffico multimediale su tale collegamento.



9.  Fare clic su **Commit**.

10. Per completare la creazione dei collegamenti area di rete per la topologia, ripetere i passaggi da 4 a 9 con le impostazioni per le altre aree.

