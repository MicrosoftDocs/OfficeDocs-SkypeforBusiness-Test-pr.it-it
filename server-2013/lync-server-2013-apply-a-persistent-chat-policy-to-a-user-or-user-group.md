---
title: "Lync Server 2013: Applica criteri Chat persistente a utente o gruppo utenti"
TOCTitle: Applicare i criteri di Chat persistente a un utente o un gruppo di utenti
ms:assetid: 809ef4e0-8d42-4feb-b7c0-3995f39867a7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205038(v=OCS.15)
ms:contentKeyID: 49301138
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Applicare i criteri di Chat persistente a un utente o un gruppo di utenti in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-06_

Se un utente è stato abilitato per Lync Server 2013, sarà possibile applicare i criteri appropriati a utenti specifici per abilitarli o disabilitarli al server Chat persistente.


> [!NOTE]
> Per configurare e utilizzare il server Chat persistente, è innanzitutto necessario utilizzare Generatore di topologie per aggiungere il supporto del server Chat persistente alla topologia e quindi pubblicare la topologia. Per informazioni dettagliate, vedere <A href="lync-server-2013-adding-persistent-chat-server-to-your-deployment.md">Aggiunta del server Chat persistente alla distribuzione in Lync Server 2013</A> nella documentazione relativa alla distribuzione.<BR>Per configurare le impostazioni di configurazione del server Chat persistente, vedere <A href="lync-server-2013-configure-persistent-chat-server-options-globally-or-for-persistent-chat-server-pool.md">Configurare le opzioni del server chat persistente a livello globale o per il pool di server chat persistente in Lync Server 2013</A> nella documentazione relativa alla distribuzione.



Utilizzare la procedura in questo argomento per applicare criteri di Chat persistente a livello utente creati in precedenza a uno o più account utente o gruppo di utenti.

## Per applicare criteri di Chat persistente a livello di utente a un account utente

1.  Da un account utente assegnato al ruolo CsPersistentChatAdministrator, CsAdministrator o CsUserAdministrator , eseguire l'accesso a qualsiasi computer nella distribuzione interna.

2.  Fare clic sul pulsante **Start** e scegliere Pannello di controllo di Lync Server oppure aprire una finestra del browser e quindi immettere l'URL di amministrazione. Per informazioni dettagliate sui diversi metodi che è possibile utilizzare per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Utenti** e quindi cercare l'account utente da configurare.

4.  Nella tabella in cui sono elencati i risultati della ricerca fare clic sull'account utente, su **Modifica** e quindi su **Mostra dettagli** .

5.  In **Modifica utente di Lync Server**, in **Criteri di Chat persistente**, selezionare i criteri di Chat persistente da applicare.
    

    > [!NOTE]
    > L'impostazione <STRONG>&lt;Automatici&gt;</STRONG> consente di applicare il criterio effettivo predefinito. Queste impostazioni vengono applicate automaticamente dal server.



6.  Fare clic su **Commit** .

