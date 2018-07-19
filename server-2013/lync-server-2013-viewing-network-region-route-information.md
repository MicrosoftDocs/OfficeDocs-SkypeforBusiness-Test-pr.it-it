---
title: Visualizzazione delle informazioni sulle route area di rete
TOCTitle: Visualizzazione delle informazioni sulle route area di rete
ms:assetid: 34dd9fa3-e695-4680-b244-3019298b5009
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688021(v=OCS.15)
ms:contentKeyID: 49887518
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzazione delle informazioni sulle route area di rete

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Ogni area di una configurazione di controllo di ammissione di chiamata deve in qualche modo poter accedere a tutte le altre aree. Mentre i collegamenti area impostano limitazioni della larghezza di banda nelle connessioni tra aree e rappresentano anche i collegamenti fisici, una route determina il percorso collegato che verrà attraversato dalla connessione per passare da un'area all'altra. Usare le procedure seguenti per visualizzare le route area di rete esistenti nel Pannello di controllo di Lync Server 2013 o in Lync Server 2013 Management Shell. Per informazioni dettagliate sulla creazione o la modifica delle route area di rete, vedere [Creazione o modifica delle route delle aree di rete](lync-server-2013-creating-or-modifying-network-region-routes.md).

## Per visualizzare informazioni sulle route area di rete nel Pannello di controllo di Lync Server

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Configurazione di rete**, quindi su **Route area**.

4.  Nella pagina **Route area** fare clic sulla route area che si vuole visualizzare.
    

    > [!NOTE]
    > È possibile visualizzare una sola route area per volta.



5.  Scegliere **Mostra dettagli** dal menu **Modifica**.

## Visualizzazione delle informazioni sulle route area di rete mediante i cmdlet di Lync Server PowerShell

Le informazioni sulle route area di rete possono essere visualizzate usando Lync Server PowerShell e il cmdlet Get-CsNetworkInterRegionRoute. Quest'ultimo può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Visualizzazione delle informazioni sulle route area di rete

  - Per visualizzare tutte le informazioni sulle route area di rete, digitare il comando seguente in Lync Server Management Shell e premere INVIO:
    
        Get-CsNetworkInterRegionRoute
    
    Verranno restituite informazioni simili a queste:
    
        Identity                  : TransAmericaRoute
        NetworkRegionLinks        : {NorthwestToNortheast}
        InterNetworkRegionRouteID : TransAmericaRoute
        NetworkRegionID1          : Pacific Northwest
        NetworkRegionID2          : Northeast

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Get-CsNetworkInterRegionRoute](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkInterRegionRoute).

## Vedere anche

#### Attività

[Creazione o modifica delle route delle aree di rete](lync-server-2013-creating-or-modifying-network-region-routes.md)  
[Eliminazione delle route delle aree di rete esistenti](lync-server-2013-deleting-existing-network-region-routes.md)

