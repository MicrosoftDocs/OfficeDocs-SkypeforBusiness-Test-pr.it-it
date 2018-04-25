---
title: Eliminare una raccolta esistente di impostazioni di configurazione di A/V Edge Server.
TOCTitle: Eliminare una raccolta esistente di impostazioni di configurazione di A/V Edge Server.
ms:assetid: 668d3613-e464-4b68-967a-cfff90b9ce4b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688077(v=OCS.15)
ms:contentKeyID: 49887588
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminare una raccolta esistente di impostazioni di configurazione di A/V Edge Server.

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Il servizio A/V Edge consente agli utenti interni, ovvero gli utenti connessi alla rete dell'organizzazione, di condividere audio e video con gli utenti esterni, ovvero gli utenti non connessi alla rete dell'organizzazione. Il servizio A/V Edge viene gestito principalmente tramite le impostazioni di configurazione di A/V Edge, configurabili con ambito sito o con ambito servizio, ovvero per un singolo server A/V Edge.

Quando si installa Lync Server, viene creata automaticamente una raccolta globale di impostazioni di configurazione del servizio A/V Edge. Questa raccolta globale non può essere eliminata. È comunque possibile utilizzare Lync Server Management Shell e il cmdlet Remove-CsAVEdgeConfiguration per "reimpostare" tale raccolta, ovvero ripristinare i valori predefiniti per tutti i valori di proprietà nella raccolta globale. Se la proprietà MaxTokenLifetime è impostata su 16 ore, ad esempio, con l'esecuzione del cmdlet verrebbe ripristinato il valore predefinito di 8 ore.

È comunque possibile utilizzare il cmdlet Remove-CsAVEdgeConfiguration per eliminare le raccolte di impostazioni personalizzate create con ambito sito o con ambito servizio. Se si eliminano le impostazioni a livello di sito, i server A/V Edge in tale sito verranno gestiti dalle impostazioni globali. Se si eliminano le impostazioni con ambito servizio, il server verrà gestito dalle impostazioni a livello sito, se esistenti, o dalle impostazioni globali se non sono disponibili impostazioni a livello di sito.

Per ulteriori informazioni, vedere l'argomento della guida relativo al cmdlet [Remove-CsAVEdgeConfiguration](remove-csavedgeconfiguration.md).

## Reimpostazione della raccolta globale

  - Il comando seguente consente di reimpostare la raccolta globale delle impostazioni di configurazione di A/V Edge:
    
        Remove-CsAVEdgeConfiguration -Identity "global"

## Rimozione di una raccolta dall'ambito sito

  - Questo comando consente di rimuovere le impostazioni di configurazione di A/V Edge applicate al sito Redmond:
    
        Remove-CsAVEdgeConfiguration -Identity "site:Redmond"

## Rimozione di una raccolta dall'ambito servizio

  - Questo comando consente di rimuovere le impostazioni applicate al server A/V Edge atl-edge-001.litwareinc.com:
    
        Remove-CsAVEdgeConfiguration -Identity "service:EdgeServer:atl-edge-001.litwareinc.com"

## Vedere anche

#### Attività

[Restituire informazioni sulla configurazione di A/V Edge Server](lync-server-2013-return-a-v-edge-server-configuration-information.md)  
[Creare o modificare una raccolta di impostazioni di configurazione di A/V Edge Server](lync-server-2013-create-or-modify-a-collection-of-a-v-edge-server-configuration-settings.md)  

#### Ulteriori risorse

[Audio/Video (A/V) Edge Server in Lync Server 2013](lync-server-2013-audio-video-a-v-edge-servers.md)  
[Remove-CsAVEdgeConfiguration](remove-csavedgeconfiguration.md)

