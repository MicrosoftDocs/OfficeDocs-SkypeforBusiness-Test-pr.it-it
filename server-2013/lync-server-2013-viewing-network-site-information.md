---
title: Visualizzazione delle informazioni sul sito di rete
TOCTitle: Visualizzazione delle informazioni sul sito di rete
ms:assetid: 24a97d98-b168-4016-81bf-c2c478092b87
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ687996(v=OCS.15)
ms:contentKeyID: 49887479
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Visualizzazione delle informazioni sul sito di rete

 

_**Ultima modifica dell'argomento:** 2013-02-23_

I siti di rete sono gli uffici o le postazioni configurate in ogni area di una distribuzione del servizio Controllo di ammissione di chiamata (CAC) o del servizio per chiamate di emergenza Enhanced 9-1-1. È possibile visualizzare le informazioni sui siti di rete nel Pannello di controllo di Lync Server 2013 o in Lync Server Management Shell. Per informazioni sulla creazione o la modifica di siti di rete, vedere [Creazione o modifica dei siti di rete](lync-server-2013-creating-or-modifying-network-sites.md).

## Per visualizzare informazioni sui siti di rete nel Pannello di controllo di Lync Server

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Sito**.

4.  Nella pagina **Sito** fare clic sul sito che si desidera visualizzare.
    

    > [!NOTE]
    > È possibile visualizzare informazioni per un solo sito alla volta.



5.  Scegliere **Mostra dettagli** dal menu **Modifica**.

## Per visualizzare informazioni sui siti di rete tramite i cmdlet di Lync Server Management Shell

È possibile visualizzare informazioni sui siti di rete tramite il cmdlet Get-CsNetworkSite, che è possibile eseguire da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per visualizzare informazioni sui siti di rete

  - Per visualizzare informazioni su tutti i siti di rete, digitare il comando seguente in Lync Server Management Shell e premere INVIO:
    
        Get-CsNetworkSite
    
    Verranno restituite informazioni simili alle seguenti:
    
        Identity          : Redmond
        NetworkSiteID     : Redmond
        Description       :
        NetworkRegionID   : Pacific Northwest
        BypassID          : 3b232b84-2c1d-4da2-8181-e9330bafebe9
        BWPolicyProfileID :
        LocationPolicy    :

Per ulteriori informazioni, vedere l'argomento della guida relativo al cmdlet [Get-CsNetworkSite](get-csnetworksite.md).

## Vedere anche

#### Attività

[Creazione o modifica dei siti di rete](lync-server-2013-creating-or-modifying-network-sites.md)  
[Eliminazione di un sito di rete esistente](lync-server-2013-deleting-an-existing-network-site.md)

