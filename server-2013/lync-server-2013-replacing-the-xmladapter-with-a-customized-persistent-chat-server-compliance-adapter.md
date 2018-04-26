---
title: Sostituzione di XmlAdapter con un adattatore conformità del server chat persistente personalizzato in Lync Server 2013
TOCTitle: Sostituzione di XmlAdapter con un adattatore conformità del server chat persistente personalizzato in Lync Server 2013
ms:assetid: 2cb70db2-663f-40a6-abcf-89ea7d4a8b65
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ680106(v=OCS.15)
ms:contentKeyID: 49887496
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Sostituzione di XmlAdapter con un adattatore conformità del server chat persistente personalizzato in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

È possibile scrivere un adattatore personalizzato anziché usare l'adattatore XmlAdapter installato con server Chat persistente. A questo scopo, è necessario specificare un assembly .NET Framework contenente una classe pubblica che implementa l'interfaccia **IComplianceAdapter** e posizionarlo nella cartella di installazione di server Chat persistente di ogni server nel pool di server Chat persistente. Ciascun Compliance Server può fornire dati di conformità all'adattatore, ma non fornirà dati di conformità duplicati a più istanze dell'adattatore.

## Implementazione dell'interfaccia IComplianceAdapter

L'interfaccia è definita nell'assembly Compliance.dll nello spazio dei nomi `Microsoft.Rtc.Internal.Chat.Server.Compliance` e definisce due metodi che l'adattatore personalizzato deve implementare.

    void SetConfig(AdapterConfig config)

Il Compliance Server Chat persistente chiamerà questo metodo al primo caricamento dell'adattatore. `AdapterConfig` contiene la configurazione di conformità di Chat persistente rilevante per l'adattatore di conformità.

    void Translate(ConversationCollection conversations)

Il Compliance Server Chat persistente chiama questo metodo a intervalli periodici se esistono nuovi dati da convertire. Questo intervallo temporale equivale al `RunInterval` impostato nella configurazione di conformità di Chat persistente.

`ConversationCollection` contiene informazioni sulla conversazione raccolte dopo l'ultima chiamata a questo metodo.

