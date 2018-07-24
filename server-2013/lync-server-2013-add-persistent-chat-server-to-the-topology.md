---
title: 'Lync Server 2013: Aggiungere il server Chat persistente alla topologia'
TOCTitle: Aggiungere il server Chat persistente alla topologia
ms:assetid: 8389b307-8c17-4e45-b3b5-5dc9fcfc2ffb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205049(v=OCS.15)
ms:contentKeyID: 49301173
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Aggiungere il server Chat persistente alla topologia in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-06_

In Lync Server 2013, necessario incorporare il supporto per il server server Chat persistente nella topologia prima di poter configurare la distribuzione affinché supporti il server server Chat persistente. In questo argomento viene illustrato come utilizzare Generatore di topologie per aggiungere il supporto per il server server Chat persistente alla topologia esistente.

## Per aggiungere un server Chat persistente a una topologia

Per installare un server pool di server Chat persistente singolo senza configurazione di ripristino di emergenza, seguire i passaggi seguenti. Per configurare un server pool di server Chat persistente esteso con elevata disponibilità e ripristino di emergenza, vedere [Configurazione del server Chat persistente per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013](lync-server-2013-configuring-persistent-chat-server-for-high-availability-and-disaster-recovery.md) nella documentazione relativa alla distribuzione.

Per distribuire più server pool di server Chat persistente, ripetere il processo per ciascun pool.

1.  In un computer che esegue Lync Server 2013 o in cui sono installati gli strumenti di amministrazione di Lync Server eseguire l'accesso con un account membro del gruppo locale Users o un account con diritti utente equivalenti.
    

    > [!NOTE]
    > È possibile definire una topologia utilizzando un account membro del gruppo locale Users, ma per pubblicare una topologia necessaria per installare un server di Lync Server 2013, è necessario utilizzare un account membro del gruppo <STRONG>Domain Admins</STRONG> e del gruppo <STRONG>RTCUniversalServerAdmins</STRONG> e con autorizzazioni di controllo completo (ovvero, lettura, scrittura e modifica) per la condivisione file da utilizzare per l'archiviazione dell'archivio file di server Chat persistente (in modo che Generatore di topologie possa configurare i DACL richiesti) o un account con diritti utente equivalenti.



2.  Avviare Generatore di topologie.

3.  Nell'albero della console passare al nodo **Pool Chat persistente** ed espanderlo per selezionare un pool di server Chat persistente oppure fare clic con il pulsante destro del mouse sul nodo e scegliere selezionare **Nuovo pool Chat persistente**. È necessario definire il nome di dominio completo (FQDN) del pool e indicare se il pool sarà una distribuzione a server singolo o a più server.
    
    È possibile scegliere un **Pool di più computer** o un **Pool computer singolo** . Scegliere la prima opzione se si intende avere più server Chat persistenteFront End Server nel pool di server Chat persistente. Questa selezione deve essere operata subito o in seguito, poiché se si crea un pool computer singolo, non è possibile aggiungervi altri server in seguito. Se si seleziona un pool di più computer, inserire i nomi dei server Chat persistenteFront End Server individuali contenuti nel pool.
    
    > [!important]  
    > Se il ruolo del server Chat persistente viene installato su un server Lync Server 2013server Standard Edition, l'FQDN deve corrispondere all'FQDN del server server Standard Edition.

4.  Definire un **Nome visualizzato** semplice per il pool di server Chat persistente. Il nome visualizzato può essere utilizzato dai client personalizzati, in particolare quando ci sono più pool di server Chat persistente, al fine di differenziare le chat room.

5.  Definire la porta utilizzata dal server server Chat persistente per comunicare con Lync ServerFront End Server. Per impostazione predefinita, viene utilizzata la porta 5041.

6.  Se l'organizzazione richiede il supporto della conformità, selezionare la casella di controllo **Abilita conformità** . Quando questa casella è selezionata, il servizio di conformità del server server Chat persistente è installato sullo stesso computer del server Chat persistenteFront End Server. In seguito verrà richiesto di selezionare un SQL Serverserver back-end per la conformità del server Chat persistente.

7.  Assegnare la persistenza per il pool di server Chat persistente. Selezionare la casella di controllo **Usa questo pool come predefinito per il sito \<NomeSito\>** o **\_Usa questo pool come predefinito per tutti i siti** per impostare questo pool di server Chat persistente come pool predefinito per il sito corrente o tutti i siti. Quando il client di Lync 2013 viene utilizzato per la creazione e la gestione delle chat room, il pool predefinito associato al sito dell'utente è utilizzato dall'esperienza di creazione e gestione delle chat room affinché possa indirizzare le operazioni di creazione e gestione delle chat room a quel pool. Ciò si applica solo quando si hanno più pool di server Chat persistente gestiti, e si desidera utilizzare le funzioni di creazione e gestione delle chat room di server Chat persistente.
    
    > [!important]  
    > È possibile personalizzare le funzionalità di creazione e gestione delle chat room attraverso l'SDK (Software Development Kit) del server Chat persistente.<br />    Per informazioni dettagliate su come configurare i database di backup di SQL Server per il ripristino di emergenza, vedere <a href="lync-server-2013-configuring-persistent-chat-server-for-high-availability-and-disaster-recovery.md">Configurazione del server Chat persistente per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013</a> nella documentazione relativa alla distribuzione.

8.  Definire l' **archivio SQL per il server back-end della server Chat persistente (in cui è archiviato il contenuto della chat room)** eseguendo una delle seguenti operazioni:
    
      - Per utilizzare un database di SQL Server esistente, nel menu a tendina fare clic sul nome del database di SQL Server che si desidera utilizzare.
    
      - Per specificare un nuovo database di SQL Server, fare clic su **Nuovo** , quindi in **Definisci nuovo archivio SQL** eseguire le seguenti operazioni:
    
    <!-- end list -->
    
      - In **FQDN SQL Server** , specificare l'FQDN del SQL Server in cui si desidera creare il nuovo database di SQL Server.
    
      - Selezionare **Istanza predefinita** per utilizzare un'istanza predefinita oppure **Istanza denominata** per specificare un'istanza diversa, quindi specificare l'istanza che si desidera utilizzare.

9.  Se è stata abilitata la conformità, definire il database di conformità di SQL Server.
    
    > [!important]  
    > Per informazioni dettagliate su come configurare i mirror di SQL Server per l'elevata disponibilità nel database di server Chat persistente e il database di conformità di server Chat persistente, vedere <a href="lync-server-2013-configuring-persistent-chat-server-for-high-availability-and-disaster-recovery.md">Configurazione del server Chat persistente per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013</a> nella documentazione relativa alla distribuzione.

10. Definire l'archivio file. Un archivio file è una cartella in cui è archiviata una copia di qualunque file caricato nell'archivio dei file (ad esempio, gli allegati pubblicati in una chat room). Nel caso di una topologia server Chat persistente a più server, questo deve essere rappresentato da un percorso UNC (Universal Naming Convention), mentre per una topologia server Chat persistente a server singolo, può trattarsi di un percorso file locale.
    
    Per utilizzare un archivio file esistente, eseguire le operazioni seguenti:
    
      - In **FQDN file server** , specificare l'FQDN dell'archivio file in cui si desidera creare il nuovo archivio file.
    
      - In **Condivisione file** , specificare l'archivio file che si desidera utilizzare.
    
    > [!important]  
    > È possibile definire l'archivio file in Generatore di topologie prima di creare l'archivio file ma è necessario crearlo nel percorso definito prima di pubblicare la topologia.

11. Selezionare il pool del Front End Server da utilizzare come hop successivo per questo pool di server Chat persistente, ovvero il pool del Front End Server in grado di instradare le richieste del server Chat persistente a questo pool.

12. Per salvare la configurazione, fare clic su **Fine** . Il pool di server Chat persistente comparirà in Generatore di topologie insieme alle impostazioni specifiche del pool.
    
    Per pubblicare la topologia aggiornata con il server Chat persistente, vedere [Pubblicare la topologia aggiornata in Lync Server 2013](lync-server-2013-publish-the-updated-topology.md) nella documentazione relativa alla distribuzione.
    

    > [!NOTE]
    > Quando Generatore di topologie è aperto, è possibile passare alla fase 3 in <A href="lync-server-2013-publish-the-updated-topology.md">Pubblicare la topologia aggiornata in Lync Server 2013</A> per avviare la pubblicazione della topologia aggiornata.


