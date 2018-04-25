---
title: 'Lync Server 2013: Richiedere certificati in anticipo (facoltativo)'
TOCTitle: Richiedere certificati in anticipo (facoltativo)
ms:assetid: 9d6d7de6-ff2a-46da-b1b7-a354c8e383e4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412733(v=OCS.15)
ms:contentKeyID: 49301468
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Richiedere certificati in anticipo (facoltativo) per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

I certificati sono necessari per tutti i server interni che eseguono Lync Server 2013, inclusi ogni Enterprise EditionFront End Server, server Standard Edition, Server Director, server perimetrale e Mediation Server autonomo. Sebbene sia consigliata un'autorità di certificazione (CA) enterprise interna per i server interni, è anche possibile usare una CA pubblica. Per informazioni dettagliate sui requisiti dei certificati e sull'uso di una CA pubblica, vedere [Requisiti dei certificati per i server interni in Lync Server 2013](lync-server-2013-certificate-requirements-for-internal-servers.md) nella documentazione sulla pianificazione.

Il programma di installazione di Lync Server 2013 include la Configurazione guidata certificati, che semplifica le attività di richiesta, assegnazione e installazione dei certificati durante la distribuzione. Se si desidera richiedere i certificati prima di installare i server, ad esempio per risparmiare tempo durante l'effettiva distribuzione dei server, è possibile utilizzare a questo scopo un computer in cui siano installati gli strumenti di amministrazione di Lync Server 2013. In alternativa è possibile utilizzare una procedura di richiesta dei certificati definita dall'organizzazione, verificando che i certificati siano esportabili e contengano tutti i nomi alternativi del soggetto necessari. La richiesta anticipata dei certificati è facoltativa. Se non vengono richiesti in anticipo, sarà necessario richiederli nell'ambito dell'installazione di ogni server che richiede un certificato.

La presente documentazione relativa alla distribuzione contiene le procedure per l'utilizzo della Configurazione guidata certificati nell'ambito del processo di installazione, come descritto nelle sezioni [Configurare i certificati per i server in Lync Server 2013](lync-server-2013-configure-certificates-for-servers.md), [Configurare i certificati per il server Director in Lync Server 2013](lync-server-2013-configure-certificates-for-the-director.md), and [Installare i file per Mediation Server in Lync Server 2013](lync-server-2013-install-the-files-for-mediation-server.md). Se si richiedono i certificati in anticipo, è necessario modificare le procedure di distribuzione dei certificati illustrate in tali sezioni in modo da poter importare e assegnare i certificati anziché richiederli al momento della distribuzione.


> [!NOTE]
> Lync Server 2013 include il supporto per i certificati SHA-256 per le connessioni da client che eseguono i sistemi operativi Windows Vista, Windows Server&nbsp;2008, Windows Server&nbsp;2008&nbsp;R2, Windows 7 e Lync Phone Edition. Per supportare l'accesso esterno mediante SHA-256, il certificato esterno viene rilasciato da una CA pubblica mediante SHA-256.


