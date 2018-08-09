---
title: "Lync Server 2013: Config. certif. nel server di messaggistica di MS Exchange Server"
TOCTitle: "Lync Server 2013: Config. certif. nel server di messaggistica di MS Exchange Server"
ms:assetid: 74c883b4-cef6-41a9-b2eb-7212be32fea4
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398564(v=OCS.15)
ms:contentKeyID: 49300991
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare i certificati nel server che esegue la messaggistica unificata di Microsoft Exchange Server

 

_**Ultima modifica dell'argomento:** 2012-09-26_

Se è stata distribuita la Messaggistica unificata di Exchange, come descritto in [Pianificazione dell'integrazione della messaggistica unificata di Exchange in Lync Server 2013](lync-server-2013-planning-for-exchange-unified-messaging-integration.md) nella documentazione relativa alla pianificazione, e si desidera offrire caratteristiche di Messaggistica unificata di Exchange agli utenti VoIP aziendale nell'organizzazione, è possibile utilizzare le procedure seguenti per configurare il certificato nel server che esegue la Messaggistica unificata di Exchange.

> [!IMPORTANT]  
> Per i certificati interni, sia i server che eseguono Lync Server 2013 sia quelli che eseguono Microsoft Exchange devono disporre di certificati di un autorità radice attendibile reciprocamente attendibili. L'autorità di certificazione può essere la stessa o una diversa purché il certificato radice dell'autorità di certificazione dei server sia registrato nell'archivio certificati dell'autorità radice attendibile.

Exchange Server deve essere configurato con un certificato del server per connettersi a Lync Server 2013:

1.  Scaricare il certificato CA per Exchange Server.

2.  Installare il certificato CA per Exchange Server.

3.  Verificare che la CA sia inclusa nell'elenco delle CA radice attendibili di Exchange Server.

4.  Creare una richiesta di certificato per Exchange Server e installare il certificato.

5.  Assegnare il certificato per Exchange Server.

## Per scaricare il certificato CA

1.  Nel server che esegue la Messaggistica unificata di Exchange fare clic sul pulsante **Start**, scegliere **Esegui**, digitare **http://\<nome server CA emittente\>/certsrv** e quindi fare clic su **OK**.

2.  In **Selezionare un'attività** fare clic su **Scarica un certificato CA, la catena di certificati o un CRL**.

3.  In **Scarica un certificato CA, la catena di certificati o un CRL** selezionare **Metodo di codifica Base 64** e quindi fare clic su **Scarica certificato CA**.
    

    > [!NOTE]
    > In questo passaggio è possibile specificare anche la codifica DER (Distinguished Encoding Rules). Se si seleziona la codifica DER, il tipo di file nel prossimo passaggio e nel passaggio 10 di <STRONG>Per installare il certificato CA</STRONG> è .p7b anziché .cer.



4.  Nella finestra di dialogo **Download file** fare clic su **Salva** e quindi salvare il file nel disco rigido del server. Il file avrà estensione cer o p7b, a seconda della codifica selezionata nel passaggio precedente.

## Per installare il certificato CA

1.  Nel server che esegue la Messaggistica unificata di Exchange aprire Microsoft Management Console (MMC). A tale scopo, fare clic sul pulsante **Start**, scegliere **Esegui**, digitare **mmc** nella casella **Apri** e quindi fare clic su **OK**.

2.  Scegliere **Aggiungi/Rimuovi snap-in** dal menu **File** e quindi fare clic su **Aggiungi**.

3.  Nella casella **Aggiungi snap-in autonomo** fare clic su **Certificati** e quindi su **Aggiungi**.

4.  Nella finestra di dialogo **Snap-in certificati** fare clic su **Account del computer** e quindi su **Avanti**.

5.  Nella finestra di dialogo **Seleziona computer** assicurarsi che la casella di controllo **Computer locale (il computer su cui è in esecuzione questa console)** sia selezionata e quindi fare clic su **Fine**.

6.  Fare clic su **Chiudi** e quindi su **OK**.

7.  Nell'albero della console espandere **Certificati (computer locale)**, espandere **Autorità di certificazione radice attendibili** e quindi fare clic su **Certificati**.

8.  Fare clic con il pulsante destro del mouse su **Certificati**, scegliere **Tutte le attività** e quindi **Importa**.

9.  Fare clic su **Avanti**.

10. Fare clic su **Sfoglia** per individuare il file e quindi fare clic su **Avanti**. Il file avrà estensione cer o p7b, a seconda della codifica selezionata nel passaggio 3 di **Per scaricare il certificato CA**.

11. Fare clic su **Mettere tutti i certificati nel seguente archivio**.

12. Fare clic su **Sfoglia** e quindi selezionare **Autorità di certificazione radice attendibili**.

13. Fare clic su **Avanti** per verificare le impostazioni e quindi fare clic su **Fine**.

## Per verificare che la CA sia inclusa nell'elenco delle CA radice attendibili

1.  Nel server che esegue la Messaggistica unificata di Exchange in MMC espandere **Certificati (computer locale)**, espandere **Autorità di certificazione radice attendibili** e quindi fare clic su **Certificati**.

2.  Nel riquadro dei dettagli verificare che la CA sia inclusa nell'elenco delle CA attendibili.

## Per configurare la messaggistica unificata di Exchange Server 2013 con Lync Server

1.  Per informazioni dettagliate, vedere "Integrazione della messaggistica unificata di Exchange 2013 con Lync Server" nella documentazione di Exchange Server all'indirizzo [http://go.microsoft.com/fwlink/?linkid=265372\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=265372%26clcid=0x410).

## Per creare una richiesta di certificato e installare il certificato in Exchange Server 2007 (SP1)

1.  Nel server che esegue la Messaggistica unificata di Exchange, fare clic sul pulsante **Start**, scegliere **Esegui**, digitare **http://\<***nome del server CA emittente***\>/certsrv** e quindi fare clic su **OK**.

2.  In **Selezionare un'attività** fare clic su **Richiedi un certificato**.

3.  In **Richiedi un certificato** fare clic su **Richiesta avanzata di certificati**.

4.  In **Richiesta avanzata certificati** fare clic su **Creare e inviare una richiesta a questa CA**.

5.  In **Richiesta avanzata di certificati** selezionare **Server Web** o un altro modello di certificato server configurato per l'autenticazione server.

6.  In **Dati di identificazione per modello non in linea** digitare il nome di dominio completo (FQDN) di Exchange Server nella casella **Nome**.
    

    > [!NOTE]
    > È necessario immettere l'FQDN di Exchange Server per garantire il funzionamento delle comunicazioni.



7.  In **Opzioni chiave** selezionare la casella di controllo **Archivia certificato nell'archivio certificati del computer locale**.

8.  Fare clic sul pulsante **Invia** nella parte inferiore della pagina Web.

9.  Nella finestra di dialogo visualizzata in cui viene richiesto di confermare l'operazione, fare clic su **Sì**.

10. Nella pagina Certificato emesso fare clic su **Installa questo certificato** in **Certificato emesso**.

11. Nella finestra di dialogo visualizzata in cui viene richiesto di confermare l'operazione, fare clic su **Sì**.

12. Verificare che venga visualizzato il messaggio indicante il completamento dell'installazione del nuovo certificato.

## Per creare un certificato in Exchange Server 2010

1.  Accedere al server che esegue la Messaggistica unificata di Exchange con diritti utente appropriati. Per informazioni dettagliate, vedere "Autorizzazioni di accesso client" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=195499\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=195499%26clcid=0x410).

2.  Per creare il certificato, fare riferimento alle procedure seguenti:
    
    1.  "Creazione di un nuovo certificato di Exchange" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=195494\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=195494%26clcid=0x410)
    
    2.  "Importazione di un certificato di Exchange" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=195496\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=195496%26clcid=0x410)
    

    > [!NOTE]
    > Per l'opzione <STRONG>Nome soggetto</STRONG> del certificato, è necessario immettere l'FQDN di Exchange Server per garantire il funzionamento delle comunicazioni.



## Per assegnare il certificato in Exchange Server 2007 (SP1)

1.  Nel server che esegue la Messaggistica unificata di Exchange aprire MMC.

2.  Nell'albero della console espandere **Personale** e quindi fare clic su **Certificati**.

3.  Nel riquadro dei dettagli verificare che il certificato personale sia visualizzato.

4.  Fare doppio clic sul certificato per leggerne i dettagli e assicurarsi che sia valido.
    

    > [!NOTE]
    > Prima che il certificato venga visualizzato come valido potrebbero essere necessari alcuni minuti.



5.  Riavviare il servizio di messaggistica unificata di Microsoft Exchange.
    

    > [!NOTE]
    > Il certificato corretto viene automaticamente recuperato dal server che esegue la messaggistica unificata di Exchange Server 2007 SP1.



6.  Aprire il Visualizzatore eventi e cercare l'ID evento 1112, che specifica il certificato recuperato dal server che esegue la messaggistica unificata di Exchange Server 2007 SP1.

## Per assegnare il certificato in Exchange Server 2010

1.  Accedere al server che esegue la Messaggistica unificata di Exchange con diritti utente appropriati. Per informazioni dettagliate, vedere "Autorizzazioni di accesso client" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=195499\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=195499%26clcid=0x410).

2.  Per la procedura di assegnazione del certificato, vedere "Assegnazione dei servizi ad un certificato" all'indirizzo [http://go.microsoft.com/fwlink/?linkid=195497\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=195497%26clcid=0x410).

