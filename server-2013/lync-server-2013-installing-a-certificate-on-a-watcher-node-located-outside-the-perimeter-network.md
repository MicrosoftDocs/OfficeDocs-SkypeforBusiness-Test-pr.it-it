---
title: "Lync Server 2013: Installa certificato in nodo Watcher fuori perimetro rete"
TOCTitle: "Lync Server 2013: Installa certificato in nodo Watcher fuori perimetro rete"
ms:assetid: 825c9c02-1951-4d7a-a25e-a313a85333f8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688113(v=OCS.15)
ms:contentKeyID: 49887631
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Installazione di un certificato in un nodo Watcher posizionato all'esterno del perimetro della rete

 

_**Ultima modifica dell'argomento:** 2012-10-22_

Gli agenti di System Center Operations Manager eseguiti nella rete perimetrale (ad esempio, un server perimetrale di Lync Server), all'esterno dell'azienda (come un nodo esterno di controllo della transazione sintetica) o entro confini di trust di Servizi di dominio Active Directory potrebbero richiedere la configurazione di un server gateway di System Center Operations Manager. Questo ruolo del server consente agli agenti che non dispongono di una relazione di trust con il server di gestione principale di emettere avvisi. Per informazioni dettagliate, vedere "Gestione dei server gateway in Operations Manager 2007" in System Center Operations Manager TechNet Library all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268703\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268703%26clcid=0x410).

Se si distribuisce un agente in una di queste posizioni, sarà necessario richiedere e configurare un certificato che consenta al nodo di controllo di inviare avvisi a System Center Operations Manager. Per semplificare questo processo, il team di Operations Manager ha creato un set di utilità che consente di richiedere e installare il tipo di certificato corretto nel computer del nodo di controllo. Per informazioni dettagliate e per scaricare queste utilità, vedere l'articolo del blog relativo alla procedura guidata per la generazione di certificati per agenti uniti non di dominio all'indirizzo [http://go.microsoft.com/fwlink/?linkid=267421\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=267421%26clcid=0x410).

