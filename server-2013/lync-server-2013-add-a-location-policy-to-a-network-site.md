---
title: Aggiungere criteri percorso a un sito di rete
TOCTitle: Aggiungere criteri percorso a un sito di rete
ms:assetid: 43bfab8a-3d6b-4ca4-8425-879fd910502e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425936(v=OCS.15)
ms:contentKeyID: 49300355
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Aggiungere criteri percorso a un sito di rete

 

_**Ultima modifica dell'argomento:** 2013-02-24_

Negli esempi seguenti viene illustrato come aggiungere in un sito di rete esistente il criterio percorso **Redmond** definito in [Creare criteri percorso in Lync Server 2013](lync-server-2013-create-location-policies.md) e come creare un nuovo sito di rete in cui viene utilizzato il criterio percorso **Redmond**.

Per informazioni dettagliate sull'utilizzo dei siti di rete, vedere nella documentazione relativa a Lync Server Management Shell i cmdlet seguenti:

  - **New-CsNetworkSite**

  - **Get-CsNetworkSite**

  - **Set-CsNetworkSite**

  - **Remove-CsNetworkSite**

## Per assegnare un criterio percorso a un sito di rete esistente

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire i cmdlet seguenti per modificare un sito di rete esistente.
    
    Assegnare il criterio percorso contrassegnato come **Redmond** a un sito di rete esistente denominato **Redmond**.
    
        Set-CsNetworkSite -Identity "Redmond" -NetworkRegionID "NorthAmerica" -LocationPolicy "Redmond"

## Per assegnare un criterio percorso a un nuovo sito di rete

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il cmdlet seguente per creare un nuovo sito di rete.
    
    Creare un nuovo sito di rete nell'area di rete e assegnare il criterio percorso contrassegnato come **Redmond**.
    
        New-CsNetworkSite -Identity "Redmond" -NetworkRegionID "NorthAmerica" -LocationPolicy "Redmond"

