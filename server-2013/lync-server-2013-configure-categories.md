---
title: 'Lync Server 2013: Configurare le categorie'
TOCTitle: Configurare le categorie
ms:assetid: 4547f514-f0c0-404d-890f-092ddeeac852
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204859(v=OCS.15)
ms:contentKeyID: 49300379
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare le categorie in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-06_

Nel Pannello di controllo di Lync Server 2013 è possibile utilizzare la sezione **Categoria** della pagina **Chat persistente** per configurare le categorie. Una categoria di chat Chat persistente è una struttura logica per l'organizzazione di chat room. Una categoria definisce un insieme predefinito di elenchi di controllo di accesso per il controllo degli utenti e dei gruppi di utenti che possono creare chat room o prendervi parte. Le categorie possono essere usate per applicare gli ethical wall tra le varie suddivisioni all'interno delle organizzazioni.

Le categorie di chat room possono contenere chat room, ma non altre categorie. Ogni categoria descrive il relativo contenuto con metadati, come *Nome* e *Descrizione* . La categoria presenta inoltre proprietà che possono essere impostate per controllare il comportamento delle chat room ad essa appartenenti, ad esempio se consentono *Inviti* o *Caricamenti file* oppure contengono *Cronologia chat* .

## Per configurare le categorie delle chat room

1.  Da un account utente assegnato al ruolo CsPersistentChatAdministrator o CsAdministrator, accedere a un qualsiasi computer nella distribuzione interna.

2.  Dal menu **Start** selezionare il Pannello di controllo di Lync Server o aprire una finestra del browser e quindi immettere l'URL di amministrazione. Per informazioni dettagliate sui diversi metodi utilizzabili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).
    
    > [!important]  
    > È inoltre possibile usare i cmdlet di Windows PowerShell. Per informazioni dettagliate, vedere <a href="configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md">Configurazione del server Chat persistente tramite i cmdlet di Windows PowerShell</a> nella documentazione relativa alla distribuzione.

3.  Nella barra di spostamento sinistra fare clic su **Chat persistente** e quindi su **Categoria** .
    
    Per più distribuzioni di pool di server Chat persistente, selezionare il pool appropriato dall'elenco a discesa.

4.  Nella pagina **Categoria** fare clic su **Nuovo** o **Modifica** .

5.  In **Seleziona un servizio** selezionare il servizio corrispondente al pool di server Chat persistente in cui deve essere creata la categoria. Il servizio è il pool server Chat persistente utilizzato da Chat persistente (client) per identificare la categoria cui appartiene il pool. Una categoria può appartenere a un solo pool di server Chat persistente e non può essere spostata in un altro o condivisa con un altro pool.

6.  In **Nuova categoria** eseguire le operazioni seguenti:
    
    1.  In **Nome** specificare un nome per la nuova categoria di chat.
    
    2.  In **Descrizione** fornire una descrizione dettagliata della categoria di chat, ad esempio una categoria di chat per Contoso.
    
    3.  Per specificare se è possibile abilitare inviti per le chat room appartenenti a questa categoria, selezionare o deselezionare la casella di controllo **Abilita inviti** . Se selezionata, è possibile attivare o disattivare gli inviti per le chat di questa categoria. Se deselezionata, per le chat di questa categoria non sono consentiti inviti. Se per una chat sono attivati gli inviti, quando si aggiunge un membro, questi riceve una notifica della nuova chat nel relativo client Chat persistente.
    
    4.  Per controllare i caricamenti file nelle chat room che appartengono a questa categoria, selezionare o deselezionare la casella di controllo **Abilita caricamento file** . Se selezionata, per le chat di questa categoria è possibile abilitare o disabilitare i caricamenti file. Se deselezionata, per le chat di questa categoria non sono consentiti caricamenti file.
        
        > [!important]  
        > Questa impostazione viene applicata sul server in quanto le applicazioni personalizzate o i client Group Chat precedenti che usano Office Communications Server 2007 R2Group Chat Server o Lync Server 2010, Group Chat possono inviare file a una chat. Il client Lync 2013 non dispone di una funzionalità di caricamento/download dei file. Pertanto, nel caso di una distribuzione di Lync 2013 pura o di un client Lync 2013, non è possibile inviare file a una chat room di server Chat persistente.    
    5.  Per controllare la cronologia chat, selezionare o deselezionare la casella di controllo **Abilita cronologia chat** . Se selezionata, le chat room diventano permanenti. In caso contrario, i messaggi delle chat non vengono memorizzati. Se è abilitata la conformità, le chat room vengono salvate in conformità, ma gli utenti non potranno accedere ai messaggi più vecchi. Questa opzione può essere usata per le chat progettate per collaborazioni ad hoc in tempo reale che non richiedono la memorizzazione permanente della cronologia chat.

7.  In **Modifica categoria** eseguire le operazioni seguenti:
    
      - In **Appartenenza** , nella sezione **Membri consentiti** aggiungere o rimuovere utenti e altre entità Servizi di dominio Active Directory (utenti, gruppi di distribuzione, unità organizzative e così via) di cui è consentita l'aggiunta come membri delle chat room appartenenti alla categoria. Le entità consentite da una categoria possono cercare le chat della categoria (a meno che la chat non sia nascosta, caso in cui solo i membri della chat possono cercarla nella directory).
    
      - In **Appartenenza** , nella sezione **Membri non consentiti** aggiungere o rimuovere utenti e altre entità Active Directory associate ai membri cui viene negato l'accesso alla chat.
    
      - In **Appartenenza** , nella sezione **Creatori** aggiungere o rimuovere utenti e altre entità Active Directory associati ai creatori della categoria. Per creatore si intende un utente con autorizzazioni per la creazione di chat room e l'assegnazione di membri e responsabili delle chat.

8.  Fare clic su **Commit** .

