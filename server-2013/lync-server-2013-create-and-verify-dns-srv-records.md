---
title: 'Lync Server 2013: Creare e verificare record DNS SRV'
TOCTitle: Creare e verificare record DNS SRV
ms:assetid: 86888c7e-1401-458f-9a7b-08ac726deeec
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398680(v=OCS.15)
ms:contentKeyID: 49301211
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creare e verificare record DNS SRV in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

Per eseguire correttamente questa procedura, è necessario connettersi al server o al dominio almeno come membro del gruppo Domain Admins o DnsAdmins.

In questo argomento viene descritto come configurare i record DNS (Domain Name System) che è necessario creare nelle distribuzioni di Lync Server 2013 e quelli necessari per l'accesso automatico dei client. Quando si crea un pool Front End, tramite il programma di installazione vengono creati gli oggetti Active Directory e le impostazioni per il pool, tra cui il nome di dominio completo (FQDN) del pool. Oggetti e impostazioni simili vengono creati per un server Standard Edition. Per consentire ai client di connettersi al pool o al server Standard Edition, il nome di dominio completo del pool o del server Standard Edition deve essere registrato in DNS. È necessario creare record DNS SRV nel sistema DNS interno per ogni dominio SIP. Per questa procedura si presuppone che nel sistema DNS interno siano disponibili aree per i domini utente SIP.

## Per configurare un record DNS SRV

1.  Nel server DNS fare clic sul pulsante **Start** , scegliere **Strumenti di amministrazione** e quindi **DNS** .

2.  Nell'albero della console per il dominio SIP espandere **Zone di ricerca diretta** e quindi fare clic con il pulsante destro del mouse sul dominio SIP in cui verrà installato Lync Server 2013.

3.  Fare clic su **Altri nuovi record** .

4.  In **Selezionare tipo di record di risorsa** fare clic su **Posizione servizio (SRV)** e quindi su **Crea record** .

5.  Fare clic su **Servizio** e quindi digitare **\_sipinternaltls** .

6.  Fare clic su **Protocollo** e quindi digitare **\_tcp**.

7.  Fare clic su **Numero porta** e quindi digitare **5061**.

8.  Fare clic su **Host che offre questo servizio** e quindi digitare il nome di dominio completo del pool o del server Standard Edition.

9.  Scegliere **OK** , quindi su **Fine** .

## Per verificare la creazione di un record DNS SRV

1.  Accedere a un computer client nel dominio con un account membro del gruppo Authenticated Users o con autorizzazioni equivalenti.

2.  Fare clic sul pulsante **Start** e quindi scegliere **Esegui** .

3.  Nella casella **Apri** digitare **cmd** e quindi fare clic su **OK** .

4.  Al prompt dei comandi digitare **nslookup** e quindi premere INVIO.

5.  Digitare **set type=srv** e quindi premere INVIO.

6.  Digitare **\_sipinternaltls.\_tcp.contoso.com** e quindi premere INVIO. L'output visualizzato per il record TSL (Transport Layer Security) è il seguente:
    
    Server: *\<server dns\>* .contoso.com
    
    Indirizzo: *\<Indirizzo IP del server\>*
    
    Risposta da un server non autorevole:
    
    percorso servizio SRV \_sipinternaltls.\_tcp.contoso.com:
    
    priorità = 0
    
    peso = 0
    
    porta = 5061
    
    nome host svr = poolname.contoso.com (o record A server Standard Edition)
    
    poolname.contoso.com indirizzo internet = *\<indirizzo IP virtuale del servizio di bilanciamento del carico\>* o *\<indirizzo IP di un singolo Server Enterprise per pool con un solo Server Enterprise\>* o *\<indirizzo IP del server Standard Edition server\>*

7.  Al termine, digitare **exit** al prompt dei comandi e quindi premere INVIO.

## Per verificare che il nome di domino completo del pool Front End o del server Standard Edition possa essere risolto

1.  Eseguire l'accesso a un computer client nel dominio.

2.  Fare clic sul pulsante **Start** e quindi scegliere **Esegui** .

3.  Nella casella **Apri** digitare **cmd** e quindi fare clic su **OK** .

4.  Al prompt dei comandi digitare **nslookup** *\<FQDN del pool Front End\>* o *\<FQDN del server Standard Edition\>* e quindi premere INVIO.

5.  Verificare di ricevere una risposta che si risolve nell'indirizzo IP appropriato per l'FQDN.

