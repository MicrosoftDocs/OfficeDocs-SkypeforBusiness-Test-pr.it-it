---
title: "Lync Server 2013: Conf. impost. glob. di bypass multim. per info su sito e area geog."
TOCTitle: "Lync Server 2013: Conf. impost. glob. di bypass multim. per info su sito e area geog."
ms:assetid: 0a21cdf1-f350-49da-b346-70806f256bea
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398150(v=OCS.15)
ms:contentKeyID: 49299623
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare le impostazioni globali di bypass multimediale per l'utilizzo delle informazioni del sito e dell'area geografica

 

_**Ultima modifica dell'argomento:** 2012-09-21_


> [!NOTE]
> In questo argomento si presuppone che il bypass multimediale (Media Bypass) sia già stato configurato per qualsiasi connessione trunk dal Mediation Server a un peer (un gateway PSTN (Public Switched Telephone Network), un IP-PBX o un Session Border Controller (SBC) presso un provider di servizi di telefonia Internet o ITSP) per un sito o un servizio specifico per il quale si desidera ignorare il Mediation Server.<BR>In questo argomento si presuppone inoltre che in Generatore di topologie tutti i siti centrali e i siti di succursale siano stati definiti in modo da corrispondere alla configurazione di aree di rete, siti di rete e subnet effettuata eseguendo le procedure descritte in <A href="lync-server-2013-create-or-modify-a-network-region.md">Creare o modificare un'area di rete in Lync Server 2013</A>, <A href="lync-server-2013-create-or-modify-a-network-site.md">Creare o modificare un sito di rete in Lync Server 2013</A> e <A href="lync-server-2013-associate-a-subnet-with-a-network-site.md">Associare una subnet a un sito di rete in Lync Server 2013</A>. Se non corrispondono, il bypass multimediale avrà esito negativo.



Oltre ad abilitare il bypass multimediale per le singole connessioni trunk associate a un peer, è necessario configurare le impostazioni globali. Se si utilizza la procedura illustrata in questo argomento per configurare le impostazioni globali per il bypass multimediale, il presupposto è che una o entrambe le situazioni seguenti incidano sulla configurazione:

  - *Non* si dispone di una buona connettività tra gli endpoint di Lync Server e i peer per cui è stato configurato il bypass multimediale sulla connessione trunk.

  - Il controllo di ammissione di chiamata per la gestione della larghezza di banda è abilitato.
    

    > [!NOTE]
    > Per informazioni dettagliate sulle considerazioni relative al controllo di ammissione di chiamata e al bypass multimediale, vedere la sezione sul controllo di ammissione di chiamata per le connessioni PSTN in <A href="lync-server-2013-media-bypass-and-mediation-server.md">Bypass multimediale e Mediation Server in Lync Server 2013</A> nella documentazione relativa alla pianificazione.



Le informazioni relative alle aree di rete e ai siti di rete vengono condivise tra le caratteristiche di VoIP aziendale avanzate del controllo di ammissione di chiamata e del bypass multimediale, quando entrambi sono abilitati. Se il controllo di ammissione di chiamata è già configurato, non sarà pertanto necessario eseguire la procedura seguente per modificare le informazioni sui siti e sulle aree in modo specifico per il bypass multimediale. Eseguire questa procedura se le aree e i siti di rete non sono stati ancora configurati per il controllo di ammissione di chiamata e si desidera modificare le impostazioni per il bypass multimediale.

In alternativa, eseguire questa procedura se si desidera utilizzare le informazioni sui siti e sulle aree per prendere una decisione relativa al bypass, ma non si ha alcuna intenzione di abilitare il controllo di ammissione di chiamata. In tal caso, i collegamenti con restrizioni per la larghezza di banda dovranno comunque essere rappresentati mediante criteri tra siti di rete, come spiegato in [Creare criteri intrasito di rete in Lync Server 2013](lync-server-2013-create-network-intersite-policies.md). Gli effettivi vincoli di larghezza di banda in questa circostanza sono meno importanti perché il controllo di ammissione di chiamata non è stato abilitato. Questi collegamenti vengono invece utilizzati per suddividere le subnet in modo da specificare quelle senza limiti di larghezza di banda e che possono quindi utilizzare il bypass multimediale. Ciò si verifica anche quando il controllo di ammissione di chiamata e il bypass multimediale sono entrambi abilitati.

Per un corretto funzionamento del bypass, è inoltre necessaria la coerenza tra la definizione di un sito in Generatore di topologie e la definizione del sito durante la configurazione delle aree e dei siti di rete. Ad esempio, se vi è un sito di succursale definito in Generatore di topologie con un solo gateway PSTN distribuito, tale sito di succursale dovrà essere configurato con criteri di VoIP aziendale che consentano l'instradamento delle chiamate PSTN degli utenti del sito attraverso il gateway PSTN nel sito in questione.

## Per configurare le informazioni relative ai siti e alle aree per il bypass multimediale

1.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

2.  Nella barra di spostamento sinistra fare clic su **Configurazione di rete**.

3.  Fare doppio clic sulla configurazione **Globale** nella tabella.

4.  Nella pagina **Modifica impostazioni globali** selezionare la casella di controllo **Abilita bypass multimediale**.

5.  Fare clic su **Utilizza configurazione siti e aree**.

6.  Se necessario, selezionare la casella di controllo **Abilita bypass per siti non mappati**.
    

    > [!NOTE]
    > Selezionare questa casella di controllo solo se alla stessa area sono associati uno o più siti di grandi dimensioni senza vincoli di larghezza di banda, ad esempio un grande sito centrale, ma anche siti di succursale con vincoli di larghezza di banda. Quando si abilita il bypass per i siti non mappati, la configurazione viene snellita perché è necessario specificare esclusivamente le subnet associate ai siti di succursale anziché tutte le subnet associate a tutti i siti. È consigliabile non selezionare questa casella di controllo se il controllo di ammissione di chiamata è abilitato.



7.  Fare clic su **Commit**.

Aggiungere quindi le subnet al sito di rete come descritto in [Associare subnet a siti di rete per bypass multimediale](lync-server-2013-associate-subnets-with-network-sites-for-media-bypass.md). Le effettive procedure per associare subnet a siti di rete sono riportate in [Associare una subnet a un sito di rete in Lync Server 2013](lync-server-2013-associate-a-subnet-with-a-network-site.md). Dopo aver associato tutte le subnet ai siti di rete, la distribuzione del bypass multimediale può considerarsi completata.

> [!IMPORTANT]  
> Se non sono stati ancora creati i siti e le aree di rete, è necessario crearli prima di poter proseguire con la distribuzione del bypass multimediale. Per informazioni dettagliate, vedere <a href="lync-server-2013-create-or-modify-a-network-region.md">Creare o modificare un'area di rete in Lync Server 2013</a> e <a href="lync-server-2013-create-or-modify-a-network-site.md">Creare o modificare un sito di rete in Lync Server 2013</a>.

## Vedere anche

#### Concetti

[Associare subnet a siti di rete per bypass multimediale](lync-server-2013-associate-subnets-with-network-sites-for-media-bypass.md)

