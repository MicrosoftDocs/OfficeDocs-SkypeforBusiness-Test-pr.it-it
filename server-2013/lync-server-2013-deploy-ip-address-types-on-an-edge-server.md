---
title: 'Lync Server 2013: Distribuire i tipi di indirizzi IP in un server perimetrale'
TOCTitle: Distribuire i tipi di indirizzi IP in un server perimetrale
ms:assetid: 6e2fe7e8-6e90-4d1a-8fc5-e3be92c46571
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204984(v=OCS.15)
ms:contentKeyID: 49300913
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuire i tipi di indirizzi IP in un server perimetrale per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-06-14_

Utilizzando Generatore di topologie, eseguire i passaggi della procedura seguente per distribuire i tipi di indirizzo IP su un server perimetrale.

## Per distribuire tipi di indirizzo IP su un server perimetrale

1.  In Generatore di topologie, sotto **Pool di server perimetrali** , fare clic con il tasto destro del mouse sul server all'interno di un pool, e selezionare **Modifica proprietà** . (Alternativamente, selezionare il server e fare clic su **Modifica proprietà** dal menu **Azione** .)

2.  Nella finestra **Modifica proprietà** , selezionare la configurazione dell'indirizzo IP che si desidera supportare. Nelle figure seguenti è mostrata una configurazione dual stack per l'interfaccia interna e l'interfaccia esterna.
    
    **Interfaccia interna del server perimetrale dual stack**
    
    ![Pagina delle proprietà generali di Lync Server](images/JJ204984.5b0883ee-b9f2-4a21-91a9-3286d0beb63b(OCS.15).png "Pagina delle proprietà generali di Lync Server")
    
    **Interfaccia esterna del server perimetrale dual stack**
    
    ![Pagina di configurazione esterna o dell'hop successivo di Lync Server](images/JJ204984.2aa00ce2-ba50-40aa-bbf1-78636016daf9(OCS.15).png "Pagina di configurazione esterna o dell'hop successivo di Lync Server")

3.  Per ciascun tipo di indirizzo selezionato, è necessario fornire gli indirizzi interni e esterni appropriati.

