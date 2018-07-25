---
title: 'Lync Server 2013: Definire topologie con server Director facoltativi nella topologia'
TOCTitle: Definire topologie con server Director facoltativi nella topologia
ms:assetid: 8e9a659d-23b0-401d-b296-59c7df414d49
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398717(v=OCS.15)
ms:contentKeyID: 49301283
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definire topologie con server Director facoltativi nella topologia per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-08_

I server Director Lync Server 2013 possono essere server a istanza singola oppure possono essere installati come pool di più server Director con bilanciamento del carico per garantire disponibilità e capacità maggiori. Sono supportati sia il bilanciamento del carico hardware che il bilanciamento del carico DNS (Domain Name System). In questo argomento viene illustrato come configurare il bilanciamento del carico DNS per i pool di server Director.

Per pubblicare, abilitare o disabilitare correttamente una topologia quando si aggiunge o si rimuove un ruolo server, è necessario accedere come utente membro dei gruppi **RTCUniversalServerAdmins** e **Domain Admins** . È inoltre possibile delegare i diritti di amministratore e le autorizzazioni appropriate per l'aggiunta di ruoli del server. Per informazioni dettagliate, vedere [Delegare le autorizzazioni di installazione in Lync Server 2013](lync-server-2013-delegate-setup-permissions.md) nella documentazione relativa alla distribuzione del server Standard Edition o Enterprise Edition. Per poter apportare altre modifiche relative alla configurazione, è necessaria solo l'appartenenza al gruppo **RTCUniversalServerAdmins** .

In questo argomento vengono descritti i passaggi necessari per definire e pubblicare la topologia relative a due topologie di Server Director:

  - Per definire il Director (istanza singola)

  - Per definire il Director (pool di più server Director)

## Per definire il Director (istanza singola)

1.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.

2.  Nella pagina di benvenuto fare clic su **Scarica topologia dalla distribuzione esistente** .

3.  Nella finestra di dialogo **Salva topologia con nome** digitare il nome e il percorso della copia locale della topologia esistente e quindi fare clic su **Salva** .

4.  Espandere il sito in cui si intende aggiungere il Director, fare clic con il pulsante destro del mouse su **Pool di server Director** e quindi fare clic su **Nuovo pool di server Director** .

5.  Nella finestra di dialogo **Definire l'FQDN del pool di server Director** eseguire le operazioni seguenti:
    
      - In **FQDN pool** digitare l'FQDN del pool di server Director.
    
      - Fare clic su **Pool computer singolo** e quindi fare clic su **Avanti** .

6.  Nella finestra di dialogo **Definire condivisione file** eseguire una delle operazioni seguenti:
    
    1.  Per usare una condivisione file esistente, fare clic su **Utilizza condivisione file definita in precedenza** , selezionare una condivisione file nell'elenco e quindi fare clic su **Avanti** .
    
    2.  Per creare una nuova condivisione file, fare clic su **Definisci nuova condivisione file** , digitare l'FQDN del percorso della condivisione file in **FQDN file server** , digitare il nome della condivisione in **Condivisione file** e quindi fare clic su **Avanti** .
    
    > [!important]  
    > La condivisione file specificata o creata in questo passaggio deve esistere o essere creata prima della pubblicazione della topologia.<br />    La condivisione file assegnata a un Director non viene usata effettivamente, pertanto è possibile assegnare la condivisione file di qualsiasi pool nell'organizzazione.

7.  Nella finestra di dialogo **Specificare l'URL dei servizi Web** , in **URL di base esterno** , specificare l'FQDN dei Director e quindi fare clic su **Fine** .
    
    > [!important]  
    > Il nome deve essere risolvibile dai server DNS Internet e puntare all'indirizzo IP pubblico del proxy inverso, che resta in attesa delle richieste HTTP/HTTPS a tale URL e le trasmette tramite proxy alla directory virtuale dei servizi Web esterni in tale Director.    

    > [!WARNING]
    > Se si hanno più pool Front End o Front End Server, l'FQDN dei servizi Web esterni deve essere univoco. Ad esempio, se si definisce l'FQDN dei servizi Web esterni di un Front End Server come <STRONG>pool01.contoso.com</STRONG>, non sarà possibile utilizzare <STRONG>pool01.contoso.com</STRONG> per un altro pool Front End o Front End Server. Se si distribuisce anche Director, l'FQDN dei servizi Web definito per ciascun Server Director o pool di server Director deve essere univoco rispetto agli altri Server Director o pool di server Director, e univoco anche rispetto agli altri pool Front End e Front End Server. Se si decide di sostituire i servizi Web interni con un FQDN definito autonomamente, ciascun FQDN deve essere diverso da quello degli altri pool Front End, Server Director o pool di server Director.



8.  Pubblicare la topologia.

## Per definire il Director (pool di più server Director)

1.  Avviare Generatore di topologie: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Generatore di topologie**.

2.  Nella pagina di benvenuto fare clic su **Scarica topologia dalla distribuzione esistente** .

3.  Nella finestra di dialogo **Salva topologia con nome** digitare il nome e il percorso della copia locale della topologia esistente e quindi fare clic su **Salva** .

4.  Espandere il sito in cui si intende aggiungere il Director, fare clic con il pulsante destro del mouse su **Pool di server Director** e quindi fare clic su **Nuovo pool di server Director** .

5.  Nella finestra di dialogo **Definire l'FQDN del pool di server Director** eseguire le operazioni seguenti:
    
      - In **FQDN pool** digitare l'FQDN del pool di server Director.
    
      - Fare clic su **Pool di più computer** e quindi su **Avanti** .

6.  Nella finestra di dialogo **Definire i computer nel pool corrente** eseguire le operazioni seguenti:
    
      - Specificare l'FQDN del computer del primo membro del pool e quindi fare clic su **Aggiungi** .
    
      - Ripetere il passaggio precedente per ogni computer da aggiungere. Al termine, fare clic su **Avanti** .

7.  Nella finestra di dialogo **Definire condivisione file** eseguire una delle operazioni seguenti:
    
      - Per usare una condivisione file esistente, fare clic su **Utilizza condivisione file definita in precedenza** , selezionare una condivisione file nell'elenco e quindi fare clic su **Avanti** .
    
      - Per creare una nuova condivisione file, fare clic su **Definisci nuova condivisione file** , digitare l'FQDN del percorso della condivisione file in **FQDN file server** , digitare il nome della condivisione in **Condivisione file** e quindi fare clic su **Avanti** .
    
    > [!important]  
    > La condivisione file specificata o creata in questo passaggio deve esistere o essere creata prima della pubblicazione della topologia.<br />    La condivisione file assegnata a un Director non viene usata effettivamente, pertanto è possibile assegnare la condivisione file di qualsiasi pool nell'organizzazione.

8.  Nella finestra di dialogo **Specificare l'URL dei servizi Web** , in **URL di base esterno** , specificare l'FQDN dei Director e quindi fare clic su **Fine** .
    
    > [!important]  
    > Il nome deve essere risolvibile dai server DNS Internet e puntare all'indirizzo IP pubblico del proxy inverso che è in attesa delle richieste HTTP/HTTPS inviate a tale URL e le trasmette mediante proxy alla directory virtuale dei Servizi Web esterni su tale pool di server Director.    

    > [!WARNING]
    > Se si hanno più pool Front End o Front End Server, l'FQDN dei servizi Web esterni deve essere univoco. Ad esempio, se si definisce l'FQDN dei servizi Web esterni di un Front End Server come <STRONG>pool01.contoso.com</STRONG>, non sarà possibile utilizzare <STRONG>pool01.contoso.com</STRONG> per un altro pool Front End o Front End Server. Se si distribuisce anche Director, l'FQDN dei servizi Web definito per ciascun Server Director o pool di server Director deve essere univoco rispetto agli altri Server Director o pool di server Director, e univoco anche rispetto agli altri pool Front End e Front End Server. Se si decide di sostituire i servizi Web interni con un FQDN definito autonomamente, ciascun FQDN deve essere diverso da quello degli altri pool Front End, Server Director o pool di server Director.



9.  Pubblicare la topologia.

