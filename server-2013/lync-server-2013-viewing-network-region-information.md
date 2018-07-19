---
title: Visualizzazione delle informazioni sulle aree di rete
TOCTitle: Visualizzazione delle informazioni sulle aree di rete
ms:assetid: 665740d0-a3ed-460f-8337-5ed945f90589
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688076(v=OCS.15)
ms:contentKeyID: 49887587
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzazione delle informazioni sulle aree di rete

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Un'area di rete collega diverse parti di una rete dislocate su diverse aree geografiche. Ogni area di rete deve essere associata a un sito centrale. Il sito centrale è il sito del centro dati in cui è in esecuzione il servizio dei criteri della larghezza di banda Controllo di ammissione di chiamata. È possibile utilizzare il Pannello di controllo di Lync Server per visualizzare le aree di rete. Per le aree di rete sono disponibili impostazioni che determinano se sono consentiti percorsi alternativi attraverso Internet per le connessioni audio e video. Le informazioni in questo argomento descrivono come visualizzare le aree di rete esistenti. Per informazioni dettagliate sulla creazione o la modifica delle aree di rete, vedere [Creazione o modifica delle aree di rete](lync-server-2013-creating-or-modifying-network-regions.md).

## Per visualizzare informazioni su un'area di rete con il Pannello di controllo di Lync Server

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Area**.

4.  Nella pagina **Area** fare clic sull'area che si desidera visualizzare.
    

    > [!NOTE]
    > È possibile visualizzare una sola area alla volta.



5.  Scegliere **Mostra dettagli** dal menu **Modifica**.

## Visualizzazione delle informazioni sulle aree di rete tramite i cmdlet Windows PowerShell

Per visualizzare informazioni sulle aree di rete, è possibile utilizzare Windows PowerShell e il cmdlet **Get-CsNetworkRegion**. È possibile eseguire questo cmdlet da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per visualizzare informazioni sulle aree di rete

  - Per visualizzare informazioni su tutte le aree di rete, digitare il comando seguente in Lync Server Management Shell e quindi premere INVIO:
    
        Get-CsNetworkRegion
    
    Verranno restituite informazioni simili alle seguenti:
    
        Identity         : Pacific Northwest
        Description      :
        BypassID         : 3b232b84-2c1d-4da2-8181-e9330bafebe9
        CentralSite      : Site:Redmond1
        BWAlternatePaths : {BWPolicyModality=Audio;AlternatePath=True, 
                           BWPolicyModality=Video;AlternatePath=True}
        NetworkRegionID  : Pacific Northwest

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Get-CsNetworkRegion](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsNetworkRegionLink).

## Vedere anche

#### Attività

[Creazione o modifica delle aree di rete](lync-server-2013-creating-or-modifying-network-regions.md)  
[Eliminazione delle aree di rete esistenti](lync-server-2013-deleting-existing-network-regions.md)

