---
title: "Lync Server 2013: Crea/modifica configurazione A/V Edge Server"
TOCTitle: "Lync Server 2013: Crea/modifica configurazione A/V Edge Server"
ms:assetid: 43899518-59c6-4be4-8892-d6f6207bfaab
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688039(v=OCS.15)
ms:contentKeyID: 49887539
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare o modificare una raccolta di impostazioni di configurazione di A/V Edge Server

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Il servizio A/V Edge consente agli utenti interni, ovvero gli utenti connessi alla rete dell'organizzazione, di condividere audio e video con gli utenti esterni, ovvero gli utenti non connessi alla rete dell'organizzazione. Il servizio A/V Edge viene gestito principalmente tramite le impostazioni di configurazione di A/V Edge, configurabili nell'ambito del sito o nell'ambito del servizio, ovvero per un singolo server A/V Edge.

Quando si installa Lync Server, viene creata automaticamente una raccolta globale di impostazioni di configurazione di A/V Edge. Inoltre è possibile utilizzare Lync Server Management Shell e il cmdlet New-CsAVEdgeConfiguration per creare nuove impostazioni nell'ambito del sito o nell'ambito del servizio, ovvero per un singolo server A/V Edge. Quando si creano nuove impostazioni, tenere presente quanto segue.

  - Le impostazioni configurate nell'ambito del servizio, ovvero in un singolo server, avranno la precedenza su tutte le altre.

  - Le impostazioni configurate nell'ambito del sito hanno la precedenza su quelle configurate nell'ambito globale. Le impostazioni dell'ambito del servizio hanno tuttavia anche la precedenza rispetto a quelle dell'ambito del sito.

  - Le impostazioni dell'ambito globale vengono utilizzate solo se non sono state configurate impostazioni del servizio nel singolo server e se non sono presenti impostazioni del sito per il sito in cui si trova il server in oggetto.

Tutte le impostazioni possono essere quindi modificate utilizzando il cmdlet Set-CsAVEdgeConfiguration. Per ulteriori informazioni, vedere gli argomenti della Guida relativi ai cmdlet [New-CsAVEdgeConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsAVEdgeConfiguration) e [Set-CsAVEdgeConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsAVEdgeConfiguration).

## Creazione di nuove impostazioni di configurazione di A/V Edge nell'ambito del sito

  - Il comando seguente crea una nuova raccolta di impostazioni di configurazione di A/V Edge per il sito Redmond.
    
        New-CsAVEdgeConfiguration -Identity "site:Redmond"

## Creazione di impostazioni personalizzate di configurazione di A/V Edge nell'ambito del sito

  - Poiché non sono stati inclusi parametri aggiuntivi, queste nuove impostazioni utilizzeranno i valori predefiniti per il servizio A/V Edge. In alternativa, è possibile inserire altri parametri e valori di parametro per creare una raccolta personalizzata. Questo comando imposta ad esempio la proprietà MaxTokenLifetime su 4 ore (04 ore : 00 minuti : 00 secondi):
    
        New-CsAVEdgeConfiguration -Identity "site:Redmond" -MaxTokenLifetime "04:00:00"

## Creazione di impostazioni personalizzate di configurazione di A/V Edge nell'ambito del servizio

  - Questo comando crea una raccolta simile applicata al server A/V Edge atl-edge-001.litwareinc.com:
    
        New-CsAVEdgeConfiguration -Identity "service:EdgeServer:atl-edge-001.litwareinc.com" -MaxTokenLifetime "04:00:00"

## Modifica delle impostazioni di configurazione di A/V Edge

  - In questo esempio il cmdlet Set-CsAVEdgeConfiguration viene utilizzato per modificare in 12 ore la durata massima dei token per il sito Redmond:
    
        Set-CsAVEdgeConfiguration -Identity "site:Redmond" -MaxTokenLifetime "12:00:00"

## Vedere anche

#### Attività

[Restituire informazioni sulla configurazione di A/V Edge Server](lync-server-2013-return-a-v-edge-server-configuration-information.md)  
[Eliminare una raccolta esistente di impostazioni di configurazione di A/V Edge Server.](lync-server-2013-delete-an-existing-collection-of-a-v-edge-server-configuration-settings.md)  

#### Ulteriori risorse

[Audio/Video (A/V) Edge Server in Lync Server 2013](lync-server-2013-audio-video-a-v-edge-servers.md)  
[New-CsAVEdgeConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsAVEdgeConfiguration)  
[Set-CsAVEdgeConfiguration](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsAVEdgeConfiguration)

