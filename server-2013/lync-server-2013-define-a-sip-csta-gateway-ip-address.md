---
title: "Lync Server 2013: Definire l'indirizzo IP di un gateway SIP/CSTA"
TOCTitle: Definire l'indirizzo IP di un gateway SIP/CSTA
ms:assetid: ae944057-3ad6-4474-a09b-81a3d27bd50f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg602125(v=OCS.15)
ms:contentKeyID: 49301654
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definire l'indirizzo IP di un gateway SIP/CSTA in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

Se si prevede che Lync Server si connetterà al gateway SIP/CSTA distribuito per il controllo delle chiamate remote utilizzando una connessione TCP (Transmission Control Protocol), è necessario definire l'indirizzo IP del gateway in Generatore di topologie. Questa operazione non è necessaria per i gateway che supportano le connessioni TLS (Transport Layer Security). Per qualsiasi gateway in grado di supportare le connessioni TLS, è possibile ignorare questa procedura e continuare la distribuzione del controllo delle chiamate remote eseguendo le operazioni descritte in [Abilitare gli utenti di Lync per il controllo delle chiamate remote in Lync Server 2013](lync-server-2013-enable-lync-users-for-remote-call-control.md).

## Per definire l'indirizzo IP di un gateway SIP/CSTA mediante Generatore di topologie

1.  Accedere al computer in cui è installato Generatore di topologie come membro del gruppo Domain Admins e del gruppo RTCUniversalServerAdmins.

2.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.

3.  Scegliere l'opzione per scaricare una topologia esistente.

4.  Espandere il nodo **Server applicazioni attendibili** .

5.  Fare clic con il pulsante destro del mouse sul pool di applicazioni attendibili creato come descritto in [Configurare una voce applicazione attendibile per il controllo delle chiamate remote in Lync Server 2013](lync-server-2013-configure-a-trusted-application-entry-for-remote-call-control.md) e quindi scegliere **Modifica proprietà** .

6.  Deselezionare la casella di controllo **Abilita la replica dei dati di configurazione nel pool** .

7.  Fare clic su **Limita utilizzo servizio a indirizzi IP selezionati** . L'impostazione predefinita è **Usa tutti gli indirizzi IP configurati** .

8.  Nella casella di testo **Indirizzo IP primario** immettere l'indirizzo IP del gateway SIP/CSTA.

9.  Per aggiornare la topologia nell'archivio di gestione centrale, fare clic su **Lync Server** nell'albero della console e quindi su **Pubblica** nel riquadro **Azioni** .

## Vedere anche

#### Attività

[Configurare una route statica per il controllo delle chiamate remote in Lync Server 2013](lync-server-2013-configure-a-static-route-for-remote-call-control.md)  
[Configurare una voce applicazione attendibile per il controllo delle chiamate remote in Lync Server 2013](lync-server-2013-configure-a-trusted-application-entry-for-remote-call-control.md)

