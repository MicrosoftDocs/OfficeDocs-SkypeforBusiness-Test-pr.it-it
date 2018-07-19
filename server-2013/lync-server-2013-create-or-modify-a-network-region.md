---
title: "Lync Server 2013: Creare o modificare un'area di rete"
TOCTitle: Creare o modificare un'area di rete
ms:assetid: bf7a3dc4-71a2-4559-a547-d90305d4f904
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412933(v=OCS.15)
ms:contentKeyID: 49301848
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare un'area di rete in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-19_

Le *aree di rete* sono gli hub di rete o backbone utilizzati nella configurazione del servizio Controllo di ammissione di chiamata, dei servizi chiamate di emergenza (E9-1-1) e di bypass multimediale. Utilizzare le procedure descritte di seguito per creare o modificare la aree di rete. Se ad esempio sono state già create aree di rete per una funzionalità vocale, non è necessario creare nuove aree. Le altre funzionalità di VoIP aziendale avanzate utilizzeranno le stesse aree di rete. Potrebbe essere necessario tuttavia modificare la definizione di un'area di rete esistente in modo da applicare impostazione specifiche della funzionalità. Se ad esempio sono state create aree di rete per i servizi chiamate di emergenza E9-1-1 (che non richiedono un sito centrale associato) e successivamente si distribuisce il servizio Controllo di ammissione di chiamata, sarà necessario modificare le definizione delle aree di rete per specificare un sito centrale. Per informazioni dettagliate, vedere [Configurare le aree di rete per il servizio Controllo di ammissione di chiamata](lync-server-2013-configure-network-regions-for-cac.md).


> [!NOTE]
> Tutti i requisiti specifici per particolari funzionalità per le definizioni delle aree di rete sono documentati negli argomenti relativi alla distribuzione per la funzionalità.



Per informazioni dettagliate sull'utilizzo delle aree di rete, vedere la documentazione di Lync Server Management Shell per i cmdlet seguenti:

  - [New-CsNetworkRegion](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsNetworkRegion)

  - [Get-CsNetworkRegion](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkRegionLink)

  - [Set-CsNetworkRegion](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsNetworkRegion)

  - [Remove-CsNetworkRegion](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsNetworkRegion)

## Creare un'area di rete

Creare un'area di rete utilizzabile dal controllo di ammissione di chiamata, E9-1-1 o il bypass multimediale.

## Per creare un'area di rete tramite Lync Server Management Shell

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il cmdlet New-CsNetworkRegion per creare le aree di rete:
    
        New-CsNetworkRegion -Identity <String> -CentralSite <String>
    
    Ad esempio:
    
        New-CsNetworkRegion -Identity NorthAmerica -CentralSite CHICAGO -Description "All North America Locations"
    
    Con questo esempio viene creata un'area di rete denominata “NorthAmerica” associata a un sito centrale con ID di sito CHICAGO.

3.  Per completare la creazione delle aree di rete per la topologia, ripetere il passaggio 2 con le impostazioni per ogni area di rete.

## Per creare un'area di rete mediante il Pannello di controllo di Lync Server

1.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

2.  Sulla barra di spostamento sinistra fare clic su **Configurazione di rete** .

3.  Fare clic su **Area** .

4.  Fare clic su **Nuovo** .

5.  Nella pagina **Nuova area** fare clic su **Nome** e quindi digitare un nome per l'area di rete.

6.  Fare clic su **Sito centrale** e quindi fare clic su un sito centrale nell'elenco.

7.  Facoltativamente, fare clic su **Descrizione** e quindi digitare ulteriori informazioni per descrivere il sito di rete.

8.  Fare clic su **Commit** .

9.  Per completare la creazione delle aree di rete per la topologia, ripetere i passaggi da 4 a 8 con le impostazioni per le altre aree.

## Modificare un'area di rete

È possibile modificare le impostazioni per un'area di rete esistente per adattarle a modifiche delle informazioni di base sull'area o a modifiche rese necessarie da una nuova funzionalità.

## Per modificare un'area di rete tramite Lync Server Management Shell

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il cmdlet Set-CsNetworkRegion per modificare un'area di rete esistente:
    
        Set-CsNetworkRegion -Identity <String> -CentralSite <String>
    
    Ad esempio:
    
        Set-CsNetworkRegion -Identity NorthAmerica -CentralSite CHICAGO -Description "North American Region"
    
    Con questo esempio si modifica un'area di rete esistente denominata “NorthAmerica” (creata con le procedure descritte in precedenza in questo argomento) modificandone la descrizione. Se per l'area “NorthAmerica” esiste già una descrizione, questo comando la sostituisce con il valore specificato. Se non è mai stata impostata una descrizione, con questo comando viene aggiunta.

3.  Per modificare altre aree di rete, ripetere il passaggio 2 con le impostazioni per le altre aree.

## Per modificare un'area di rete mediante il Pannello di controllo di Lync Server

1.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

2.  Sulla barra di spostamento sinistra fare clic su **Configurazione di rete** .

3.  Fare clic sul pulsante di spostamento **Area** .

4.  Nella tabella fare clic sull'area di rete che si desidera modificare.

5.  Fare clic su **Modifica** e quindi su **Mostra dettagli** .

6.  Nella pagina **Modifica area** modificare i valori per le impostazioni dell'area di rete in base alle esigenze.

7.  Fare clic su **Commit** .

8.  Per completare la modifica delle aree di rete, ripetere i passaggi da 4 a 7 con le impostazioni per le altre aree.

