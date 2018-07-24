---
title: 'Lync Server 2013: Definire un gateway in Generatore di topologie'
TOCTitle: Definire un gateway in Generatore di topologie
ms:assetid: 456e5a96-d9f6-42a6-862c-a69464391628
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg425945(v=OCS.15)
ms:contentKeyID: 49300383
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definire un gateway in Generatore di topologie in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-04_

Eseguire la procedura seguente per utilizzare il Generatore di topologie per definire un *peer* a cui sia possibile associare un Mediation Server per garantire la connettività alla rete PSTN (Public Switched Telephone Network) agli utenti abilitati per VoIP aziendale. Un peer del Mediation Server può essere un gateway PSTN, un IP-PBX o un SBC (Session Border Controller) per un provider di servizi di telefonia Internet (ITSP) a cui ci si connette configurando un trunk SIP.


> [!NOTE]
> In questo argomento si presuppone che sia stato configurato come minimo un pool Front End o un server Standard Edition interno in almeno un sito centrale con un Mediation Server collocato o autonomo, come descritto in <A href="lync-server-2013-define-and-configure-a-front-end-pool-or-standard-edition-server.md">Definire e configurare un pool Front End o un server Standard Edition in Lync Server 2013</A> e in <A href="lync-server-2013-publish-the-topology.md">Pubblicare la topologia in Lync Server 2013</A> nella documentazione relativa alla distribuzione. In questo argomento si presuppone inoltre che sia stata verificata la conformità dell'infrastruttura ai prerequisiti descritti in <A href="lync-server-2013-software-prerequisites-for-enterprise-voice.md">Prerequisiti software per VoIP aziendale in Lync Server 2013</A> e <A href="lync-server-2013-security-and-configuration-prerequisites-for-enterprise-voice.md">Prerequisiti di configurazione e sicurezza per VoIP aziendale in Lync Server 2013</A>.



## Per definire un peer per il Mediation Server

1.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.

2.  In Lync Server 2013, al di sotto del nome del sito, Componenti condivisi, fare clic con il pulsante destro del mouse sul nodo **Gateway PSTN** e quindi scegliere **Nuovo gateway PSTN** .
    
    ![Generatore di topologie Lync Server 2013](images/Gg425945.d898c3c1-8798-4b74-8f02-b994ef3db4c1(OCS.15).png "Generatore di topologie Lync Server 2013")

3.  Nella finestra **Definisci nuovo gateway IP/PSTN** digitare il nome di dominio completo (FQDN) o l'indirizzo IP del peer e quindi fare clic su **Avanti** .
    
    ![Gateway IP/PSTN](images/Gg425945.8017ba5e-41bc-48d4-97d9-fd306cd322b8(OCS.15).png "Gateway IP/PSTN")
    

    > [!NOTE]
    > Se si specifica TLS (Transport Layer Security) come tipo di trasporto, sarà necessario specificare l'FQDN anziché l'indirizzo IP del peer del Mediation Server.



4.  Definire la modalità di attesa (IPv4 o IPv6) dell'indirizzo IP del nuovo gateway PSTN e quindi fare clic su **Avanti** .
    
    ![Indirizzo IP](images/Gg425945.c7fc0d12-adc8-45a7-aca1-b376e1d2fcec(OCS.15).png "Indirizzo IP")

5.  Definire un *trunk radice* per il gateway PSTN. Un trunk è una connessione logica tra un Mediation Server e un gateway identificato in modo univoco dalla tuple.
    
    {FQDN del Mediation Server, porta di attesa del Mediation Server (TLS o TCP) : IP e FQDN del gateway, porta di attesa del gateway}
    
      - Quando si definisce un gateway PSTN nel Generatore di topologie, è necessario definire un trunk radice perché sia possibile aggiungerlo a una topologia.
    
      - Il trunk radice non può essere rimosso se non si rimuove prima il gateway PSTN associato.
    
    ![Definizione del gateway: trunk radice](images/Gg425945.3b030757-eb35-4616-bb6b-74ee67507e3d(OCS.15).png "Definizione del gateway: trunk radice")

6.  In **Porta di attesa per gateway IP/PSTN** digitare la porta di attesa che verrà utilizzata dal gateway, dal PBX o dal sistema SBC per i messaggi SIP provenienti dal Mediation Server che verrà associato al trunk radice del gateway PSTN. Per impostazione predefinita, vengono utilizzate la porta 5066 per TCP (Transmission Control Protocol) e la porta 5067 per TLS (Transport Layer Security) in un gateway PSTN, un PBX o un sistema SBC. In un Survivable Branch Appliance in un sito di succursale vengono utilizzate per impostazione predefinita la porta 5081 per TCP e la porta 5082 per TLS.

7.  In **Protocollo trasporto SIP** fare clic sul tipo di trasporto utilizzato dal peer e quindi su **OK** .
    

    > [!NOTE]
    > Per motivi di sicurezza, è consigliabile distribuire un peer nel Mediation Server che può utilizzare TLS.



8.  In **Mediation Server associato** selezionare il pool di Mediation Server da associare al trunk radice di questo gateway PSTN.

9.  In **Porta Mediation Server associato** digitare la porta di attesa che verrà utilizzata dal Mediation Server per i messaggi SIP provenienti dal gateway.
    

    > [!NOTE]
    > Grazie al supporto di più trunk di Lync Server 2013, è possibile definire più porte di segnalazione SIP per il Mediation Server da utilizzare per la comunicazione con più gateway PSTN. Quando si definisce un trunk, il valore di <STRONG>Porta Mediation Server associato</STRONG> deve rientrare nell'intervallo delle porte di attesa del rispettivo protocollo consentito dal Mediation Server. Questo intervallo di porte viene definito in Lync Server 2013 e Pool Mediation Server. Fare clic con il pulsante destro del mouse sul pool di Mediation Server desiderato e quindi scegliere <STRONG>Modifica proprietà</STRONG> . Specificare l'intervallo di porte nel campo <STRONG>Porte di attesa</STRONG> .



10. Fare clic su **Fine** .

> [!important]  
> Prima di completare questo passaggio, verificare che il peer definito sia in esecuzione e utilizzi l'FQDN o l'indirizzo IP specificato.

Per aggiungere successivamente il peer alla topologia, seguire le procedure illustrate in [Pubblicare la topologia in Lync Server 2013](lync-server-2013-publish-the-topology.md) nella documentazione relativa alla distribuzione. È necessario pubblicare la topologia ogni volta che si utilizza il Generatore di topologie per creare o modificare la topologia, in modo che i dati possano essere utilizzati per installare i file per i server che eseguono Lync Server.

## Vedere anche

#### Attività

[Modificare un trunk in Generatore di topologie in Lync Server 2013](lync-server-2013-modify-a-trunk-in-topology-builder.md)

