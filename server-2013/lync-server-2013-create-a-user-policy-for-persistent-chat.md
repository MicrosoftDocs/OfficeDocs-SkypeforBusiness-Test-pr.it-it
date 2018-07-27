---
title: 'Lync Server 2013: Creare criteri utente per Chat persistente'
TOCTitle: Creare criteri utente per Chat persistente
ms:assetid: aa3774af-d442-4206-8a68-2fbb9102e9d6
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205170(v=OCS.15)
ms:contentKeyID: 49301611
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare criteri utente per Chat persistente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-06_

Nel Pannello di controllo di Lync Server definire i criteri utente che possono essere assegnati agli utenti in **Utenti** .

Il criterio utente ha la priorità sul criterio globale e sui criteri sito, ma solo per gli utenti specifici a cui viene assegnato il criterio utente.


> [!NOTE]
> Per configurare e utilizzare il server Chat persistente, è innanzitutto necessario utilizzare Generatore di topologie per aggiungere il supporto del server Chat persistente alla topologia e quindi pubblicare la topologia. Per informazioni dettagliate, vedere <A href="lync-server-2013-adding-persistent-chat-server-to-your-deployment.md">Aggiunta del server Chat persistente alla distribuzione in Lync Server 2013</A> nella documentazione relativa alla distribuzione.<BR>Per configurare le impostazioni di configurazione del server Chat persistente, vedere <A href="lync-server-2013-configure-persistent-chat-server-options-globally-or-for-persistent-chat-server-pool.md">Configurare le opzioni del server chat persistente a livello globale o per il pool di server chat persistente in Lync Server 2013</A> nella documentazione relativa alla distribuzione.



## Per creare un criterio utente per Chat persistente

1.  Da un account utente assegnato al ruolo CsPersistentChatAdministrator, CsAdministrator o CsUserAdministrator , eseguire l'accesso a qualsiasi computer nella distribuzione interna.

2.  Fare clic sul pulsante **Start** e scegliere Pannello di controllo di Lync Server oppure aprire una finestra del browser e quindi immettere l'URL di amministrazione. Per informazioni dettagliate sui diversi metodi che è possibile utilizzare per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).
    
    > [!IMPORTANT]  
    > È inoltre possibile utilizzare i cmdlet di Windows PowerShell. Vedere <a href="configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md">Configurazione del server Chat persistente tramite i cmdlet di Windows PowerShell</a> nella documentazione relativa alla distribuzione.

3.  Sulla barra di spostamento sinistra fare clic su **Chat persistente** e quindi su **Criteri Chat persistente**.

4.  Fare clic su **Nuovo** e quindi su **Criteri utente** .

5.  In **Nuovi criteri Chat persistente** eseguire le operazioni seguenti:
    
      - In **Nome** specificare un nome per il nuovo criterio utente.
    
      - In **Descrizione** immettere informazioni dettagliate sugli scopi del criterio utente, ad esempio "Criterio Chat persistente per l'utente specifico".
    
      - Per controllare Chat persistente per tutti gli utenti non controllati specificamente tramite un criterio utente, selezionare o deselezionare la casella di controllo **Abilita Chat persistente**.

6.  Fare clic su **Commit** .

