---
title: 'Lync Server 2013: Abilitare i criteri del server Chat persistente'
TOCTitle: Abilitare i criteri del server Chat persistente
ms:assetid: 87063d6c-2e38-4970-b76d-2aa15f0de29e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205056(v=OCS.15)
ms:contentKeyID: 49301214
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Abilitare i criteri del server Chat persistente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-06_

Nel Pannello di controllo di Lync Server 2013 è possibile utilizzare la pagina **Criteri di Chat persistente** del gruppo **Chat persistente** per gestire i criteri a livello globale, di pool, di sito o di utente, incluse la configurazione dei criteri globali predefiniti e la creazione di uno o più criteri di utente e sito aggiuntivi per la distribuzione. Se un utente è abilitato tramite criteri all'utilizzo del server Chat persistente, l'ambiente del server Chat persistente comparirà nel client Lync 2013 dello stesso.


> [!NOTE]
> Nella topologia, i criteri di sito del server Chat persistente si applicano a livello globale, per pool utente, per sito utente o per utente.



Il criterio globale viene creato automaticamente quando si distribuisce il server Chat persistente e può essere configurato, ma non eliminato. Poiché il criterio globale si applica a tutti gli utenti, non è necessario configurarlo per utente.

È possibile creare e configurare più criteri utente e sito che, insieme al criterio globale, abilitano gli utenti al server Chat persistente. I criteri pool e sito del server Chat persistente hanno priorità sul criterio globale del server Chat persistente, ma solo per gli utenti di quel sito. I criteri utente hanno la priorità sia sul criterio globale che sui criteri pool e sito per gli utenti a cui viene assegnato il criterio utente.


> [!NOTE]
> Per configurare e utilizzare il server Chat persistente, è innanzitutto necessario utilizzare Generatore di topologie per aggiungere il supporto del server Chat persistente alla topologia e quindi pubblicare la topologia. Per informazioni dettagliate, vedere <A href="lync-server-2013-adding-persistent-chat-server-to-your-deployment.md">Aggiunta del server Chat persistente alla distribuzione in Lync Server 2013</A> nella documentazione relativa alla distribuzione.



## Contenuto della sezione

  - [Configurare i criteri globali per Chat persistente in Lync Server 2013](lync-server-2013-configure-the-global-policy-for-persistent-chat.md)

  - [Creare criteri sito per chat persistente in Lync Server 2013](lync-server-2013-create-a-site-policy-for-persistent-chat.md)

  - [Creare criteri utente per Chat persistente in Lync Server 2013](lync-server-2013-create-a-user-policy-for-persistent-chat.md)

  - [Applicare i criteri di Chat persistente a un utente o un gruppo di utenti in Lync Server 2013](lync-server-2013-apply-a-persistent-chat-policy-to-a-user-or-user-group.md)

