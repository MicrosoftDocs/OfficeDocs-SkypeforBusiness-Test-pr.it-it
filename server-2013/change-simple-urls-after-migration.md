---
title: Modificare gli URL semplici dopo la migrazione
TOCTitle: Modificare gli URL semplici dopo la migrazione
ms:assetid: addb0dc8-8324-42b1-9a00-f4bd14fdf5c0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721844(v=OCS.15)
ms:contentKeyID: 49887701
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modificare gli URL semplici dopo la migrazione

 

_**Ultima modifica dell'argomento:** 2012-09-22_

Lync Server supporta tre URL semplici:

  - L'URL **riunione** (meet) viene utilizzato come URL di base per tutte le conferenze nel sito o nell'organizzazione. Con l'URL semplice riunione, i collegamenti per partecipare alle riunioni sono semplici da capire, da comunicare e da distribuire.

  - L'URL **per accesso esterno** (dialin) consente di accedere alla pagina Web Impostazioni conferenza telefonica con accesso esterno. L'URL semplice per accesso esterno è incluso in tutti gli inviti a riunioni, in modo che gli utenti che desiderano eseguire l'accesso esterno alla riunione dispongano delle informazioni necessarie sul numero di telefono e sul PIN.

  - L'URL di **amministrazione** (admin) consente di accedere rapidamente al Pannello di controllo di Lync Server. L'URL semplice di amministrazione è interno all'organizzazione.

Dopo la migrazione in Lync Server 2013, è necessario tenere conto del modo in cui la modifica ha effetto sui record DNS e sui certificati per gli URL semplici. Se il Director di Lync Server 2010 legacy rimane in uso nella topologia, non sono necessarie modifiche relative agli URL semplici. Se il Director di Lync Server 2010 viene rimosso dalla topologia dopo la migrazione, i record DNS degli URL semplici devono essere aggiornati in modo da puntare a uno dei pool di Lync Server 2013. Ogni volta che si modifica il nome di un URL semplice, è necessario però eseguire Enable-CsComputer in ogni Director e Front End Server per registrare la modifica.

## Modifica degli URL semplici dopo la migrazione

**Per aggiornare l'URL semplice riunione**

1.  In Generatore di topologie fare clic con il pulsante destro del mouse sul nodo principale **Lync Server** e quindi scegliere **Modifica proprietà** .

2.  Nel riquadro sinistro selezionare **URL semplici** , quindi in **URL riunione** selezionare l'URL riunione e quindi fare clic su **Modifica URL** .

3.  Aggiornare l'URL in base al valore desiderato e quindi fare clic su **OK** per salvare l'URL modificato.

**Per aggiornare l'URL semplice di amministrazione**

1.  In Generatore di topologie fare clic con il pulsante destro del mouse sul nodo principale **Lync Server** e quindi scegliere **Modifica proprietà** .

2.  Nel riquadro sinistro selezionare **URL semplici** , quindi nella casella **URL di accesso amministrativo** immettere l'URL semplice che si desidera utilizzare per l'accesso amministrativo al Pannello di controllo di Lync Server 2013 e quindi fare clic su **OK** .
    
    > [!TIP]  
    > È consigliabile utilizzare l'URL più semplice possibile per l'accesso amministrativo. L'opzione più semplice è <strong>https://admin.</strong> <em>&lt;domain&gt;</em> .

## Vedere anche

#### Concetti

[Pianificazione degli URL semplici in Lync Server 2013](lync-server-2013-planning-for-simple-urls.md)

