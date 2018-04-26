---
title: 'Lync Server 2013: Modifica della progettazione'
TOCTitle: Modifica della progettazione
ms:assetid: 08f639ba-0e5f-4ae7-9191-c3d96c25b169
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558608(v=OCS.15)
ms:contentKeyID: 52062091
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modifica della progettazione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

Dopo avere risposto alle domande iniziali, è possibile modificare il nome di dominio completo (FQDN) e gli indirizzi IP del sito. A tale scopo, nella pagina **Topologia globale** fare doppio clic sul sito che si desidera modificare.

Nello Strumento di pianificazione verrà visualizzata la topologia del sito selezionato. Nella parte inferiore della pagina relativa al sito sono disponibili quattro schede:

![Topologia del sito dello strumento di pianificazione](images/Gg558608.e6189c20-360a-42bd-ba90-11bdb5b7551b(OCS.15).jpg "Topologia del sito dello strumento di pianificazione")

  - Topologia sito - È la pagina attualmente visualizzata e offre una panoramica visiva della topologia consigliata.

  - Diagramma di rete perimetrale - Questa è la pagina in cui il progettista eseguirà la maggior parte del lavoro necessario nello Strumento di pianificazione. Nel diagramma viene visualizzata la configurazione di rete per una topologia di Lync Server 2013 consigliata, con voci modificabili per gli indirizzi IP e gli FQDN dei server, il pool e servizi di bilanciamento del carico sia hardware che DNS (Domain Name System).

  - Rapporto amministratore server perimetrale - Questa scheda è costituita da un totale di quattro rapporti:
    
    ![Pagina del rapporto di amministrazione della rete perimetrale](images/Gg558608.0019cc5e-af39-4cb9-82ce-58f6388242ff(OCS.15).jpg "Pagina del rapporto di amministrazione della rete perimetrale")  
    
      - Rapporto riepilogativo - Si tratta di un rapporto generale sulle impostazioni per la configurazione della rete perimetrale. Se si modificano i valori nella pagina **Diagramma di rete perimetrale** impostando gli indirizzi TCP/IP e gli FQDN della topologia della distribuzione effettiva, nel rapporto verranno visualizzati tali indirizzi e nomi, altrimenti verrà visualizzato il testo predefinito.
    
      - Rapporto certificati - In questo rapporto vengono elencati i nomi soggetto e i nomi alternativi del soggetto relativi ai certificati necessari per la topologia.
    
      - Rapporto firewall - In questo rapporto vengono elencate le informazioni necessarie per configurare i firewall perimetrali nell'infrastruttura. Vengono visualizzati gli indirizzi IP (i valori predefiniti o modificati), il ruolo del server, l'indirizzo IP e la porta di origine, l'indirizzo IP e la porta di destinazione, il protocollo di trasporto, il protocollo applicativo e le note pertinenti.
    
      - Rapporto DNS - In questo rapporto vengono elencate le informazioni relative alle voci DNS da creare. Sono inclusi il tipo di record, l'FQDN, l'indirizzo IP e i commenti necessari per un corretto funzionamento.

  - Riepilogo sito - Tale riepilogo presenta una panoramica delle selezioni effettuate durante le domande iniziali o dei valori inseriti in **Progetta siti** . Vengono inoltre visualizzate informazioni sulla capacità.
    

    > [!NOTE]
    > Le informazioni presenti nella pagina Riepilogo sito sono personalizzate per ogni progettazione e potrebbero non includere tutte le sezioni o le informazioni illustrate in questo argomento.



## Vedere anche

#### Concetti

[Modifica del diagramma di configurazione della rete in Lync Server 2013](lync-server-2013-editing-the-network-configuration-diagram.md)

