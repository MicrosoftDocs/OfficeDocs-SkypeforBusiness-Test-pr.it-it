---
title: Eliminazione delle route delle aree di rete esistenti
TOCTitle: Eliminazione delle route delle aree di rete esistenti
ms:assetid: 6256ff80-5f1e-48b4-928b-24aeb3c1a0e7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688074(v=OCS.15)
ms:contentKeyID: 49887584
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminazione delle route delle aree di rete esistenti

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Ogni area di una configurazione di controllo di ammissione di chiamata deve in qualche modo poter accedere a tutte le altre aree. Mentre i collegamenti area impostano limitazioni della larghezza di banda nelle connessioni tra aree e rappresentano anche i collegamenti fisici, una route determina il percorso collegato che verrà attraversato dalla connessione per passare da un'area all'altra. È possibile utilizzare il Pannello di controllo di Lync Server per configurare le route area di rete. Nel Pannello di controllo di Lync Server è possibile creare, modificare o eliminare una route area di rete. Utilizzare questo argomento per informazioni su come eliminare le route area di rete. Per informazioni dettagliate sulla creazione o la modifica delle route area di rete, vedere [Creazione o modifica delle route delle aree di rete](lync-server-2013-creating-or-modifying-network-region-routes.md).

## Per eliminare una route area di rete

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Route area**.

4.  Nella pagina **Route area** fare clic sulla route area che si desidera eliminare.
    

    > [!NOTE]
    > È possibile eliminare più di una route area per volta. A tale scopo, selezionare più route area tenendo premuto CTRL oppure, per selezionare tutte le route area, scegliere <STRONG>Seleziona tutto</STRONG> dal menu <STRONG>Modifica</STRONG>.



5.  Scegliere **Elimina** dal menu **Modifica**.

6.  Fare clic su **OK**.

## Vedere anche

#### Attività

[Creazione o modifica delle route delle aree di rete](lync-server-2013-creating-or-modifying-network-region-routes.md)  

#### Concetti

[Configurare una route area tra reti](https://technet.microsoft.com/it-it/library/gg133706\(v=ocs.15\))  

#### Ulteriori risorse

[New-CsNetworkInterRegionRoute](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkInterRegionRoute)  
[Set-CsNetworkInterRegionRoute](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsNetworkInterRegionRoute)  
[Remove-CsNetworkInterRegionRoute](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsNetworkInterRegionRoute)  
[Get-CsNetworkInterRegionRoute](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkInterRegionRoute)

