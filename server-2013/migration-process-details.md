---
title: Processo di migrazione - Dettagli
TOCTitle: Processo di migrazione - Dettagli
ms:assetid: ca7e352c-9bde-47d9-8273-5cf2fdfdfe7e
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205264(v=OCS.15)
ms:contentKeyID: 49301985
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Processo di migrazione - Dettagli

 

_**Ultima modifica dell'argomento:** 2012-10-19_

Utilizzare i prerequisiti e i passaggi dettagliati descritti di seguito per eseguire la migrazione di Lync Server 2010, Group Chat o di Office Communications Server 2007 R2  Group Chat al server Chat persistente di Lync Server 2013.

## Prerequisiti per la migrazione

Verificare che vengano soddisfatti i prerequisiti seguenti prima di eseguire la migrazione di Lync Server 2010, Group Chat o di Office Communications Server 2007 R2  Group Chat al server Chat persistente di Lync Server 2013.

1.  Distribuire almeno un pool di Lync Server 2013. Se si dispone di più pool di Lync Server 2013, decidere quale pool di Lync Server 2013 definire come pool principale per il nuovo pool di server Chat persistente di Lync Server 2013.

2.  Installare il pool di server Chat persistente di Lync Server 2013. Sarà vuoto e non includerà categorie, chat room o componenti aggiuntivi. Prima di eseguire la migrazione delle categorie, delle chat room o dei componenti aggiuntivi legacy, è possibile creare chat room, categorie o componenti aggiuntivi nella distribuzione del server Chat persistente di Lync Server 2013.
    
    > [!IMPORTANT]  
    > Considerare che questi elementi appena creati possono essere in conflitto con gli elementi legacy di cui viene eseguita la migrazione. Evitare conflitti di denominazione, altrimenti verranno sovrascritti con la migrazione dei dati legacy.

## Preparazione dei dati di origine per la migrazione

Eseguire le operazioni seguenti per preparare correttamente i dati di origine per la migrazione.

1.  Eseguire il backup dei database di origine per Lync Server 2010, Group Chat o per Office Communications Server 2007 R2Group Chat. Per informazioni dettagliate sul backup di SQL Server, vedere "Panoramica del backup (SQL Server)" all'indirizzo <http://go.microsoft.com/fwlink/p/?linkid=254851>.
    
    > [!IMPORTANT]  
    > Servizi di dominio Active Directory deve rimanere lo stesso. Come condizione per la migrazione, non è possibile eseguire la migrazione a un pool in una distribuzione diversa, in particolare in una foresta di Active Directory diversa.

2.  Esaminare le chat room e la configurazione delle categorie di Lync Server 2010, Group Chat o di Office Communications Server 2007 R2  Group Chat. Qualsiasi modifica delle categorie, delle chat room o dei componenti aggiuntivi della distribuzione legacy esistente deve essere eseguita con lo strumento di amministrazione Group Chat.
    
    > [!tip]  
    > Qualsiasi modifica delle categorie, delle chat room o dei componenti aggiuntivi della distribuzione del server Chat persistente di Lync Server 2013 deve essere eseguita con il Pannello di controllo di Lync Server o i cmdlet di Windows PowerShell.    
    Eseguire le operazioni seguenti per preparare il sistema legacy per la migrazione.
    
    1.  Il server Chat persistente supporta un livello singolo di categorie e non un insieme gerarchico complesso di categorie. Dopo la migrazione, ai nomi delle sottocategorie vengono anteposti i nomi completi delle categorie padre. È possibile semplificare la struttura di categorie esistente in modo che la struttura risultante soddisfi le proprie esigenze.
    
    2.  Verificare se sono inclusi **Responsabili** nella categoria radice. Gli eventuali responsabili presenti a questo livello verranno aggiunti come **Responsabili** in tutte le chat room dopo la migrazione. Se non è un requisito dell'organizzazione, rimuovere i responsabili dalla categoria radice.
    
    3.  Verificare la lunghezza dei nomi delle chat room. A causa della semplificazione delle strutture di categorie, se dopo la migrazione sono presenti chat room in una categoria figlio, verranno anteposti i nomi completi delle categorie padre. Il limite per i nomi è di 256 caratteri, inclusi i nomi delle categorie padre. È necessario verificare la lunghezza dei nomi delle chat room e possibilmente abbreviarli qualora siano troppo lunghi.
    
    4.  Se in Lync Server 2013 gli **inviti** di una categoria sono impostati su true, è possibile scegliere true o false per gli inviti alle chat room di tale categoria. Se invece sono impostati su false, gli inviti sono disattivati per le chat room di tale categoria. Prima della migrazione, è necessario riconfigurare le impostazioni degli inviti nella versione di Lync Server  Group Chat Server legacy se si desidera che le chat room siano incluse in una categoria specifica. In caso contrario, durante la migrazione verranno visualizzati avvisi in Lync Server 2013 e per le chat room verrà impostato il valore predefinito false.
    
    5.  Se sono stati utilizzati file nelle chat room, sarà necessario eseguire manualmente XCOPY per i file nel nuovo archivio file di Chat persistente dopo la migrazione. Tale operazione infatti non verrà eseguita automaticamente dagli strumenti.
    
    6.  Se si dispone di utenti federati e di chat room con utenti federati, tenere presente che il server Chat persistente non supporta la federazione. La migrazione delle chat room con utenti federati verrà eseguita, ma gli utenti non saranno in grado di accedere al contenuto, poiché non è supportato l'accesso federato.
    
    7.  Identificare gli utenti di cui non si desidera eseguire la migrazione e contrassegnarli come disabilitati.
    
    8.  Identificare la data a partire dalla quale si desidera eseguire la migrazione del contenuto delle chat room. È ad esempio possibile scegliere di non eseguire la migrazione dei messaggi antecedenti al 1° gennaio 2010 perché potrebbero essere obsoleti o non pertinenti per la migrazione.

## Esecuzione della migrazione

Eseguire le operazioni seguenti per la migrazione di Group Chat Server legacy.

1.  Arrestare i servizi di Lync Server 2010, Group Chat, Office Communications Server 2007 R2  Group Chat o del server Chat persistente di Lync Server 2013. Poiché devono essere arrestati tutti i servizi, pianificare questa operazione per un periodo in cui è disponibile un tempo di inattività sufficiente. Come descritto in precedenza, eseguire il backup del database di Group Chat corrente.

2.  Eseguire il cmdlet **Export-CsPersistentChatData** di Windows PowerShell come membro del ruolo RBAC amministratore di Chat persistente (CsPersistentChatAdministrator). Per informazioni dettagliate sui cmdlet di importazione/esportazione, vedere [Risoluzione dei problemi di configurazione del server Chat persistente tramite i cmdlet di Windows PowerShell in Lync Server 2013](lync-server-2013-troubleshooting-persistent-chat-server-configuration-using-windows-powershell-cmdlets.md).
    
    Esaminare il contenuto esportato.

3.  Prima di procedere con l'importazione, arrestare i servizi del server Chat persistente di Lync Server 2013. Poiché devono essere arrestati tutti i servizi, pianificare questa operazione per un periodo in cui è disponibile un tempo di inattività sufficiente.

4.  Eseguire un backup del database di Chat persistente se sono state create categorie, chat room o componenti aggiuntivi nella distribuzione di Lync Server 2013 prima della migrazione. Con il processo di esportazione/importazione i dati legacy verranno uniti nella distribuzione di Lync Server 2013, ma è consigliabile eseguire il backup del database qualora il contenuto venga accidentalmente sovrascritto, ad esempio in caso di conflitti di denominazione.

5.  Eseguire il cmdlet **Import-CsPersistentChatData** (strumento di importazione) di Windows PowerShell con il comando **WhatIf** per popolare il server back-end del pool di server Chat persistente con i dati di cui è stata eseguita la migrazione. Nel processo vengono eseguite alcune conversioni per supportare il modello di amministrazione semplificata. Correggere gli eventuali errori o avvisi visualizzati.

6.  Eseguire il cmdlet **Import-CsPersistentChatData** di Windows PowerShell nel server Chat persistente come membro del ruolo RBAC amministratore di Chat persistente (CsPersistentChatAdministrator). Per informazioni dettagliate sui cmdlet di esportazione/importazione, vedere [Risoluzione dei problemi di configurazione del server Chat persistente tramite i cmdlet di Windows PowerShell in Lync Server 2013](lync-server-2013-troubleshooting-persistent-chat-server-configuration-using-windows-powershell-cmdlets.md).

7.  È necessario eseguire XCOPY per tutti i file caricati (cartella completa) nel nuovo archivio file di Chat persistente di Lync Server 2013.
    
    > [!IMPORTANT]  
    > Il client Lync 2013 non supporta il caricamento o la visualizzazione di file nelle chat room. È comunque possibile utilizzare il client legacy per inviare e visualizzare file nella chat room.

8.  Convertire l'URI del server di ricerca di Lync Server 2010, Group Chat o di Office Communications Server 2007 R2  Group Chat nell'oggetto contatto del server Chat persistente di Lync Server 2013. Le operazioni seguenti sono obbligatorie se i client Lync 2010, Group Chat oppure Office Communicator 2007 R2  Group Chat devono connettersi al client Chat persistenteLync 2013 più recente dopo la migrazione senza modifiche della configurazione sul lato client:
    
      - Eliminare l'account utente del server di ricerca ocschat@ *\<nomeDominio\>* .com utilizzato per puntare al servizio di ricerca in Lync Server 2010, Group Chat. È possibile disinstallare il pool e rimuovere le voci trusted in un secondo momento.
    
      - Creare un endpoint legacy (oggetto contatto del server Chat persistente) eseguendo il cmdlet **New-CsPersistentChatEndpoint** di Windows PowerShell con lo stesso URI SIP in modo che il client legacy funzioni correttamente quando viene riavviato il servizio.
    
    Il processo di migrazione obbligatorio è stato completato. I client Lync 2010, Group Chat oppure Office Communicator 2007 R2Group Chat possono connettersi ora al pool di server Chat persistente in modo trasparente.
    
    Eseguire queste operazioni aggiuntive di rimozione delle autorizzazioni per Lync Server 2010, Group Chat o per Office Communications Server 2007 R2Group Chat.

9.  Avviare i servizi del server Chat persistente attivando tutti i computer del nuovo pool di server Chat persistente.

10. Utilizzare il Pannello di controllo di Lync Server e i cmdlet di Windows PowerShell per verificare che la migrazione dei dati sia stata eseguita correttamente.

11. Disinstallare Lync 2010, Group Chat oppure Office Communicator 2007 R2Group Chat dai computer del pool di Group Chat Server.

12. Eliminare l'applicazione attendibile e il pool di applicazioni attendibili utilizzando i cmdlet di Windows PowerShell. In questo modo questi elementi verranno eliminati dall' archivio di gestione centrale e le voci di servizio trusted associate verranno eliminate da Active Directory. In alternativa, questa operazione può essere eseguita utilizzando Generatore di topologie (le applicazioni e i pool attendibili dispongono di un nodo dedicato anche in questa posizione).

13. È ora possibile iniziare ad abilitare la funzionalità server Chat persistente nei nuovi client. Per informazioni dettagliate sull'abilitazione del server Chat persistente, vedere [Distribuzione del server Chat persistente in Lync Server 2013](lync-server-2013-deploying-persistent-chat-server.md).
    
    > [!IMPORTANT]  
    > Lync Server 2013 supporta più pool di server Chat persistente. È supportata tuttavia la migrazione di un pool di Lync 2010, Group Chat o di Office Communications Server 2007 R2  Group Chat in un singolo pool di server Chat persistente di Lync Server 2013. È possibile aggiungere altri nuovi pool di server Chat persistente nella distribuzione per soddisfare esigenze particolari, ad esempio la conservazione dei dati in un'area geografica specifica.
