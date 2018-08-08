---
title: "Lync Server 2013: Modifica route vocali per usare LS 2013 Mediation Server"
TOCTitle: "Lync Server 2013: Modifica route vocali per usare LS 2013 Mediation Server"
ms:assetid: acd487b3-377c-46bf-9f71-fe6152002664
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205162(v=OCS.15)
ms:contentKeyID: 49301638
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modificare le route vocali per l'utilizzo del nuovo Lync Server 2013 Mediation Server

 

_**Ultima modifica dell'argomento:** 2012-09-28_

Questa procedura consente di modificare le route vocali per utilizzare il Mediation Server di Lync Server 2013, anziché il Mediation Server di Office Communications Server 2007 R2 legacy.

## Per modificare le route vocali per l'utilizzo del nuovo Mediation Server

1.  Pannello di controllo di Lync Server 2013

2.  Nel riquadro sinistro selezionare **Routing vocale** e quindi **Route** .

3.  Fare clic su **Nuovo** per creare una nuova route vocale.

4.  Completare i campi seguenti:
    
      - **Nome** : digitare un nome descrittivo per la route vocale. Per questo documento verrà utilizzato il nome **W15PSTNRoute** .
    
      - **Descrizione** : digitare una breve descrizione della route vocale.

5.  Ignorare tutte le altre sezioni fino a **Gateway associati** . Fare clic su **Aggiungi** . Selezionare il nuovo gateway predefinito e fare clic su **OK** .

6.  In **Utilizzi PSTN associati** fare clic su **Seleziona**

7.  Nella pagina **Seleziona record utilizzo PSTN** selezionare un nome di record e quindi fare clic su **OK** .

8.  Nella pagina **Nuova route vocale** fare clic su **OK** per creare la **Route vocale** .

9.  Nella pagina **Routing vocale** selezionare **Route** .

10. Spostare la nuova route creata all'inizio dell'elenco e quindi selezionare **Commit** .

