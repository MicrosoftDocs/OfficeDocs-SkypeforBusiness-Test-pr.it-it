---
title: 'Lync Server 2013: Creare criteri sito per chat persistente'
TOCTitle: Creare criteri sito per chat persistente
ms:assetid: 1327ff5c-b859-4010-a240-e0b2b084b5bd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204693(v=OCS.15)
ms:contentKeyID: 49299746
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare criteri sito per chat persistente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-06_

Per ognuno dei siti distribuiti è possibile creare criteri di Chat persistente specifici.

La configurazione dei criteri sito ha la precedenza sui criteri globali, ma solo per il sito specifico a cui i criteri si riferiscono.


> [!NOTE]
> Per configurare e utilizzare il server Chat persistente, è innanzitutto necessario utilizzare Generatore di topologie per aggiungere il supporto del server Chat persistente alla topologia e quindi pubblicare la topologia. Per informazioni dettagliate, vedere <A href="lync-server-2013-adding-persistent-chat-server-to-your-deployment.md">Aggiunta del server Chat persistente alla distribuzione in Lync Server 2013</A> nella documentazione relativa alla distribuzione.<BR>Per configurare le impostazioni di configurazione del server Chat persistente, vedere <A href="lync-server-2013-configure-persistent-chat-server-options-globally-or-for-persistent-chat-server-pool.md">Configurare le opzioni del server chat persistente a livello globale o per il pool di server chat persistente in Lync Server 2013</A> nella documentazione relativa alla distribuzione.



## Per creare criteri di Chat persistente per un sito

1.  Da un account utente assegnato al ruolo CsPersistentChatAdministrator, CsAdministrator o CsUserAdministrator , eseguire l'accesso a qualsiasi computer nella distribuzione interna.

2.  Fare clic sul pulsante **Start** e scegliere Pannello di controllo di Lync Server oppure aprire una finestra del browser e quindi immettere l'URL di amministrazione. Per informazioni dettagliate sui diversi metodi che è possibile utilizzare per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Chat persistente** e quindi su **Criteri Chat persistente**.
    
    > [!important]  
    > È inoltre possibile usare i cmdlet di Windows PowerShell. Per informazioni dettagliate, vedere <a href="configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md">Configurazione del server Chat persistente tramite i cmdlet di Windows PowerShell</a> nella documentazione relativa alla distribuzione.

4.  Fare clic su **Nuovo** e quindi su **Criteri sito** .

5.  In **Seleziona un sito** fare clic sul sito a cui devono essere applicati i criteri.

6.  In **Nuovi criteri Chat persistente** eseguire le operazioni seguenti:
    
      - In **Nome** specificare un nome per i nuovi criteri di sito, ad esempio Redmond.
    
      - In **Descrizione** immettere informazioni dettagliate sugli scopi dei criteri di sito, ad esempio "Criteri chat room per Redmond".
    
      - Per controllare Chat persistente per tutti i siti non controllati specificatamente attraverso un criterio di sito, selezionare o deselezionare la casella di controllo **Abilita Chat persistente**.

7.  Fare clic su **Commit** .

