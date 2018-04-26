---
title: 'Lync Server 2013: Definire ulteriori trunk in Generatore di topologie'
TOCTitle: Definire ulteriori trunk in Generatore di topologie
ms:assetid: e68b8377-50a2-452a-bf5c-910929e34236
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721915(v=OCS.15)
ms:contentKeyID: 49887796
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definire ulteriori trunk in Generatore di topologie in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-04_

Eseguire le procedure descritte di seguito per utilizzare Generatore di topologie per definire un trunk aggiuntivo a cui è possibile associare un *peer* con un Mediation Server. Un peer offre agli utenti abilitati per VoIP aziendale la connettività alla rete PSTN (Public Switched Telephone Network). Un peer può essere un gateway PSTN, un IP-PBX, o un SBC (Session Border Controller) per un provider di servizi di telefonia Internet (ITSP). Il trunk definisce la connessione tra il Mediation Server e il peer. È possibile definire più trunk per ogni Mediation Server. Un Mediation Server può essere associato a più peer.

Un trunk è una connessione logica tra un Mediation Server e un gateway identificato in modo univoco dalla tupla:

{FQDN del Mediation Server, porta di attesa del Mediation Server (TLS o TCP) : IP e FQDN del gateway, porta di attesa del gateway}


> [!NOTE]
> In questo argomento si presuppone che sia già stato installato un gateway PSTN e un trunk radice con almeno un Mediation Server collocato o autonomo o un pool Mediation Server, come descritto in <A href="lync-server-2013-define-a-gateway-in-topology-builder.md">Definire un gateway in Generatore di topologie in Lync Server 2013</A> nella documentazione relativa alla distribuzione.




> [!NOTE]
> In questo argomento si presuppone che sia stato configurato come minimo un pool Front End o un server Standard Edition in almeno un sito centrale, come descritto in <A href="lync-server-2013-define-and-configure-a-front-end-pool-or-standard-edition-server.md">Definire e configurare un pool Front End o un server Standard Edition in Lync Server 2013</A> e <A href="lync-server-2013-publish-the-topology.md">Pubblicare la topologia in Lync Server 2013</A> nella documentazione relativa alla distribuzione.



## Per definire un trunk aggiuntivo tra un Mediation Server e un peer gateway

1.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.

2.  In Lync Server 2013, nome del sito, **Componenti condivisi** fare clic con il pulsante destro del mouse sul nodo **Trunk** e quindi scegliere **Nuovo trunk** .
    
    ![Schermata della struttura di file di Generatore di topologie di Lync Server](images/JJ721915.90d5b349-aa1e-407a-87ed-fa112f478560(OCS.15).png "Schermata della struttura di file di Generatore di topologie di Lync Server")

3.  In **Definisci nuovo trunk** , specificare un nome descrittivo per identificare in modo univoco il trunk. Non è possibile definire due trunk con lo stesso nome.
    

    > [!NOTE]
    > Se si specifica TLS (Transport Layer Security) come tipo di trasporto, sarà necessario specificare l'FQDN anziché l'indirizzo IP del peer del Mediation Server.



4.  In **Gateway PSTN associato** selezionare il peer gateway PSTN da associare al trunk.
    
    ![Impostazioni delle proprietà del peer gateway PSTN per trunk](images/JJ721915.7c3fe8ee-8f4c-4413-8462-8347228e61bb(OCS.15).png "Impostazioni delle proprietà del peer gateway PSTN per trunk")

5.  In **Porta di attesa per gateway IP/PSTN** digitare una porta di attesa che verrà utilizzata dal peer (gateway PSTN, IP-PBX o SBC) per la ricezione dei messaggi SIP dal Mediation Server associato a questo trunk. Le porte predefinite per il peer sono 5066 per TCP (Transmission Control Protocol) e 5067 per TLS (Transport Layer Security). Le porte predefinite per Survivable Branch Appliance sono 5081 per TCP e 5082 per TLS.

6.  In **Protocollo trasporto SIP** fare clic sul tipo di di trasporto utilizzato dal peer.
    

    > [!NOTE]
    > Per motivi di sicurezza, è consigliabile distribuire un peer nel Mediation Server che può utilizzare TLS.



7.  In **Mediation Server associato** selezionare il pool Mediation Server da associare al trunk radice del peer.

8.  In **Porta Mediation Server associato** digitare la porta di attesa su cui il Mediation Server riceverà i messaggi SIP dal peer.
    

    > [!NOTE]
    > Con il supporto di più trunk in Lync Server 2013, due trunk con nomi diversi non possono essere configurati con gli stessi valori per <STRONG>Porta Mediation Server associato</STRONG> e <STRONG>Porta di attesa per gateway IP/PSTN</STRONG> .

    

    > [!NOTE]
    > Con il supporto di più trunk in Lync Server 2013, è possibile definire più porte di segnalazione SIP nel Mediation Server per le comunicazioni con più peer. Durante la definizione di un trunk, il numero in <STRONG>Porta Mediation Server associato</STRONG> deve essere compreso nell'intervallo delle porte di attesa per il rispettivo protocollo consentito dal Mediation Server. Questo intervallo di porte è definito in Lync Server 2013 e pool di Mediation Server. Fare clic con il pulsante destro del mouse sul pool di Mediation Server rilevante e scegliere <STRONG>Modifica proprietà</STRONG> . Specificare l'intervallo di porte nel campo <STRONG>Porte di attesa</STRONG> .



9.  Fare clic su **OK** .

## Vedere anche

#### Attività

[Modificare un trunk in Generatore di topologie in Lync Server 2013](lync-server-2013-modify-a-trunk-in-topology-builder.md)

