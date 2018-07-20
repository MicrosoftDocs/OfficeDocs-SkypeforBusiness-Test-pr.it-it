---
title: Visualizzazione delle informazioni sulle subnet di rete
TOCTitle: Visualizzazione delle informazioni sulle subnet di rete
ms:assetid: 46f165f2-efe3-4cc1-9fee-a78b7f2ed41e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688044(v=OCS.15)
ms:contentKeyID: 49887542
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzazione delle informazioni sulle subnet di rete

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Per visualizzare una subnet di rete è possibile attenersi alla procedura seguente. Dal Pannello di controllo di Lync Server è possibile creare, modificare o eliminare subnet di rete. Per informazioni dettagliate sulla creazione o sulla modifica delle subnet di rete, vedere [Creare o modificare subnet di rete](lync-server-2013-create-or-modify-network-subnets.md).

## Per visualizzare una subnet di rete

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Subnet**.

4.  Nella pagina **Subnet** fare clic sulla subnet che si desidera visualizzare.
    

    > [!NOTE]
    > È possibile visualizzare una sola subnet alla volta.



5.  Scegliere **Mostra dettagli** dal menu **Modifica**.

## Visualizzazione delle informazioni di configurazione delle subnet di rete tramite i cmdlet di PowerShell per Lync Server

Per visualizzare informazioni sulle subnet, è inoltre possibile utilizzare PowerShell per Lync Server e il cmdlet Get-CsNetworkSubnet. È possibile eseguire questo cmdlet da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Visualizzazione di informazioni sulle subnet

  - Per visualizzare informazioni su tutte le subnet di rete, digitare il comando seguente in Lync Server Management Shell e quindi premere INVIO:
    
        Get-CsNetworkSubnet
    
    Verranno restituite informazioni simili alle seguenti:
    
        Identity      : 172.11.15.0
        MaskBits      : 28
        Description   :
        NetworkSiteID : Redmond
        SubnetID      : 172.11.15.0

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Get-CsNetworkSubnet](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkSubnet).

## Vedere anche

#### Attività

[Creare o modificare subnet di rete](lync-server-2013-create-or-modify-network-subnets.md)  
[Eliminazione di subnet di rete](lync-server-2013-deleting-network-subnets.md)

