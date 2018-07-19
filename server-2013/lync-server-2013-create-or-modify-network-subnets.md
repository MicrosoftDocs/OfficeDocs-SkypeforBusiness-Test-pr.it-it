---
title: Creare o modificare subnet di rete
TOCTitle: Creare o modificare subnet di rete
ms:assetid: 1ba8c4e3-fbc7-4758-88ac-d651fef17bed
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520957(v=OCS.15)
ms:contentKeyID: 49299845
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare subnet di rete

 

_**Ultima modifica dell'argomento:** 2013-02-21_

Una subnet di rete deve essere associata a un sito di rete per la determinazione della posizione geografica dell'host appartenente alla subnet. È possibile utilizzare il Pannello di controllo di Lync Server per configurare le subnet. Dal Pannello di controllo di Lync Server è infatti possibile creare, modificare o eliminare una subnet di rete. Per informazioni sull'eliminazione delle subnet di rete, vedere [Eliminazione di subnet di rete](lync-server-2013-deleting-network-subnets.md)

Nella maggior parte delle distribuzioni di Microsoft Lync Server 2013 in cui è implementato il controllo di ammissione di chiamata (CAC) generalmente sarà presente un numero elevato di subnet. Di conseguenza, spesso è consigliabile configurare le subnet tramite Lync Server Management Shell, da cui è possibile chiamare **New-CsNetworkSubnet** insieme al cmdlet **Import-CSV** di Windows PowerShell. L'utilizzo congiunto di questi due cmdlet consente di leggere le impostazioni delle subnet da un file con valori delimitati da virgole (con estensione csv) e di creare più subnet contemporaneamente. Per alcuni esempi di come creare subnet da un file csv, vedere [New-CsNetworkSubnet](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkSubnet).

## Per creare una subnet di rete

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Subnet**.

4.  Nella pagina **Subnet** fare clic su **Nuovo**.

5.  In **Nuova subnet** immettere un valore nel campo **ID subnet**. Questo valore deve essere il primo indirizzo IP (ad esempio, 174.11.12.0) dell'intervallo di indirizzi IP definito dalla subnet.

6.  Nel campo **Maschera** immettere un valore numerico compreso tra 1 e 32.
    

    > [!NOTE]
    > Questo valore corrisponde alla maschera di bit da applicare alla subnet da creare.



7.  In **ID sito di rete** selezionare il sito a cui appartiene la subnet.

8.  (Facoltativo) Digitare un valore nel campo **Descrizione** per fornire ulteriori informazioni sulla subnet che non possono essere espresse dal solo nome.

9.  Fare clic su **Commit**.

## Per modificare una subnet di rete

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Subnet**.

4.  Nella pagina **Subnet** fare clic sulla subnet che si desidera modificare.

5.  Scegliere **Mostra dettagli** dal menu **Modifica**.

6.  Nella pagina **Modifica Subnet** è possibile modificare la maschera di bit, il sito di rete associato o la descrizione. Se si modifica la maschera di bit, tenere presente che l'ID subnet deve essere comunque il primo indirizzo IP dell'intervallo di indirizzi IP definito dalla subnet.

7.  Fare clic su **Commit**.

## Vedere anche

#### Attività

[Eliminazione di subnet di rete](lync-server-2013-deleting-network-subnets.md)  

#### Concetti

[Informazioni su aree di rete, siti e subnet in Lync Server 2013](lync-server-2013-about-network-regions-sites-and-subnets.md)  

#### Ulteriori risorse

[New-CsNetworkSubnet](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkSubnet)  
[Set-CsNetworkSubnet](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsNetworkSubnet)  
[Remove-CsNetworkSubnet](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsNetworkSubnet)  
[Get-CsNetworkSubnet](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkSubnet)

