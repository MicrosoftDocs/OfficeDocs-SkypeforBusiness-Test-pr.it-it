---
title: Creazione o modifica delle aree di rete
TOCTitle: Creazione o modifica delle aree di rete
ms:assetid: bd08bb66-5976-4ece-b45c-7de19569f814
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg182579(v=OCS.15)
ms:contentKeyID: 49301819
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creazione o modifica delle aree di rete

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Un'area di rete interconnette diverse parti di una rete dislocate su più aree geografiche. Ogni area di rete deve essere associata a un sito centrale. Il sito centrale è il sito del data center in cui è in esecuzione il servizio dei criteri di larghezza di banda del controllo di ammissione di chiamata. È possibile utilizzare il Pannello di controllo di Lync Server per configurare le aree di rete. Queste includono impostazioni che determinano se consentire percorsi alternativi Internet per le connessioni audio e video. Dal Pannello di controllo di Lync Server è possibile creare, modificare o eliminare un'area di rete. Utilizzare questo argomento per creare e modificare le aree di rete. Per informazioni dettagliate sull'eliminazione di aree di rete esistenti, vedere [Eliminazione delle aree di rete esistenti](lync-server-2013-deleting-existing-network-regions.md).

## Per creare un'area di rete

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Area**.

4.  Nella pagina **Area** fare clic su **Nuovo**.

5.  Nella pagina **Nuova area** digitare un valore nel campo **Nome**. Questo valore deve essere univoco nella distribuzione di Microsoft Lync Server 2013.

6.  Nell'elenco a discesa **Sito centrale** selezionare il sito centrale per questa area di rete.

7.  La casella di controllo **Abilita percorso alternativo audio** è selezionata per impostazione predefinita. Questo campo determina se le chiamate audio verranno instradate tramite un percorso alternativo se non è disponibile una larghezza di banda adeguata nel percorso principale. Deselezionare questa casella di controllo solo se è necessario disattivare l'offload su Internet. Se alcune delle chiamate vengono effettuate via Internet, questa casella di controllo deve essere selezionata, indipendentemente dalle impostazioni della larghezza di banda.

8.  La casella di controllo **Abilita percorso alternativo video** è selezionata per impostazione predefinita. Questo parametro determina se le chiamate video verranno instradate tramite un percorso alternativo se non è disponibile una larghezza di banda adeguata nel percorso principale. Deselezionare questa casella di controllo solo se è necessario disattivare l'offload su Internet. Se alcune delle chiamate vengono effettuate via Internet, questa casella di controllo deve essere selezionata, indipendentemente dalle impostazioni della larghezza di banda.

9.  (Facoltativo) Digitare un valore nel campo **Descrizione** per specificare ulteriori informazioni sull'area che non è possibile fornire solo con il nome.

10. Fare clic su **Commit**.

La tabella **Siti associati** non viene utilizzata per la creazione di un'area di rete. Si associa un sito a un'area durante la creazione o la modifica del sito. Per informazioni dettagliate, vedere [Creazione o modifica dei siti di rete](lync-server-2013-creating-or-modifying-network-sites.md).

## Per modificare un'area di rete

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Area**.

4.  Nella pagina **Area** fare clic sull'area che si desidera modificare.

5.  Scegliere **Mostra dettagli** dal menu **Modifica**.

6.  Nella pagina **Modifica area** è possibile modificare le impostazioni per abilitare e disabilitare i percorsi alternativi per audio e video, nonché modificare la descrizione. Per informazioni dettagliate, vedere la sezione "Per creare un'area di rete" più indietro in questo argomento.

7.  Fare clic su **Commit**.

Non è possibile modificare i **Siti associati** in questa pagina. L'elenco dei siti associati viene fornito per riferimento in modo da sapere quali siti saranno interessati dalla modifica delle impostazioni dell'area.

## Vedere anche

#### Attività

[Eliminazione delle aree di rete esistenti](lync-server-2013-deleting-existing-network-regions.md)  
[Configurare le aree di rete per il servizio Controllo di ammissione di chiamata](lync-server-2013-configure-network-regions-for-cac.md)  

#### Ulteriori risorse

[New-CsNetworkRegion](new-csnetworkregion.md)  
[Set-CsNetworkRegion](set-csnetworkregion.md)  
[Remove-CsNetworkRegion](remove-csnetworkregion.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)

