---
title: 'Lync Server 2013: Definire un Mediation Server in Generatore di topologie'
TOCTitle: Definire un Mediation Server in Generatore di topologie
ms:assetid: 59d8f5ba-5064-4ea5-b4bf-2b9736e0fedd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398391(v=OCS.15)
ms:contentKeyID: 49300641
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definire un Mediation Server in Generatore di topologie in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-03-25_

Eseguire i passaggi descritti in questo argomento per utilizzare Generatore di topologie per definire un Mediation Server autonomo o un pool collocato con un pool Front End in un sito per il quale precedentemente non è stato distribuito VoIP aziendale.

È possibile definire una topologia utilizzando un account membro del gruppo Administrators.

## Definire Mediation Server in collocazione con un pool Front End

Eseguire i passaggi descritti in questo argomento per utilizzare Generatore di topologie per definire un Mediation Server collocato con un pool Front End in un sito per il quale precedentemente non è stato distribuito VoIP aziendale.

## Per aggiungere un Mediation Server a un pool Front End

1.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.

2.  In Generatore di topologie, nell'albero della console, espandere il nome del sito per cui si desidera definire un pool Front End.

3.  Nell'albero della console fare clic con il pulsante destro del mouse sul tipo di pool Front End desiderato e quindi scegliere **Nuovo pool Front End**.

4.  Scorrere i vari passaggi della procedura guidata **Definisci nuovo pool Front End** fino a raggiungere la pagina **Selezionare ruoli server collocati** .

5.  In **Selezionare ruoli server collocati** selezionare l'opzione **Colloca Mediation Server**.
    

    > [!NOTE]
    > <UL>
    > <LI>
    > <P>Se il tipo di pool Front End selezionato è Enterprise Edition, il componente Mediation Server verrà installato in tutti i Front End Server di tale pool Front End.</P>
    > <LI>
    > <P>Il <STRONG>Pool hop successivo</STRONG> utilizzato dal Mediation Server sarà il pool Front End in cui è collocato il Mediation Server.</P>
    > <LI>
    > <P>Il <STRONG>Pool di server perimetrali</STRONG> utilizzato dal Mediation Server sarà lo stesso pool di server perimetrali associato al pool Front End in cui è collocato il Mediation Server.</P></LI></UL>



6.  Fare clic su **Rendi predefinito** per utilizzare questo pool Front End per instradare le chiamate da Microsoft Office Communications Server 2007 R2 al PSTN.

7.  Fare clic su **Fine** dopo aver completato l'associazione di uno o più peer al pool Front End.
    

    > [!NOTE]
    > Prima di procedere con il passaggio successivo nel processo di distribuzione di VoIP aziendale, assicurarsi che il pool del Mediation Server (ovvero il pool Front End in collocazione con il componente Mediation Server) stia utilizzando i nomi FQDN specificati.



8.  Seguire quindi le procedure descritte in [Pubblicare la topologia in Lync Server 2013](lync-server-2013-publish-the-topology.md) nella documentazione della guida alla distribuzione per aggiungere il Mediation Server alla topologia prima di procedere con il passaggio successivo che prevede la modifica delle porte di attesa del Mediation Server, se necessario. È necessario pubblicare la topologia ogni volta che si utilizza Generatore di topologie per definire o modificare la topologia.

## Definire il Mediation Server autonomo

Eseguire i passaggi descritti in questo argomento per utilizzare Generatore di topologie per definire un Mediation Server autonomo o un pool Mediation Server in un sito per il quale precedentemente non è stato distribuito VoIP aziendale.

Se i Mediation Server sono già stati distribuiti in collocazione in pool Front End nel sito, è possibile ignorare questa sezione e [Installare i file per Mediation Server in Lync Server 2013](lync-server-2013-install-the-files-for-mediation-server.md) prima di continuare con [Configurazione di trunk in Lync Server 2013](lync-server-2013-configuring-trunks.md).


> [!NOTE]
> In questa sezione si presuppone che sia già stato installato almeno un pool Front End, come descritto in <A href="lync-server-2013-define-and-configure-a-front-end-pool-or-standard-edition-server.md">Definire e configurare un pool Front End o un server Standard Edition in Lync Server 2013</A> e <A href="lync-server-2013-publish-the-topology.md">Pubblicare la topologia in Lync Server 2013</A> nella documentazione della guida alla distribuzione.



## Per aggiungere un Mediation Server

1.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.

2.  In Generatore di topologie, nell'albero della console, espandere il nome del sito per cui si desidera definire un Mediation Server.

3.  Nell'albero della console fare clic con il pulsante destro del mouse sul nodo **Pool Mediation Server** e quindi scegliere **pool di Mediation Server**.

4.  In **Definisci nuovo pool Mediation Server** digitare il nome di dominio completo (FQDN) del pool Mediation Server.

5.  Eseguire quindi una delle operazioni seguenti:
    
      - Se si desidera distribuire più Mediation Server nel pool per ottenere disponibilità elevata, selezionare **Pool di più computer** .
        

        > [!NOTE]
        > È necessario distribuire il bilanciamento del carico DNS per supportare i pool Mediation Server con più Mediation Server. Per informazioni dettagliate, vedere la sezione dedicata all'utilizzo del bilanciamento del carico DNS in pool Mediation Server nell'argomento <A href="lync-server-2013-dns-load-balancing.md">Bilanciamento del carico DNS in Lync Server 2013</A> nella documentazione relativa alla pianificazione.

    
      - Se si desidera distribuire un solo Mediation Server nel pool perché non è necessaria la disponibilità elevata, selezionare **Pool computer singolo** e ignorare il passaggio seguente.

6.  Se si seleziona **Pool di più computer** nel passaggio precedente , in **Definire i computer nel pool corrente** fare clic su **FQDN computer** , digitare l'FQDN di ogni server nel pool e quindi fare clic su **Aggiungi** . Ripetere il passaggio per tutti i Mediation Server che si desidera aggiungere al pool. Dopo aver definito tutti i computer nel pool, fare clic su **Avanti** .

7.  Nella pagina **Selezionare l'hop successivo** fare clic su **Pool hop successivo** , fare clic sul nome FQDN del pool Front End che utilizzerà questo pool Mediation Server e quindi fare clic su **Avanti** .

8.  Nella pagina **Selezionare un server perimetrale** eseguire una delle operazioni seguenti:
    
      - Se si desidera rendere disponibile la connettività PSTN agli utenti esterni abilitati per VoIP aziendale, in **Selezionare il pool di server perimetrali utilizzato dal Mediation Server** fare clic sul nome FQDN del pool di server perimetrali che utilizzeranno questo pool Mediation Server per rendere disponibile la connettività PSTN a tali utenti esterni e quindi fare clic su **Avanti** .
    
      - Se non si prevede di abilitare gli utenti esterni per VoIP aziendale o non si desidera rendere disponibile la connettività PSTN per gli utenti quando si trovano all'esterno della rete interna, fare clic su **Avanti** .

9.  Seguire quindi le procedure in [Pubblicare la topologia in Lync Server 2013](lync-server-2013-publish-the-topology.md) nella documentazione relativa alla distribuzione per aggiungere il Mediation Server alla topologia. È necessario pubblicare la topologia ogni volta che si utilizza Generatore di topologie per creare o modificare la topologia, in modo che i dati possano essere utilizzati per installare i file per i server che eseguono Lync Server. Continuare quindi con i passaggi successivi per modificare le porte di attesa nel Mediation Server, se necessario.

## Definire le porte di attesa di Mediation Server

Eseguire i passaggi descritti in questo argomento per utilizzare Generatore di topologie per definire le porte di attesa sulle quali un Mediation Server o un pool Mediation Server accetterà le connessioni in arrivo da un peer gateway.

## Per modificare le porte di attesa di Mediation Server

1.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.

2.  In Generatore di topologie, nell'albero della console espandere il nodo **Pool Mediation Server** e quindi fare clic con il pulsante destro del mouse sul Mediation Server precedentemente creato.

3.  Per impostazione predefinita, le porte di attesa SIP nel Mediation Server sono 5070 per il traffico TLS da Lync Server e 5067 per il traffico TLS dai peer (gateway, PBX o SBC). La porta TCP è disabilitata per impostazione predefinita. È necessario abilitare la porta TCP in presenza di gateway che non supportano TLS.

4.  Specificare l'intervallo di porte di attesa TLS o TCP desiderato per il quale il Mediation Server accetterà connessioni in arrivo dai gateway PSTN.
    

    > [!NOTE]
    > Non è necessario immettere un intervallo di porte TCP se l'opzione <STRONG>Abilita la porta TCP</STRONG> non è selezionata. Questa impostazione è facoltativa.



A questo punto, [Definire un gateway in Generatore di topologie in Lync Server 2013](lync-server-2013-define-a-gateway-in-topology-builder.md) e installare i file in ogni Mediation Server nel pool seguendo le procedure descritte in [Installare i file per Mediation Server in Lync Server 2013](lync-server-2013-install-the-files-for-mediation-server.md).

