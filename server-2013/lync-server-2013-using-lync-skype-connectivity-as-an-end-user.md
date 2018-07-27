---
title: 'Lync Server 2013: Uso della connettività Lync-Skype come utente finale'
TOCTitle: Uso della connettività Lync-Skype come utente finale
ms:assetid: ad22f731-118c-4349-8790-b1a72941cbdd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn440175(v=OCS.15)
ms:contentKeyID: 59602744
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Uso della connettività Lync-Skype in Lync Server 2013 come utente finale

 

_**Ultima modifica dell'argomento:** 2014-12-05_

La connettività Lync-Skype consente agli utenti di Skype e a quelli di Lync di aggiungersi a vicenda come contatti, scambiarsi messaggi istantanei ed effettuare chiamate audio e video. Quando un utente di Skype aggiunge un utente di Lync, crea un contatto in Skype che contiene l'URI (Uniform Resource Identifier) SIP (Session Initiation Protocol) dell'utente di Lync. Al contrario, quando un utente di Lync aggiunge un contatto di Skype, l'utente di Lync crea un contatto in Lync che contiene l'account Microsoft (MSA), e non il nome utente, dell'utente di Skype.

**Cos'è un MSA?** Per comunicare con i contatti di Lync, gli utenti di Skype devono accedere a Skype con un account Microsoft (precedentemente denominato Windows Live ID). Un account Microsoft è costituito dalla combinazione di un indirizzo di posta elettronica e una password, che possono essere usati anche per accedere a servizi come la tecnologia di archiviazione Microsoft OneDrive, Windows Phone, il servizio di giochi online Microsoft Xbox LIVE e il client di messaggistica e collaborazione Microsoft Outlook (e, in passato, il servizio di posta elettronica basato sul Web Microsoft Hotmail o Windows Live Messenger). Se si usa un indirizzo di posta elettronica e una password per accedere a questi o ad altri servizi, si dispone già di un account Microsoft. Per informazioni dettagliate sulla creazione di un account Microsoft, vedere la relativa pagina di registrazione all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=306061](http://go.microsoft.com/fwlink/p/?linkid=306061). È possibile unire l'account di Skype con l'account Microsoft per il Single Sign-On in un'ampia varietà di applicazioni e servizi. In seguito all'unione dell'account, un utente di Skype può inviare richieste di contatto agli utenti di Lync.

> [!IMPORTANT]  
> Perché gli utenti di Lync e quelli di Skype possano comunicare in modo completo, devono essere soddisfatti i requisiti seguenti:<ul><li><p>Gli utenti di Skype devono avere effettuato l'accesso al client di Skype con un account Microsoft (MSA).</p></li>
> <li><p>L'amministratore di Lync deve abilitare gli utenti di Lync per la connettività per messaggistica istantanea pubblica.</p></li>
> <li><p>Quando un utente di Skype aggiunge un contatto di Lync, verificare che la parola Lync compaia sotto il nome del contatto, a indicare che è stato trovato un URI Lync.</p></li>
> 
> <li><p>Quando un utente di Skype aggiunge un contatto di Lync e non vengono restituiti risultati di ricerca per quel dominio di Lync, è possibile che il processo di provisioning PIC non sia stato completato o che il dominio di Lync non sia stato configurato.</p></li>
> 
> 
> <li><p>A seconda delle impostazioni di privacy degli utenti di Lync e di Skype, è possibile che le funzionalità di messaggistica istantanea, video e presenza non siano disponibili finché i nuovi contatti non vengono accettati da ogni utente.</p></li></ul>


**Per aggiungere un contatto di Skype a Lync 2013**

1.  In Lync fare clic su **Aggiungi contatto, Aggiungi contatto esterno all'organizzazione**.

2.  Nell'elenco dei provider di contatti selezionare **Skype**, come illustrato di seguito.
    
    ![Aggiunta di un contatto di Skype nel client Lync](images/Dn440175.ac4e2f21-c1d9-47d8-b99e-d49fe4eb36d7(OCS.15).jpg "Aggiunta di un contatto di Skype nel client Lync")

3.  Nel campo **Indirizzo di messaggistica istantanea** immettere l'account Microsoft (MSA) dell'utente di Skype.

4.  Nell'elenco a discesa **Aggiungi al gruppo di contatti** selezionare un gruppo di contatti a cui aggiungere l'utente.

5.  Nell'elenco a discesa **Impostare la relazione di privacy** selezionare l'impostazione del contatto appropriata e fare clic su **OK**.

6.  L'utente appare ora come contatto in Lync. Selezionarlo, fare clic con il pulsante destro del mouse sul nome utente e quindi scegliere **Visualizza scheda contatto** per visualizzare le proprietà dell'utente. Come mostra l'immagine sotto, è possibile anche fare clic su **Chiama** e quindi su **Chiamata Lync** per stabilire una chiamata audio o video con il nuovo utente di Skype aggiunto.
    
    ![Avvio di una chiamata a un contatto nel client Lync](images/Dn440175.cd7cb21a-87f7-4bfa-b30c-980d4098d226(OCS.15).jpg "Avvio di una chiamata a un contatto nel client Lync")

Per altre informazioni sul supporto per i contatti, vedere [Aggiungere un contatto in Lync](http://office.microsoft.com/it-it/office365-lync-online-help/add-a-contact-in-lync-ha102828922.aspx) e [Aggiungere un contatto esterno in Lync](http://office.microsoft.com/it-it/office365-lync-online-help/add-an-external-contact-in-lync-ha104038998.aspx?ctt=5%26origin=ha102828922)

Quando l'account Microsoft di un utente di Skype usa un nome di dominio personalizzato, ad esempio <strong>guido@contoso.com</strong>, l'utente di Lync può aggiungere l'account Microsoft a Lync in due modi:

1.  Usando l'icona **Aggiungi contatto** oppure

2.  Usando il campo **Trovare un contatto o una chat room oppure comporre un numero**.

In ogni istanza, l'utente di Lync deve inserire l'indirizzo di posta elettronica dell'utente di Skype nel formato seguente: <strong>utente(nome di dominio)@msn.com</strong>.

> [!IMPORTANT]  
> Questa operazione non è necessaria per gli account Microsoft che usano i nomi di dominio seguenti: <strong>@live.com, @hotmail.com o @outlook.com</strong>. Per altre informazioni sui nomi di dominio personalizzati supportati, vedere <a href="http://support.microsoft.com/kb/897567">Domini di messaggistica istantanea pubblica supportati</a>.

**Per aggiungere un contatto di Skype a Lync quando si usa un nome di dominio personalizzato**

1.  In Lync fare clic su **Aggiungi contatto, Aggiungi contatto esterno all'organizzazione**.

2.  Nell'elenco dei provider di contatti selezionare **Skype**, come illustrato di seguito.
    
    ![Aggiunta di un contatto di Skype nel client Lync](images/Dn440175.ac4e2f21-c1d9-47d8-b99e-d49fe4eb36d7(OCS.15).jpg "Aggiunta di un contatto di Skype nel client Lync")

3.  Nel campo **Indirizzo di messaggistica istantanea** immettere l'account Microsoft (MSA) dell'utente di Skype nel formato <strong>utente(nome di dominio)@msn.com</strong>. Per l'utente guido@contoso.com immettere quindi <strong>guido(contoso.com)@msn.com</strong>, come illustrato di seguito.
    
    ![Impostazioni del nuovo contatto del client Lync](images/Dn440175.422e69b5-2c0c-4260-858f-f10309af772f(OCS.15).jpg "Impostazioni del nuovo contatto del client Lync")

4.  Nell'elenco a discesa **Aggiungi al gruppo di contatti** selezionare un gruppo di contatti a cui aggiungere l'utente.

5.  Nell'elenco a discesa **Impostare la relazione di privacy** selezionare l'impostazione del contatto appropriata e fare clic su **OK**.

6.  Un utente di Lync può inoltre usare il campo **Trovare un contatto o una chat room oppure comporre un numero** in Lync e aggiungere un indirizzo nel formato <strong>utente(nome di dominio)@msn.com</strong>. Per l'account Microsoft guido@contoso.com il formato sarà quindi <strong>guido(contoso.com)@msn.com</strong>, come illustrato di seguito.
    
    ![Ricerca di un contatto nel client Lync](images/Dn440175.69787db8-f9b9-49e5-b197-b90b10393301(OCS.15).jpg "Ricerca di un contatto nel client Lync")

7.  Eseguire i passaggi 4 e 5 di questa procedura per aggiungere il contatto a un gruppo di contatti e per selezionare la relazione di privacy appropriata.

**Per aggiungere un contatto di Lync a Skype**

1.  Accedere a Skype. L'utente di Skype deve avere effettuato l'accesso al client di Skype con un account Microsoft (MSA).
    
    ![Pagina di accesso al client Skype](images/Dn440175.b4fd7c5a-be35-4205-80c7-872863b7a91d(OCS.15).jpg "Pagina di accesso al client Skype")

2.  Selezionare l'icona Aggiungi contatti.

3.  Immettere l'URI SIP dell'utente di Lync, ad esempio guido@contoso.com.

4.  Quando Skype trova la corrispondenza nei risultati della ricerca, cercare la parola **Lync** sotto il nome dell'utente di Lync. La presenza della parola Lync indica che Skype ha individuato correttamente l'URI SIP del client Lync. Fare clic sul nome.
    
    ![Client Skype con contatto di Lync](images/Dn440175.4e690a72-1a54-4442-89cf-0fb45ac5f56a(OCS.15).jpg "Client Skype con contatto di Lync")

5.  Nell'angolo in alto a destra delle finestra fare clic su Aggiungi a contatti.

6.  Il nuovo contatto è ora aggiunto all'elenco contatti, ma al posto dell'icona di stato viene visualizzato un punto interrogativo finché il contatto non accetta la richiesta. Quando il nuovo contatto accetta la richiesta, sarà possibile vedere quando è online, iniziare conversazioni di messaggistica istantanea ed effettuare chiamate audio e video.
    
    ![Conversazione di messaggistica istantanea del client Skype con un contatto di Lync](images/Dn440175.86ca6f81-4db9-45ba-8511-1f7541aaf066(OCS.15).jpg "Conversazione di messaggistica istantanea del client Skype con un contatto di Lync")
    
    > [!IMPORTANT]  
    > L'amministratore di Lync Server deve configurare le impostazioni dei criteri dell'utente di Lync per consentire le richieste in arrivo, altrimenti l'utente di Lync non riceverà le richieste di contatto dall'utente di Skype. In base alla configurazione delle impostazioni dei criteri dell'utente di Lync, la richiesta di aggiungere l'utente di Skype viene visualizzata nella scheda <strong>Nuovo</strong> del client Lync. Per iniziare a comunicare con l'utente di Skype, l'utente di Lync deve aggiungere l'utente di Skype all'elenco Preferiti o a un elenco contatti. L'immagine seguente mostra la posizione della scheda <strong>Nuovo</strong> nel client Lync.    
    ![Pagina Nuovi contatti del client Lync](images/Dn440175.b1cf8570-1401-47d9-ab14-b04f0d7e8a7a(OCS.15).jpg "Pagina Nuovi contatti del client Lync")

Un utente di Lync deve configurare gli avvisi di Lync per poter visualizzare e individuare le richieste inviate da un utente di Skype. Per configurare gli avvisi di Lync, completare la procedura seguente.

**Per configurare gli avvisi di Lync**

1.  Nel client Lync fare clic sull'icona **Opzioni**.

2.  Selezionare **Avvisi**.

3.  In **Avvisi generali** selezionare **Avvisa quando qualcuno aggiunge l'utente corrente al proprio elenco contatti**.

4.  In **Contatti che non usano Lync** selezionare **Consenti gli inviti ma blocca tutte le altre comunicazioni**.

5.  Fare clic su **OK** per chiudere la finestra Opzioni.

![Finestra di dialogo Opzioni del client Lync - Pagina Avvisi](images/Dn440175.b36ed67f-f394-4f66-b60a-b74793001bfc(OCS.15).jpg "Finestra di dialogo Opzioni del client Lync - Pagina Avvisi")

