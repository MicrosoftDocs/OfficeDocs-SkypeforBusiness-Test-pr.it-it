---
title: 'Lync Server 2013: Creare o modificare un sito di rete'
TOCTitle: Creare o modificare un sito di rete
ms:assetid: 14e24856-9996-4da4-9f31-300940bdf5aa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398218(v=OCS.15)
ms:contentKeyID: 49299772
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare un sito di rete in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-24_

Le distribuzioni del servizio Controllo di ammissione di chiamata, dei servizi di emergenza e del bypass multimediale sono basate sulla configurazione dei *siti di rete* definiti all'interno e sempre associati a un'area di rete. Un sito di rete rappresenta una succursale, un insieme di edifici o un campus universitario. I siti di rete rappresentano insiemi di subnet con larghezza di banda analoga.

Eseguire le procedure seguenti per creare o modificare siti di rete. Se ad esempio sono già stati creati siti di rete per una funzionalità vocale, non è necessario crearne di nuovi. Per le altre funzionalità vocali verranno utilizzati gli stessi siti. Potrebbe tuttavia essere necessario modificare la definizione di un sito di rete esistente per applicare le impostazioni specifiche di una funzionalità. Se ad esempio è stato creato un sito di rete per il servizio E9-1-1, sarà necessario modificarlo durante la distribuzione del controllo di ammissione di chiamata per applicare un profilo criteri larghezza di banda.


> [!NOTE]
> Nella documentazione di distribuzione relativa a ogni funzionalità sono disponibili, se applicabili, esempi e requisiti specifici per i siti di rete per una funzionalità vocale avanzata: 
> <UL>
> <LI>
> <P><A href="lync-server-2013-configure-network-sites-for-cac.md">Configurare siti di rete per il servizio Controllo di ammissione di chiamata in Lync Server 2013</A></P></LI></UL>



Per informazioni dettagliate sull'utilizzo dei siti di rete, vedere nella documentazione relativa a Lync Server Management Shell i cmdlet seguenti:

  - [New-CsNetworkSite](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkSite)

  - [Get-CsNetworkSite](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkSite)

  - [Set-CsNetworkSite](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsNetworkSite)

  - [Remove-CsNetworkSite](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsNetworkSite)

## Creare un sito di rete

Creare un'area di rete utilizzabile dal controllo di ammissione di chiamata, E9-1-1 o il bypass multimediale.

## Per creare un sito di rete utilizzando Management Shell

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il cmdlet New-CsNetworkSite per creare i siti di rete:
    
        New-CsNetworkSite -NetworkSiteID <string>
    
    Ad esempio:
    
        New-CsNetworkSite -NetworkSiteID Chicago -Description "Corporate headquarters"-NetworkRegionID NorthAmerica
    
    In questo esempio è stato creato un sito di rete denominato "Chicago" contenuto nell'area di rete "NorthAmerica".
    

    > [!NOTE]
    > Per il corretto funzionamento di questo comando, l'area di rete NorthAmerica deve esistere già.



3.  Per completare la creazione dei siti di rete per la propria topologia, ripetere il passaggio 2 con le impostazioni relative agli altri siti.

## Per creare un sito di rete utilizzando il Pannello di controllo di Lync Server

1.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

2.  Sulla barra di spostamento sinistra fare clic su **Configurazione di rete** .

3.  Fare clic sul pulsante di spostamento **Sito** .

4.  Fare clic su **Nuovo** .

5.  Nella pagina **Nuovo sito** fare clic su **Nome** e quindi digitare un nome per il sito di rete.

6.  Fare clic su **Area** e quindi selezionare un'area nell'elenco.

7.  Facoltativamente, fare clic su **Criteri larghezza di banda** e quindi selezionare un criterio larghezza di banda nell'elenco.
    

    > [!NOTE]
    > Il criterio larghezza di banda è necessario solo se nel sito viene distribuito il controllo di ammissione di chiamata.



8.  Facoltativamente, fare clic su **Criteri percorso** e quindi selezionare un criterio percorso nell'elenco.
    

    > [!NOTE]
    > Il criterio percorso è necessario solo se nel sito viene distribuito il servizio E9-1-1.



9.  Facoltativamente, fare clic su **Descrizione** e quindi digitare ulteriori informazioni per descrivere il sito di rete.

10. Fare clic su **Commit** .

11. Per completare la creazione dei siti di rete per la propria topologia, ripetere i passaggi da 4 a 10 con le impostazioni relative agli altri siti.

## Modificare un sito di rete

Modificare un'area di rete utilizzabile dal controllo di ammissione di chiamata, dal servizio E9-1-1 o dal bypass multimediale.

## Per modificare un sito di rete

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il cmdlet Set-CsNetworkSite per modificare i siti di rete:
    
        Set-CsNetworkSite -Identity <string>
    
    Ad esempio:
    
        Set-CsNetworkSite -Identity Albuquerque -NetworkRegionID NorthAmerica
    
    In questo esempio il sito denominato "Albuquerque" viene spostato nell'area di rete "NorthAmerica". Per modificare la configurazione del sito di rete in modo da distribuire il controllo di ammissione di chiamata, il servizio E9-1-1 o il bypass multimediale, modificare le impostazioni del sito di rete eseguendo il cmdlet Set-CsNetworkSite rispettivamente con il parametro BWPolicyProfileID o LocationPolicy.
    

    > [!NOTE]
    > Anche se per il bypass multimediale esiste il parametro BypassID, è consigliabile non sostituire gli ID bypass generati automaticamente. Non è necessario specificare ulteriori parametri per configurare un sito di rete per il bypass multimediale.



3.  Per completare la modifica dei siti di rete per la propria topologia, ripetere il passaggio 2 con le impostazioni relative agli altri siti.

## Per modificare un sito di rete utilizzando il Pannello di controllo di Lync Server

1.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

2.  Sulla barra di spostamento sinistra fare clic su **Configurazione di rete** .

3.  Fare clic sul pulsante di spostamento **Sito** .

4.  Nella tabella fare clic sul sito di rete che si desidera modificare.

5.  Fare clic su **Modifica** e quindi su **Mostra dettagli...** .

6.  Nella pagina **Modifica sito** modificare i valori relativi alle impostazioni del sito di rete in base alle proprie esigenze.

7.  Fare clic su **Commit** .

8.  Per completare la modifica dei siti di rete, ripetere i passaggi da 4 a 7 con le impostazioni relative agli altri siti.

