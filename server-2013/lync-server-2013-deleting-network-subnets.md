---
title: Eliminazione di subnet di rete
TOCTitle: Eliminazione di subnet di rete
ms:assetid: c1850f38-40a3-48c9-b6f1-f181c5e63b6b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721873(v=OCS.15)
ms:contentKeyID: 49887735
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminazione di subnet di rete

 

_**Ultima modifica dell'argomento:** 2013-02-21_

È possibile utilizzare la procedura seguente per eliminare una subnet. Dal Pannello di controllo di Lync Server è infatti possibile creare, modificare o eliminare una subnet di rete. Per informazioni dettagliate sulla creazione o la modifica delle subnet di rete, vedere [Creare o modificare subnet di rete](lync-server-2013-create-or-modify-network-subnets.md).

Nella maggior parte delle distribuzioni di Microsoft Lync Server 2013 in cui è implementato il controllo di ammissione di chiamata (CAC) generalmente sarà presente un numero elevato di subnet. Di conseguenza, spesso è consigliabile configurare le subnet tramite Lync Server Management Shell, da cui è possibile chiamare **New-CsNetworkSubnet** insieme al cmdlet **Import-CSV** di Windows PowerShell. L'utilizzo congiunto di questi due cmdlet consente di leggere le impostazioni delle subnet da un file con valori delimitati da virgole (con estensione csv) e di creare più subnet contemporaneamente. Per alcuni esempi di come creare subnet da un file csv, vedere [New-CsNetworkSubnet](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkSubnet).

## Per eliminare una subnet di rete

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Subnet**.

4.  Nella pagina **Subnet** fare clic sulla subnet che si desidera eliminare.
    

    > [!NOTE]
    > È possibile eliminare più subnet contemporaneamente. A tale scopo, tenere premuto CTRL e selezionare le diverse subnet. In alternativa, per selezionare tutte le subnet, scegliere <STRONG>Seleziona tutto</STRONG> dal menu <STRONG>Modifica</STRONG>.



5.  Scegliere **Elimina** dal menu **Modifica**.

6.  Fare clic su **OK**.

## Vedere anche

#### Attività

[Creare o modificare subnet di rete](lync-server-2013-create-or-modify-network-subnets.md)

