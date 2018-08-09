---
title: "Lync Server 2013: Configura siti di rete per CAC"
TOCTitle: "Lync Server 2013: Configura siti di rete per CAC"
ms:assetid: afcea38f-5789-45ec-97af-c6e38364950c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412840(v=OCS.15)
ms:contentKeyID: 49301676
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare siti di rete per il servizio Controllo di ammissione di chiamata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-05_

> [!IMPORTANT]  
> Se sono stati già creati siti di rete per il servizio per chiamate di emergenza (E9-1-1) o per il bypass multimediale, è possibile modificare i siti di rete esistenti per applicare un profilo di criteri di larghezza di banda utilizzando il cmdlet <strong>Set-CsNetworkSite</strong>. Per un esempio della modifica di un sito di rete, vedere <a href="lync-server-2013-create-or-modify-a-network-site.md">Creare o modificare un sito di rete in Lync Server 2013</a>.

I *siti di rete* sono gli uffici o le postazioni in ogni area di rete delle distribuzioni del servizio Controllo di ammissione di chiamata (CAC), del servizio per chiamate di emergenza E9-1-1 e del bypass multimediale. Utilizzare le procedure seguenti per creare siti di rete da allineare ai siti di rete nella topologia di rete di esempio per il servizio Controllo di ammissione di chiamata. In queste procedure viene illustrato come creare e configurare siti di rete vincolati dalla larghezza di banda WAN che quindi richiedono criteri di larghezza di banda per limitare il flusso di traffico audio o video in tempo reale.

Nella distribuzione di esempio del servizio Controllo di ammissione di chiamata, il Nord America ha sei siti. Tre di questi siti sono vincolati dalla larghezza di banda WAN: Reno, Portland e Albuquerque. Gli altri tre siti, *non* vincolati dalla larghezza di banda WAN, sono: New York, Chicago e Detroit. Per un esempio della creazione o della modifica di questi altri siti di rete, vedere [Creare o modificare un sito di rete in Lync Server 2013](lync-server-2013-create-or-modify-a-network-site.md).

Per visualizzare la topologia di rete di esempio, vedere [Esempio: raccolta dei requisiti dell'organizzazione per il controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-example-of-gathering-your-requirements-for-call-admission-control.md) nella documentazione relativa alla pianificazione.


> [!NOTE]
> Nella procedura seguente viene utilizzato Lync Server Management Shell per creare un sito di rete. Per informazioni dettagliate sull'utilizzo del Pannello di controllo di Lync Server per creare un sito di rete, vedere <A href="lync-server-2013-create-or-modify-a-network-site.md">Creare o modificare un sito di rete in Lync Server 2013</A>.



## Per creare siti di rete per il servizio Controllo di ammissione di chiamata

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il cmdlet **New-CsNetworkSite** per creare i siti di rete e applicare un profilo di criteri di larghezza di banda appropriato a ogni sito. Ad esempio, eseguire:
    
    ```
    New-CsNetworkSite -NetworkSiteID Reno -Description "NA:Branch office for sales force" -NetworkRegionID NorthAmerica -BWPolicyProfileID 10MB_Link
    ```
    ```
    New-CsNetworkSite -NetworkSiteID Portland -Description "NA:Branch office for marketing force" -NetworkRegionID NorthAmerica -BWPolicyProfileID 5MB_Link
    ```
    ```
    New-CsNetworkSite -NetworkSiteID Albuquerque -Description "NA:Branch office for SouthWest sales" -NetworkRegionID EMEA -BWPolicyProfileID 10MB_Link
    ```

3.  Per completare la creazione dei siti di rete per l'intera topologia di esempio, ripetere il passaggio 2 per i siti di rete vincolati dalla larghezza di banda nelle aree EMEA e APAC.

