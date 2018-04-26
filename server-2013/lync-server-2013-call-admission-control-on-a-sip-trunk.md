---
title: 'Lync Server 2013: Controllo di ammissione di chiamata in un trunk SIP'
TOCTitle: Controllo di ammissione di chiamata in un trunk SIP
ms:assetid: 7eada098-3d47-4be2-839f-8f87d582efe8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398632(v=OCS.15)
ms:contentKeyID: 49301113
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Controllo di ammissione di chiamata in un trunk SIP in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-22_

Per distribuire il servizio Controllo di ammissione di chiamata in un trunk SIP, creare un sito di rete per rappresentare il provider di servizi di telefonia Internet (ITSP). Per applicare i valori dei criteri di larghezza di banda nel trunk SIP, creare criteri tra siti tra il sito di rete dell'organizzazione e il sito di rete creato per rappresentare l'ITSP.

Nella figura seguente è illustrato un esempio di distribuzione del servizio Controllo di ammissione di chiamata in un trunk SIP.

**Configurazione del servizio Controllo di ammissione di chiamata in un trunk SIP**

![Diagramma del trunking SIP del controllo di ammissione di chiamata](images/Gg398632.276c0d8f-1dd5-4883-8499-c202399ddbe9(OCS.15).jpg "Diagramma del trunking SIP del controllo di ammissione di chiamata")

Per configurare il servizio Controllo di ammissione di chiamata in un trunk SIP, è necessario eseguire le operazioni seguenti durante la distribuzione del servizio:

1.  Creare un sito di rete per rappresentare l'ITSP. Associare il sito di rete a un'area di rete appropriata e allocare una larghezza di banda pari a zero per audio e video per il sito di rete. Per informazioni dettagliate, vedere [Configurare siti di rete per il servizio Controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-configure-network-sites-for-cac.md) nella documentazione relativa alla distribuzione.
    

    > [!NOTE]
    > Per l'ITSP, questa configurazione del sito di rete non è funzionale. I valori dei criteri di larghezza di banda vengono effettivamente applicati nel passaggio 2.



2.  Creare un collegamento tra siti per il trunk SIP utilizzando i valori dei parametri rilevanti per il sito creato nel passaggio 1. Utilizzare, ad esempio, il nome del sito di rete dell'organizzazione come valore del parametro NetworkSiteID1 e il sito di rete dell'ITSP come valore del parametro NetworkSiteID2. Per ulteriori informazioni, vedere [Creare criteri intrasito di rete in Lync Server 2013](lync-server-2013-create-network-intersite-policies.md) nella documentazione relativa alla distribuzione. Vedere inoltre l'argomento relativo al cmdlet New-CsNetworkInterSitePolicy nella documentazione di Lync Server Management Shell.

3.  Ottenere l'indirizzo IP del punto di terminazione multimediale SBC (Session Border Controller) dall'ITSP. Aggiungere tale indirizzo IP con una subnet mask di 32 al sito di rete che rappresenta l'ITSP. Per informazioni dettagliate, vedere [Associare una subnet a un sito di rete in Lync Server 2013](lync-server-2013-associate-a-subnet-with-a-network-site.md).

