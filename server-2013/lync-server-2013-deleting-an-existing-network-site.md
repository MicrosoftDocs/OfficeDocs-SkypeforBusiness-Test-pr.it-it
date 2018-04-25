---
title: Eliminazione di un sito di rete esistente
TOCTitle: Eliminazione di un sito di rete esistente
ms:assetid: 2762149b-3572-4513-b838-beda7fa9e81e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688001(v=OCS.15)
ms:contentKeyID: 49887487
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminazione di un sito di rete esistente

 

_**Ultima modifica dell'argomento:** 2012-11-01_

I siti di rete sono gli uffici o le postazioni configurate in ogni area di una distribuzione del servizio Controllo di ammissione di chiamata (CAC) o del servizio per chiamate di emergenza Enhanced 9-1-1. È possibile usare il Pannello di controllo di Lync Server 2013 per configurare i siti e associarli alle aree. Ad esempio, un'area di rete per il Nord America potrebbe essere associata a siti di rete come Chicago, Redmond e Vancouver. È necessario creare un sito di rete del servizio Controllo di ammissione di chiamata per ogni sito di un'organizzazione, anche se tale sito non presenta limitazioni per la larghezza di banda. Dal Pannello di controllo di Lync Server è possibile creare, modificare ed eliminare siti di rete. Per eliminare un sito di rete esistente, usare la procedura che segue. Per informazioni dettagliate sulla creazione o sulla modifica dei siti di rete, vedere [Creazione o modifica dei siti di rete](lync-server-2013-creating-or-modifying-network-sites.md)

## Per eliminare un sito di rete

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Sito**.

4.  Nella pagina **Sito** fare clic sul sito da eliminare.
    

    > [!NOTE]
    > È possibile eliminare più siti contemporaneamente. A tale scopo, premere CTRL e selezionare più siti sempre tenendo premuto CTRL. In alternativa, per selezionare tutti i siti, scegliere <STRONG>Seleziona tutto</STRONG> dal menu <STRONG>Modifica</STRONG>.



5.  Dal menu **Modifica** fare clic su **Elimina**.

6.  Fare clic su **OK**.
    

    > [!WARNING]
    > Se un sito di rete è associato a una subnet di rete, non è possibile rimuoverlo. Se si tenta di rimuovere un sito associato a una subnet, verrà visualizzato un messaggio di errore. Per controllare se un sito è associato a eventuali subnet, fare clic sul sito e quindi scegliere <STRONG>Mostra dettagli</STRONG> dal menu <STRONG>Modifica</STRONG>.


