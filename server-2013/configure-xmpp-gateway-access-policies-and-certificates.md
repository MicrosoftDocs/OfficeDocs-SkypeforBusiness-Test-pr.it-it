---
title: Configurare criteri di accesso e certificati del gateway XMPP
TOCTitle: Configurare criteri di accesso e certificati del gateway XMPP
ms:assetid: fac02f4e-d14d-4be3-b53c-74c82436fd93
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721945(v=OCS.15)
ms:contentKeyID: 49887837
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare criteri di accesso e certificati del gateway XMPP

 

_**Ultima modifica dell'argomento:** 2012-10-15_

La federazione di XMPP definisce una distribuzione esterna in base al protocollo XMPP (Extensible Messaging and Presence Protocol). Una configurazione XMPP consente agli utenti di Lync di accedere agli utenti del dominio XMPP mediante:

  - Messaggistica istantanea e presenza (solo diretta)

  - Creazione di contatti federati XMPP nel client Lync

Quando si configurano criteri per supportare i partner federati XMPP (Extensible Messaging and Presence Protocol), i criteri si applicano agli utenti dei domini federati XMPP, ma non agli utenti dei provider di servizi di messaggistica istantanea SIP (Session Initiation Protocol), ad esempio Windows Live, o dei domini federati SIP. Configurare un partner federato XMPP per ogni dominio federato XMPP che gli utenti potranno aggiungere ai contatti e con cui potranno comunicare. Dopo che sono stati creati i criteri, è necessario configurare i certificati del gateway XMPP.


> [!NOTE]
> Per iniziare la migrazione del gateway XMPP, distribuire il gateway XMPP di Lync Server 2013 e configurare i criteri di accesso per abilitare gli utenti per il gateway XMPP di Lync Server 2013. Prima di eseguire la procedura, spostare tutti gli utenti nella distribuzione di Lync Server 2013. Per informazioni dettagliate, vedere <A href="configure-xmpp-gateway-on-lync-server-2013.md">Configurare il gateway XMPP in Lync Server 2013</A>.



## Configurare un criterio di accesso esterno per abilitare gli utenti per il gateway XMPP di Lync Server 2013

1.  Aprire il Pannello di controllo di Lync Server.

2.  Sulla barra di spostamento sinistra fare clic su **Federazione e accesso esterno** e quindi su **Criteri di accesso esterno** .

3.  Fare clic su **Nuovo** e quindi su **Criteri utente** .

4.  Immettere un nome per i criteri di accesso per gli utenti esterni.

5.  Specificare una descrizione per i criteri di accesso per gli utenti esterni.

6.  Selezionare **Abilita comunicazioni con utenti federati** .

7.  Selezionare **Abilita le comunicazioni con gli utenti federati XMPP** .

8.  Fare clic su **Commit** per salvare le modifiche apportate ai criteri utente o sito.

