---
title: Restituire informazioni sulla configurazione di A/V Edge Server
TOCTitle: Restituire informazioni sulla configurazione di A/V Edge Server
ms:assetid: b041f5a4-2387-4075-846c-ec4f99640903
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721850(v=OCS.15)
ms:contentKeyID: 49887708
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Restituire informazioni sulla configurazione di A/V Edge Server

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Il servizio A/V Edge consente agli utenti interni, ovvero agli utenti connessi alla rete dell'organizzazione, di condividere audio e video con utenti esterni, che non sono connessi alla rete dell'organizzazione. Il servizio A/V Edge viene gestito principalmente mediante l'utilizzo di impostazioni di configurazione A/V Edge, che possono essere configurate nell'ambito del sito o del servizio, ovvero possono essere configurate per un singolo A/V Edge Server.

Per restituire informazioni sulle impostazioni di configurazione A/V Edge in uso nell'organizzazione, è necessario utilizzare Lync Server Management Shell e il cmdlet Get-CsAVEdgeConfiguration. Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Get-CsAVEdgeConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Get-CsAVEdgeConfiguration).

Le informazioni restituite dal cmdlet Get-CsAVEdgeConfiguration saranno simili alle seguenti:

    Identity              : Global
    MaxTokenLifetime      : 08:00:00
    MaxBandwidthPerUserKb : 10000
    MaxBandwidthPerPortKb : 3000

## Restituzione delle informazioni relative a tutte le impostazioni di configurazione A/V Edge

  - Il comando seguente restituisce informazioni su tutte le impostazioni di configurazione A/V Edge attualmente in uso nell'organizzazione:
    
        Get-CsAVEdgeConfiguration

## Restituzione delle informazioni relative alle impostazioni di configurazione A/V Edge con il sito come ambito

  - Per restituire informazioni su una raccolta specifica di impostazioni di configurazione A/V Edge, specificare l'identità (Identity) di tale raccolta quando si esegue il cmdlet Get-CsAVEdgeConfiguration. Questo comando ad esempio restituisce informazioni solo sulle impostazioni applicate al sito Redmond:
    
        Get-CsAVEdgeConfiguration -Identity "site:Redmond"

## Restituzione delle informazioni relative alle impostazioni di configurazione A/V Edge con il servizio come ambito

  - Questo comando restituisce informazioni solo sulle impostazioni applicate a un A/V Edge Server specifico:
    
        Get-CsAVEdgeConfiguration -Identity "service:EdgeServer:atl-edge-001.litwareinc.com"

## Vedere anche

#### Attività

[Creare o modificare una raccolta di impostazioni di configurazione di A/V Edge Server](lync-server-2013-create-or-modify-a-collection-of-a-v-edge-server-configuration-settings.md)  
[Eliminare una raccolta esistente di impostazioni di configurazione di A/V Edge Server.](lync-server-2013-delete-an-existing-collection-of-a-v-edge-server-configuration-settings.md)  

#### Ulteriori risorse

[Audio/Video (A/V) Edge Server in Lync Server 2013](lync-server-2013-audio-video-a-v-edge-servers.md)

