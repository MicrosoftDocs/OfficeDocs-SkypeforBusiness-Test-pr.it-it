---
title: 'Lync Server 2013: Definire la topologia perimetrale'
TOCTitle: Definire la topologia perimetrale
ms:assetid: 787b23f1-8fa0-4c37-abf2-c516c5dd66f0
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398591(v=OCS.15)
ms:contentKeyID: 49301043
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definire la topologia perimetrale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-28_

È necessario utilizzare Generatore di topologie per creare la topologia ed è necessario configurare almeno un pool Front End interno o un server Standard Edition prima di poter distribuire il server perimetrale. Utilizzare la procedura seguente per definire la topologia perimetrale per un singolo server perimetrale e quindi utilizzare le procedure incluse in [Pubblicare la topologia in Lync Server 2013](lync-server-2013-publish-your-topology.md) e [Esportare la topologia di Lync Server 2013 e copiarla su supporto esterno per l'installazione perimetrale](lync-server-2013-export-your-topology-and-copy-it-to-external-media-for-edge-installation.md) per pubblicare la topologia e renderla disponibile per il server perimetrale.


> [!NOTE]
> Per l'interfaccia perimetrale interna e per quella esterna è necessario utilizzare lo stesso tipo di bilanciamento del carico. Non è possibile utilizzare il bilanciamento del carico DNS in un'interfaccia perimetrale e il bilanciamento del carico hardware nell'altra.



Per pubblicare, abilitare o disabilitare correttamente una topologia quando si aggiunge o rimuove un ruolo del server, è necessario aver effettuato l'accesso come membro dei gruppi RTCUniversalServerAdmins e Domain Admins. È anche possibile concedere le autorizzazioni e i diritti di amministratore necessari per l'aggiunta di ruoli del server a un account utente. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md) nella documentazione relativa alla distribuzione di server Standard Edition e Server Enterprise. Per altre modifiche di configurazione, è necessaria solo l'appartenenza al gruppo RTCUniversalServerAdmins.

Se la topologia perimetrale è stata definita durante la definizione e la pubblicazione della topologia interna e non sono richieste modifiche alla topologia perimetrale creata in precedenza, non è necessario definirla e pubblicarla di nuovo. Utilizzare la procedura seguente solo se è necessario apportare modifiche alla topologia perimetrale. È necessario rendere la topologia precedentemente definita e pubblicata disponibile per i server perimetrali, utilizzando la procedura descritta in [Esportare la topologia di Lync Server 2013 e copiarla su supporto esterno per l'installazione perimetrale](lync-server-2013-export-your-topology-and-copy-it-to-external-media-for-edge-installation.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Non è possibile eseguire Generatore di topologie da un server perimetrale, ma è necessario eseguirlo dai server Front End Server o Standard Edition.</td>
</tr>
</tbody>
</table>


Il processo per la definizione della topologia del server perimetrale avviene in Generatore di topologie. In seguito sono elencati i tre tipi principali di topologie dei server perimetrali che è possibile pianificare e configurare:

  - Per definire la topologia per un singolo server perimetrale

  - Per definire la topologia per un pool di server perimetrali con bilanciamento del carico

  - Per definire la topologia per un pool di server perimetrali con bilanciamento del carico hardware

## Per definire la topologia per un singolo server perimetrale

1.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.

2.  Nell'albero della console espandere il sito in cui si desidera distribuire un server perimetrale.

3.  Fare clic con il pulsante destro del mouse su **Pool di server perimetrali** e quindi scegliere **Nuovo pool di server perimetrali** .

4.  In **Definire il nuovo pool di server perimetrali** fare clic su **Avanti** .

5.  In **Definire l'FQDN del pool di server perimetrali** eseguire le operazioni seguenti:
    
      - In **FQDN pool** digitare il nome di dominio completo (FQDN) dell'interfaccia interna per il server perimetrale.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Il nome specificato deve essere identico al nome del computer configurato nel server. Per impostazione predefinita, il nome di un computer che non fa parte di un dominio è un nome breve, non un FQDN. Poiché Generatore di topologie utilizza gli FQDN e non i nomi brevi, è necessario aggiungere un suffisso DNS al nome del computer che non fa parte di un dominio e che deve essere distribuito come server perimetrale. Nell'assegnare FQDN dei server Lync Server, dei server perimetrali e dei pool, utilizzare solo i caratteri standard (inclusi i caratteri A-Z, a-z, 0-9 e i trattini). Non utilizzare caratteri Unicode o di sottolineatura. I caratteri non standard in un FQDN spesso non sono supportati nel sistema DNS esterno e nelle CA pubbliche (quando l'FQDN deve essere assegnato al nome soggetto nel certificato). Per informazioni dettagliate sull'aggiunta di un suffisso DNS a un nome di computer, vedere <a href="lync-server-2013-configure-dns-for-edge-support.md">Configurare DNS per il supporto dei componenti perimetrali in Lync Server 2013</a>.</td>
        </tr>
        </tbody>
        </table>
    
      - Fare clic su **Pool computer singolo** e quindi fare clic su **Avanti** .

6.  In **Selezionare funzionalità** eseguire le operazioni seguenti:
    
      - Se si prevede di utilizzare un singolo FQDN e indirizzo IP per il servizio di accesso SIP, il servizio Web Conferencing di Lync Server 2013 e i servizi A/V Edge, selezionare la casella di controllo **Utilizzare FQDN e indirizzo IP singoli** .
    
      - Se si prevede di abilitare la federazione, selezionare la casella di controllo **Abilita la federazione per questo pool di server perimetrali (porta 5061)** .
        

        > [!NOTE]
        > È possibile selezionare questa opzione, tuttavia solo un pool di server perimetrali o un server perimetrale dell'organizzazione può essere pubblicato esternamente per la federazione. Tutto l'accesso da parte di utenti federati, inclusi gli utenti di messaggistica istantanea pubblica, passa per lo stesso pool di server perimetrali o server perimetrale singolo. Se, ad esempio, la distribuzione include un pool di server perimetrali o un singolo server perimetrale distribuito a New York e uno distribuito a Londra e si abilita il supporto per la federazione nel pool di server perimetrali o nel server perimetrale di New York, il traffico dei segnali per gli utenti federati passerà per il pool di server perimetrali o il singolo server perimetrale di New York. Ciò vale anche per le comunicazioni con gli utenti di Londra, anche se un utente interno di Londra che chiami un utente federato di Londra utilizzerà il pool o il server perimetrale di Londra per il traffico audio/video.

    
      - Se si prevede di supportare il protocollo XMPP per la distribuzione, selezionare la casella di controllo **Abilita la federazione XMPP (porta 5269)**

7.  In **Selezionare le opzioni IP** eseguire le operazioni seguenti:
    
      - **Abilita IPv4 su interfaccia interna** : selezionare questa casella di controllo se si desidera applicare un indirizzo IPv4 all'interfaccia interna di server perimetrale o pool di server perimetrali
    
      - **Abilita IPv6 su interfaccia interna** : selezionare questa casella di controllo se si desidera applicare un indirizzo IPv6 all'interfaccia interna di server perimetrale o pool di server perimetrali
    
      - **Abilita IPv4 su interfaccia esterna** : selezionare questa casella di controllo se si desidera applicare un indirizzo IPv4 all'interfaccia esterna di server perimetrale o pool di server perimetrali
    
      - **Abilita IPv6 su interfaccia esterna** : selezionare questa casella di controllo se si desidera applicare un indirizzo IPv6 all'interfaccia esterna di server perimetrale o pool di server perimetrali
    
    È inoltre possibile configurare il server perimetrale o il pool di server perimetrali affinché utilizzi un indirizzo NAT (network address translation) per gli indirizzi IP esterni. È possibile eseguire questa configurazione selezionando la casella di controllo **L'indirizzo IP esterno del pool di server perimetrali è convertito da NAT.** .

8.  In **FQDN esterni** eseguire le operazioni seguenti:
    
      - Se in **Selezionare funzionalità** si è scelto di utilizzare un singolo FQDN e indirizzo IP per l'accesso SIP, il servizio Web Conferencing e il servizio A/V Edge, digitare l'FQDN esterno in **Accesso SIP** .
        

        > [!NOTE]
        > Se si sceglie di selezionare questa opzione, è necessario specificare un numero di porta diverso per ogni servizio Edge (impostazioni di porta consigliate: 5061 per il servizio Access Edge, 444 per il servizio Web Conferencing Edge e 443 per il servizio A/V Edge). Selezionando questa opzione, è possibile evitare possibili problemi di connettività e semplificare la configurazione, in quanto è quindi possibile utilizzare lo stesso numero di porta, ad esempio 443, per i tre servizi.

    
      - Se in **Selezionare funzionalità** non si è scelto di utilizzare un singolo FQDN e indirizzo IP, digitare gli FQDN esterni per **Accesso SIP** , **Web Conferencing** e **Audio/Video** , mantenendo le porte predefinite.

9.  Fare clic su **Avanti** .

10. In **Definire l'indirizzo IP interno** , digitare l'indirizzo IP del server perimetrale in **Indirizzo IPv4 interno** e **Indirizzo IPv6 interno** , a seconda dei propri requisiti. Fare clic su **Avanti** .

11. In **Definire l'indirizzo IP esterno** eseguire le operazioni seguenti:
    
      - Se si è scelto di utilizzare un singolo FQDN e indirizzo IP per l'accesso SIP, il servizio Web Conferencing e il servizio A/V Edge, digitare l'indirizzo IPv4 esterno del server perimetrale in **Accesso SIP** e quindi fare clic su **Avanti** .
    
      - Se si è scelto di utilizzare indirizzi IPv6, digitare l'indirizzo IPv6 esterno del server perimetrale in **Accesso SIP** , quindi fare clic su **Avanti** .
    
      - Se non si è scelto di utilizzare un singolo FQDN e indirizzo IP per l'accesso SIP, il servizio Web Conferencing e il servizio A/V Edge, digitare gli indirizzi IPv4 esterni del server perimetrale in **Accesso SIP** , **Web Conferencing** e **A/V Conferencing** e quindi fare clic su **Avanti** .
    
      - Se si è scelto di utilizzare indirizzi IPv6 ma non si è scelto di utilizzare un singolo FQDN e indirizzo IP per l'accesso SIP, il servizio Web Conferencing e il servizio A/V Edge, digitare gli indirizzi IPv6 esterni del server perimetrale in **Accesso SIP** , **Web Conferencing** e **A/V Conferencing** e quindi fare clic su **Avanti** .
        

        > [!NOTE]
        > Se non è stato scelto di abilitare e assegnare gli indirizzi IPv6, questa finestra di dialogo non viene visualizzata.



12. Se si è scelto di utilizzare NAT, viene visualizzata una finestra di dialogo. In **Indirizzo IPv4 pubblico per il servizio A/V Edge** digitare l'indirizzo IPv4 pubblico da convertire tramite NAT e quindi fare clic su **Avanti** .
    

    > [!NOTE]
    > Tale indirizzo deve corrispondere all'indirizzo IP esterno del servizio A/V Edge.



13. Se si è scelto di utilizzare NAT e indirizzi IPv6, viene visualizzata una finestra di dialogo. In **Indirizzo IPv6 pubblico per il servizio A/V Edge** digitare l'indirizzo IPv6 pubblico da convertire tramite NAT e quindi fare clic su **Avanti** .
    

    > [!NOTE]
    > Tale indirizzo deve corrispondere all'indirizzo IP esterno del servizio A/V Edge.



14. In **Pool hop successivo** in **Definire l'hop successivo** selezionare il nome del pool interno, che può essere un pool Front End o un pool Standard Edition. In alternativa, se la distribuzione include un server Director, selezionare il nome di questo server e quindi fare clic su **Avanti** .

15. In **Associare pool Front End** specificare uno o più pool interni, che possono includere pool Front End e server Standard Edition, da associare a questo server perimetrale, selezionando i nomi dei pool interni che utilizzeranno il server perimetrale per la comunicazione con gli utenti esterni supportati.
    

    > [!NOTE]
    > È possibile associare solo un pool di server perimetrali o un singolo server perimetrale con carico bilanciato a ogni pool interno per il traffico audio/video. Se è già stato associato un pool interno a un pool di server perimetrali o a un server perimetrale, viene visualizzato un avviso che indica che al pool interno è già associato un pool di server perimetrali o un server perimetrale. Se si seleziona un pool già associato a un altro server perimetrale, l'associazione verrà modificata.



16. Fare clic su **Fine** .

17. Pubblicare la topologia.

## Per definire la topologia per un pool di server perimetrali con bilanciamento del carico DNS

1.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.

2.  Nell'albero della console espandere il sito in cui si desidera distribuire i server perimetrali.

3.  Fare clic con il pulsante destro del mouse su **Pool di server perimetrali** e quindi scegliere **Nuovo pool di server perimetrali** .

4.  In **Definire il nuovo pool di server perimetrali** fare clic su **Avanti** .

5.  In **Definire l'FQDN del pool di server perimetrali** eseguire le operazioni seguenti:
    
      - In **Pool FQDN** digitare il nome di dominio completo (FQDN) della connessione interna del server perimetrale.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Utilizzare solo caratteri standard, ovvero A-Z, a-z, 0-9 e trattini, per assegnare FQDN dei server Lync Server, dei server perimetrali e dei pool. Non utilizzare caratteri Unicode o di sottolineatura. La presenza di caratteri non standard in un FQDN è spesso non supportata da DNS esterni e CA pubbliche (quando l'FQDN deve essere assegnato al nome soggetto nel certificato). Per informazioni dettagliate sull'aggiunta di un suffisso DNS a un nome di computer, vedere Generatore di topologie.</td>
        </tr>
        </tbody>
        </table>
    
      - Fare clic su **Pool di più computer** e quindi su **Avanti** .

6.  In **Selezionare funzionalità** eseguire le operazioni seguenti:
    
      - Se si prevede di utilizzare un singolo FQDN e indirizzo IP per l'accesso SIP, il servizio Web Conferencing di Lync Server 2013 e il servizio A/V Edge, selezionare la casella di controllo **Utilizzare FQDN e indirizzo IP singoli** .
    
      - Se si prevede di abilitare la federazione, selezionare la casella di controllo **Abilita la federazione per questo pool di server perimetrali (porta 5061)** . Fare clic su **Avanti**
        

        > [!NOTE]
        > È possibile selezionare questa opzione, ma è possibile pubblicare esternamente per la federazione solo un pool di server perimetrali o un server perimetrale nell'organizzazione. Tutto l'accesso da parte di utenti federati, inclusi gli utenti di messaggistica istantanea pubblica, passa per lo stesso pool di server perimetrali o singolo server perimetrale. Se, ad esempio, la distribuzione include un pool di server perimetrali o un singolo server perimetrale distribuito a New York e uno distribuito a Londra e si abilita il supporto per la federazione nel pool di server perimetrali o nel server perimetrale di New York, il traffico dei segnali per gli utenti federati passerà per il pool di server perimetrali o il singolo server perimetrale di New York. Ciò vale anche per le comunicazioni con gli utenti di Londra, anche se un utente interno di Londra che chiama un utente federato di Londra utilizzerà il pool o il server perimetrale di Londra per il traffico audio/video.

    
      - Se si prevede di supportare il protocollo XMPP per la distribuzione, selezionare la casella di controllo **Abilita la federazione XMPP (porta 5269)**

7.  Fare clic su **Avanti** .

8.  In **Selezionare le opzioni IP** eseguire le operazioni seguenti:
    
      - **Abilita IPv4 su interfaccia interna** : selezionare questa casella di controllo se si desidera applicare un indirizzo IPv4 all'interfaccia interna di server perimetrale o pool di server perimetrali
    
      - **Abilita IPv6 su interfaccia interna** : selezionare questa casella di controllo se si desidera applicare un indirizzo IPv6 all'interfaccia interna di server perimetrale o pool di server perimetrali
    
      - **Abilita IPv4 su interfaccia esterna** : selezionare questa casella di controllo se si desidera applicare un indirizzo IPv4 all'interfaccia esterna di server perimetrale o pool di server perimetrali
    
      - **Abilita IPv6 su interfaccia esterna** : selezionare questa casella di controllo se si desidera applicare un indirizzo IPv6 all'interfaccia esterna di server perimetrale o pool di server perimetrali
    
    È inoltre possibile configurare il server perimetrale o il pool di server perimetrali affinché utilizzi un indirizzo NAT (network address translation) per gli indirizzi IP esterni. È possibile eseguire questa configurazione selezionando la casella di controllo **L'indirizzo IP esterno del pool di server perimetrali è convertito da NAT.** .

9.  In **FQDN esterni** eseguire le operazioni seguenti:
    
      - Se in **Selezionare funzionalità** si è scelto di utilizzare un singolo FQDN e indirizzo IP per l'accesso SIP, il servizio Web Conferencing e il servizio A/V Edge, digitare l'FQDN esterno in **Accesso SIP** .
        

        > [!NOTE]
        > Se si sceglie di selezionare questa opzione, è necessario specificare un numero di porta diverso per ogni servizio Edge (impostazioni di porta consigliate: 5061 per il servizio Access Edge, 444 per il servizio Web Conferencing Edge e 443 per il servizio A/V Edge). Selezionando questa opzione, è possibile evitare possibili problemi di connettività e semplificare la configurazione, in quanto è quindi possibile utilizzare lo stesso numero di porta, ad esempio 443, per i tre servizi.

    
      - Se in **Selezionare funzionalità** non si è scelto di utilizzare un singolo FQDN e indirizzo IP, digitare l'FQDN scelto per il lato pubblico del pool di server perimetrali in **Accesso SIP** . In **Web Conferencing** digitare l'FQDN scelto per il lato pubblico del pool di server perimetrali. In **Audio/Video** digitare l'FQDN scelto per il lato pubblico del pool di server perimetrali. Utilizzare le porte predefinite.

10. Fare clic su **Avanti** .

11. In **Definire i computer nel pool corrente** fare clic su **Aggiungi** .

12. In **Indirizzo IP e FQDN interni** eseguire le operazioni seguenti:
    
      - In **Indirizzo IPv4 interno** , digitare l'indirizzo IPv4 e l' **Indirizzo IPv6 interno** , a seconda dei propri requisiti, del primo server perimetrale che si desidera creare nel pool.
    
      - In **FQDN interno** digitare l'FQDN del primo server perimetrale che si desidera creare nel pool.
        

        > [!NOTE]
        > Il nome specificato deve essere identico al nome del computer configurato nel server. Per impostazione predefinita, il nome di un computer che non fa parte di un dominio è un nome breve, non un FQDN. Poiché Generatore di topologie utilizza gli FQDN e non i nomi brevi, è necessario aggiungere un suffisso DNS al nome del computer che non fa parte di un dominio e che deve essere distribuito come server perimetrale. Nell'assegnare FQDN dei server Lync Server, dei server perimetrali, dei pool e degli array, utilizzare solo i caratteri standard (inclusi i caratteri A-Z, a-z, 0-9 e i trattini). Non utilizzare caratteri Unicode o di sottolineatura. I caratteri non standard in un FQDN spesso non sono supportati nel sistema DNS esterno e nelle CA pubbliche (quando l'FQDN deve essere assegnato al nome soggetto nel certificato). Per informazioni dettagliate sull'aggiunta di un suffisso DNS a un nome di computer, vedere <A href="lync-server-2013-configure-dns-for-edge-support.md">Configurare DNS per il supporto dei componenti perimetrali in Lync Server 2013</A>.



13. Fare clic su **Avanti** .

14. In **Definire l'indirizzo IP esterno** eseguire le operazioni seguenti:
    
      - Se si è scelto di utilizzare un singolo FQDN e indirizzo IP per l'accesso SIP, il servizio Web Conferencing e il servizio A/V Edge, digitare l'indirizzo IP esterno del server perimetrale in **Accesso SIP** .
    
      - Se non si è scelto di utilizzare un singolo FQDN e indirizzo IP per l'accesso SIP, il servizio Web Conferencing e il servizio A/V Conferencing, digitare l'indirizzo IP scelto per il lato pubblico di questo server del pool di server perimetrali in **Accesso SIP** . In **Web Conferencing** digitare l'indirizzo IP scelto per il lato pubblico di questo server del pool di server perimetrali. In **A/V Conferencing** digitare l'indirizzo IP scelto per il lato pubblico di questo server del pool di server perimetrali.

15. Fare clic su **Avanti** .

16. Se è stato scelto di abilitare gli indirizzi IPv6, in **Definire l'indirizzo IP esterno** eseguire le operazioni seguenti:
    
      - Se si è scelto di utilizzare un singolo FQDN e indirizzo IP per l'accesso SIP, il servizio Web Conferencing e il servizio A/V Edge, digitare l'indirizzo IPv6 esterno del server perimetrale in **Accesso SIP** .
    
      - Se non si è scelto di utilizzare un singolo FQDN e indirizzo IP per l'accesso SIP, il servizio Web Conferencing e il servizio A/V Conferencing, digitare l'indirizzo IPv6 scelto per il lato pubblico di questo server del pool di server perimetrali in **Accesso SIP** . In **Web Conferencing** digitare l'indirizzo IPv6 scelto per il lato pubblico di questo server del pool di server perimetrali. In **A/V Conferencing** digitare l'indirizzo IPv6 scelto per il lato pubblico di questo server del pool di server perimetrali.
    

    > [!NOTE]
    > Se non è stato scelto di abilitare e assegnare gli indirizzi IPv6, questa finestra di dialogo non viene visualizzata.



17. Fare clic su **Fine** .
    

    > [!NOTE]
    > Il primo server perimetrale creato nel pool verrà ora visualizzato nella finestra di dialogo <STRONG>Definire i computer nel pool corrente</STRONG> .



18. In **Definire i computer nel pool corrente** fare clic su **Aggiungi** e quindi ripetere i passaggi da 11 a 14 per il secondo server perimetrale che si desidera aggiungere al pool di server perimetrali.

19. Dopo aver ripetuto i passaggi da 11 a 14, fare clic su **Avanti** in **Definire i computer nel pool corrente** .
    

    > [!NOTE]
    > A questo punto, è possibile visualizzare entrambi i server perimetrali nel pool.



20. Se si è scelto di utilizzare NAT, viene visualizzata una finestra di dialogo. In **Indirizzo IP pubblico** digitare l'indirizzo IPv4 o IPv6 pubblico (come appropriato) da convertire tramite NAT e quindi fare clic su **Avanti** .
    

    > [!NOTE]
    > Tale indirizzo deve corrispondere all'indirizzo IP esterno di A/V Edge.



21. Nell'elenco **Pool hop successivo** in **Definire l'hop successivo** selezionare il nome del pool interno, che può essere un pool Front End o un pool Standard Edition. In alternativa, se la distribuzione include un server Director, selezionare il nome di questo server e quindi fare clic su **Avanti** .

22. In **Associare pool Front End** specificare uno o più pool interni, che possono includere pool Front End e server Standard Edition, da associare a questo server perimetrale, selezionando i nomi dei pool interni che utilizzeranno il server perimetrale per la comunicazione con gli utenti esterni supportati.
    

    > [!NOTE]
    > È possibile associare solo un pool di server perimetrali o un singolo server perimetrale con carico bilanciato a ogni pool interno per il traffico audio/video. Se è già stato associato un pool interno a un pool di server perimetrali o a un server perimetrale, viene visualizzato un avviso che indica che al pool interno è già associato un pool di server perimetrali o un server perimetrale. Se si seleziona un pool già associato a un altro server perimetrale, l'associazione verrà modificata.



23. Fare clic su **Fine** .

24. Pubblicare la topologia.

## Per definire la topologia per un pool di server perimetrali con bilanciamento del carico hardware

1.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.

2.  Nell'albero della console espandere il sito in cui si desidera distribuire i server perimetrali.

3.  Fare clic con il pulsante destro del mouse su **Pool di server perimetrali** e quindi scegliere **Nuovo pool di server perimetrali** .

4.  In **Definire il nuovo pool di server perimetrali** fare clic su **Avanti** .

5.  In **Definire l'FQDN del pool di server perimetrali** eseguire le operazioni seguenti:
    
      - In **FQDN** digitare il nome di dominio completo (FQDN) scelto per il lato interno del pool di server perimetrali.
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>Utilizzare solo caratteri standard, ovvero A-Z, a-z, 0-9 e trattini, per assegnare FQDN dei server Lync Server, dei server perimetrali e dei pool. Non utilizzare caratteri Unicode o di sottolineatura. La presenza di caratteri non standard in un FQDN è spesso non supportata da DNS esterni e CA pubbliche (quando l'FQDN deve essere assegnato al nome soggetto nel certificato). Per informazioni dettagliate sull'aggiunta di un suffisso DNS a un nome di computer, vedere Generatore di topologie.</td>
        </tr>
        </tbody>
        </table>
    
    <!-- end list -->
    
      - Fare clic su **Pool di più computer** e quindi su **Avanti** .

6.  In **Selezionare funzionalità** eseguire le operazioni seguenti:
    
      - Se si prevede di utilizzare un singolo FQDN e indirizzo IP per il servizio di accesso SIP, il servizio Web Conferencing di Lync Server e il servizio A/V Edge, selezionare la casella di controllo **Utilizzare FQDN e indirizzo IP singoli** .
    
      - Se si prevede di abilitare la federazione, selezionare la casella di controllo **Abilita la federazione per questo pool di server perimetrali (porta 5061)** .
        

        > [!NOTE]
        > È possibile selezionare questa opzione, ma è possibile pubblicare esternamente per la federazione solo un pool di server perimetrali o un server perimetrale nell'organizzazione. Tutto l'accesso da parte di utenti federati, inclusi gli utenti di messaggistica istantanea pubblica, passa per lo stesso pool di server perimetrali o singolo server perimetrale. Se, ad esempio, la distribuzione include un pool di server perimetrali o un singolo server perimetrale distribuito a New York e uno distribuito a Londra e si abilita il supporto per la federazione nel pool di server perimetrali o nel server perimetrale di New York, il traffico dei segnali per gli utenti federati passerà per il pool di server perimetrali o il singolo server perimetrale di New York. Ciò vale anche per le comunicazioni con gli utenti di Londra, anche se un utente interno di Londra che chiami un utente federato di Londra utilizzerà il pool o il server perimetrale di Londra per il traffico audio/video.

    
      - Se si prevede di supportare il protocollo XMPP per la distribuzione, selezionare la casella di controllo **Abilita la federazione XMPP (porta 5269)**

7.  Fare clic su **Avanti** .

8.  In **Selezionare le opzioni IP** eseguire le operazioni seguenti:
    
      - **Abilita IPv4 su interfaccia interna** : selezionare questa casella di controllo se si desidera applicare un indirizzo IPv4 all'interfaccia interna di server perimetrale o pool di server perimetrali
    
      - **Abilita IPv6 su interfaccia interna** : selezionare questa casella di controllo se si desidera applicare un indirizzo IPv6 all'interfaccia interna di server perimetrale o pool di server perimetrali
    
      - **Abilita IPv4 su interfaccia esterna** : selezionare questa casella di controllo se si desidera applicare un indirizzo IPv4 all'interfaccia esterna di server perimetrale o pool di server perimetrali
    
      - **Abilita IPv6 su interfaccia esterna** : selezionare questa casella di controllo se si desidera applicare un indirizzo IPv6 all'interfaccia esterna di server perimetrale o pool di server perimetrali
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><strong>Non</strong> selezionare la casella di controllo <strong>L'indirizzo IP esterno del pool di server perimetrali è convertito da NAT</strong> . Network Address Translation (NAT) non è supportato quando si utilizza il bilanciamento del carico di rete hardware.</td>
    </tr>
    </tbody>
    </table>


9.  In **FQDN esterni** eseguire le operazioni seguenti:
    
      - Se in **Selezionare funzionalità** si è scelto di utilizzare un singolo FQDN e indirizzo IP per l'accesso SIP, il servizio Web Conferencing e il servizio A/V Edge, digitare l'FQDN esterno in **Accesso SIP** .
        

        > [!NOTE]
        > Se si sceglie di selezionare questa opzione, è necessario specificare un numero di porta diverso per ogni servizio Edge (impostazioni di porta consigliate: 5061 per il servizio Access Edge, 444 per il servizio Web Conferencing Edge e 443 per il servizio A/V Edge). Selezionando questa opzione, è possibile evitare possibili problemi di connettività e semplificare la configurazione, in quanto è quindi possibile utilizzare lo stesso numero di porta, ad esempio 443, per i tre servizi.

    
      - Se in **Selezionare funzionalità** non si è scelto di utilizzare un singolo FQDN e indirizzo IP, digitare l'FQDN scelto per il lato pubblico del pool di server perimetrali in **Accesso SIP** . In **Web Conferencing** digitare l'FQDN scelto per il lato pubblico del pool di server perimetrali. In **Audio/Video** digitare l'FQDN scelto per il lato pubblico del pool di server perimetrali. Utilizzare le porte predefinite.
        

        > [!NOTE]
        > Questi saranno gli FQDN IP virtuali (VIP) del lato pubblico per il pool.



10. Fare clic su **Avanti** .

11. In **Definire i computer nel pool corrente** fare clic su **Aggiungi** .

12. In **Definire l'indirizzo IP esterno** eseguire le operazioni seguenti:
    
      - Se si è scelto di utilizzare un singolo FQDN e indirizzo IP per l'accesso SIP, il servizio Web Conferencing e il servizio A/V Edge, digitare l'indirizzo IPv4 esterno del server perimetrale in **Accesso SIP** e quindi fare clic su **Avanti** .
    
      - Se non si è scelto di utilizzare un singolo FQDN e indirizzo IP per l'accesso SIP, il servizio Web Conferencing e il servizio A/V Conferencing, digitare l'indirizzo IP scelto per il lato pubblico di questo server del pool di server perimetrali in **Accesso SIP** . In **Web Conferencing** digitare l'indirizzo IP scelto per il lato pubblico di questo server del pool di server perimetrali. In **A/V Conferencing** digitare l'indirizzo IP scelto per il lato pubblico di questo server del pool di server perimetrali.

13. Fare clic su **Avanti** .

14. Se è stato scelto di abilitare gli indirizzi IPv6, in **Definire l'indirizzo IP esterno** eseguire le operazioni seguenti:
    
      - Se si è scelto di utilizzare un singolo FQDN e indirizzo IP per l'accesso SIP, il servizio Web Conferencing e il servizio A/V Edge, digitare l'indirizzo IPv6 esterno del server perimetrale in **Accesso SIP** .
    
      - Se non si è scelto di utilizzare un singolo FQDN e indirizzo IP per l'accesso SIP, il servizio Web Conferencing e il servizio A/V Conferencing, digitare l'indirizzo IPv6 scelto per il lato pubblico di questo server del pool di server perimetrali in **Accesso SIP** . In **Web Conferencing** digitare l'indirizzo IPv6 scelto per il lato pubblico di questo server del pool di server perimetrali. In **A/V Conferencing** digitare l'indirizzo IPv6 scelto per il lato pubblico di questo server del pool di server perimetrali.
    

    > [!NOTE]
    > Se non è stato scelto di abilitare e assegnare gli indirizzi IPv6, questa finestra di dialogo non viene visualizzata.



15. Fare clic su **Fine** .
    

    > [!NOTE]
    > Il primo server perimetrale creato nel pool verrà ora visualizzato nella finestra di dialogo <STRONG>Definire i computer nel pool corrente</STRONG> .



16. In **Definire i computer nel pool corrente** fare clic su **Aggiungi** e quindi ripetere i passaggi da 11 a 14 per il secondo server perimetrale che si desidera aggiungere al pool di server perimetrali.

17. Dopo aver ripetuto i passaggi da 11 a 14, fare clic su **Avanti** in **Definire i computer nel pool corrente** .
    

    > [!NOTE]
    > A questo punto, è possibile visualizzare entrambi i server perimetrali nel pool.



18. Nell'elenco **Pool hop successivo** in **Definire l'hop successivo** selezionare il nome del pool interno, che può essere un pool Front End o un pool Standard Edition. In alternativa, se la distribuzione include un server Director, selezionare il nome di questo server e quindi fare clic su **Avanti** .

19. In **Associare pool Front End** specificare uno o più pool interni, che possono includere pool Front End e server Standard Edition, da associare a questo server perimetrale, selezionando i nomi dei pool interni che utilizzeranno il server perimetrale per la comunicazione con gli utenti esterni supportati.
    

    > [!NOTE]
    > È possibile associare solo un pool di server perimetrali o un singolo server perimetrale con carico bilanciato a ogni pool interno per il traffico audio/video. Se è già stato associato un pool interno a un pool di server perimetrali o a un server perimetrale, viene visualizzato un avviso che indica che al pool interno è già associato un pool di server perimetrali o un server perimetrale. Se si seleziona un pool già associato a un altro server perimetrale, l'associazione verrà modificata.



20. Fare clic su **Fine** .

21. Pubblicare la topologia.

