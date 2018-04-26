---
title: Configurazione del supporto per le riunioni di grandi dimensioni
TOCTitle: Configurazione del supporto per le riunioni di grandi dimensioni
ms:assetid: 8e22d34b-b395-408d-9d48-8f2a3abe9513
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205074(v=OCS.15)
ms:contentKeyID: 49301284
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione del supporto per le riunioni di grandi dimensioni

 

_**Ultima modifica dell'argomento:** 2014-05-12_

Il supporto di un gran numero di riunioni fino a 1000 utenti richiede la creazione di una topologia appropriata, il rispetto di prerequisiti hardware e software e la configurazione idonea dell'ambiente.

## Requisiti della topologia

Una singola riunione di grandi dimensioni richiede almeno un Front End Server e un server back-end. Tuttavia, per offrire disponibilità elevata, è consigliabile un pool di due Front End Server con server back-end con mirroring.

L'account dell'utente che ospita le riunioni di grandi dimensioni deve trovarsi in questo pool. Non è tuttavia consigliabile ospitare altri account utente in questo pool. Utilizzarlo invece solo per le riunioni di grandi dimensioni. È preferibile creare un account utente speciale in questo pool da utilizzare solo per ospitare riunioni di grandi dimensioni. Poiché l'impostazione delle riunioni di grandi dimensioni è ottimizzata per le prestazioni, l'utilizzo come utente normale potrebbe causare problemi quali l'impossibilità di promuovere una sessione P2P a riunione quando è coinvolto un endpoint PSTN.

La gestione di un pool con due server front-end richiede alcune considerazioni speciali. Per ulteriori informazioni, vedere [Topologie e componenti per Front End Server, messaggistica istantanea e presenza in Lync Server 2013](lync-server-2013-topologies-and-components-for-front-end-servers-instant-messaging-and-presence.md).

Inoltre, se si desidera offrire backup e failover a fini di ripristino di emergenza per il pool usato per le riunioni di grandi dimensioni, è possibile abbinarlo a un pool dedicato con configurazione analoga in un altro data center. Per informazioni dettagliate, vedere [Pianificazione per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013](lync-server-2013-planning-for-high-availability-and-disaster-recovery.md).

![Configurazione di pool per riunioni di grandi dimensioni](images/JJ205074.ee00e1c0-c3b2-464d-aa89-a1e877cd034d(OCS.15).jpg "Configurazione di pool per riunioni di grandi dimensioni")

Note aggiuntive sulla topologia:

  - È necessaria una condivisione di file per archiviare i contenuti delle riunioni e se il server di archiviazione è distribuito e abilitato, per i file di archiviazione. La condivisione di file può essere dedicata al pool oppure corrispondere a quella usata da un altro pool nello stesso sito di distribuzione. Per informazioni dettagliate sulla configurazione della condivisione di file, vedere [Configurare l'archiviazione dei file per Lync Server 2013](lync-server-2013-configure-dfs-file-storage.md).

  - È necessario un Server Office Web Apps per abilitare la funzionalità relativa alle presentazioni di PowerPoint nelle riunioni di grandi dimensioni. Il Server Office Web Apps può essere dedicato al pool per le riunioni di grandi dimensioni oppure essere lo stesso Server Office Web Apps usato da altri pool del sito in cui è distribuito il pool dedicato.

  - Il bilanciamento del carico del Front End Server richiede bilanciamento del carico hardware per il traffico HTTP (ad esempio il download di contenuti della riunione). Per il traffico SIP è consigliato il bilanciamento del carico DNS. Per informazioni dettagliate, vedere [Requisiti per il bilanciamento del carico per Lync Server 2013](lync-server-2013-load-balancing-requirements.md).

  - Se si vuole usare il Monitoring Server per il pool dedicato alle riunioni di grandi dimensioni, è consigliabile l'uso del Monitoring Server e del relativo database condivisi tra tutti i pool Front End Server nella distribuzione di Lync Server.

## Requisiti hardware e software

I requisiti hardware per i server in un pool dedicato alle riunioni di grandi dimensioni sono gli stessi come per gli altri server Lync Server 2013. Per dettagli sui requisiti hardware, vedere "[Piattaforme hardware server per Lync Server 2013](lync-server-2013-server-hardware-platforms.md).

I server in un pool dedicato per riunioni di grandi dimensioni devono soddisfare tutti i requisiti software di Lync Server 2013. Per informazioni dettagliate sui requisiti software, vedere la documentazione seguente:

  - [Supporto del sistema operativo per server e strumenti in Lync Server 2013](lync-server-2013-server-and-tools-operating-system-support.md)

  - [Supporto per il software di database in Lync Server 2013](lync-server-2013-database-software-support.md)

  - [Requisiti software aggiuntivi per Lync Server 2013](lync-server-2013-additional-software-requirements.md)

Inoltre, sia a Lync Server 2013 che a tutti i client Lync Server 2013 devono essere stati applicati gli aggiornamenti più recenti.

## Requisiti di configurazione

È consigliabile creare un nuovo criteri di conferenza specifico per le riunioni di grandi dimensioni e quindi assegnare il criterio di conferenza agli utenti ospitati in un pool dedicato a riunioni di grandi dimensioni. Configurare il criterio per conferenze con le impostazioni seguenti:

  - Impostare l'opzione **MaxMeetingSize** su **1000**. Il valore predefinito è **250**.

  - Impostare l'opzione **AllowLargeMeetings** su **True**.

  - Impostare l'opzione **EnableAppDesktopSharing** su **None**.

  - Impostare l'opzione **AllowUserToScheduleMeetingsWithAppSharing** su **False**.

  - Impostare l'opzione **AllowSharedNotes** su **False**.

  - Impostare l'opzione **AllowAnnotations** su **False**.

  - Impostare l'opzione **DisablePowerPointAnnotations** su **True**.

  - Impostare l'opzione **AllowMultiview** su **False**.

  - Impostare l'opzione **EnableMultiviewJoin** su **False**.


> [!NOTE]
> Il supporto per riunioni di grandi dimensioni nell'ordine di 1000 utenti in Lync Server 2013 richiede che l'impostazione <STRONG>AllowLargeMeetings</STRONG> nei criteri di conferenza per l'utilità di pianificazione delle riunioni sia impostata su true. In questo modo, l'esperienza di Lync risulterà ottimizzata per riunioni particolarmente vaste. In particolare, in una grande riunione, Lync non visualizza l'elenco iniziale o aggiornato completo dei partecipanti alla riunione, il che costituisce un collo di bottiglia delle prestazioni per i client e Lync Server 2013. Al contrario, Lync mostrerà solo informazioni sull'utente e l'elenco di relatori della riunione. Lync mostrerà comunque correttamente il numero totale di partecipanti disponibili nelle riunioni di grandi dimensioni.



Ad eccezione dell'impostazione **Dimensione massima riunione**, tutti gli altri criteri di conferenza specificati qui sono necessari per disabilitare le funzionalità di conferenza non necessarie in riunioni di grandi dimensioni.

È inoltre necessario configurare il pool dedicato alle riunioni di grandi dimensioni in modo che ogni utente di Lync Server 2013 ospitato nel pool e responsabile della gestione della pianificazione della riunione disponga delle autorizzazioni appropriate. A tale scopo, procedere come segue:

  - Impostare l'opzione **Designa come relatore** a **Nessuno**. In genere, uno o pochi altri utenti tra tutti i partecipanti a una riunione di grandi dimensioni sono relatori, pertanto i partecipanti non devono essere automaticamente ammessi a riunioni di grandi dimensioni come relatori. I relatori dovrebbero invece essere designati in modo esplicito al momento di pianificare la riunione oppure durante la riunione stessa.

  - Accertarsi che la casella di controllo **Tipo di conferenza assegnato per impostazione predefinita** non sia selezionata. Questa impostazione controlla se componente aggiuntivo per riunioni online per Lync 2013 deve pianificare sempre le conferenze usando la conferenza assegnata dell'organizzatore, il che significa che le riunioni pianificate non hanno lo stesso URL di accesso e le stesse informazioni sull'audio. In scenari di collaborazione di piccoli gruppi, l'assegnazione di un tipo di conferenza funziona bene perché ognuno dispone di una conferenza individuale assegnata e l'URL di accesso e le informazioni audio consentono di agevolare un più rapido accesso alla riunione. Tuttavia, in scenari con riunioni di grandi dimensioni, il personale di queste ultime pianifica le riunioni più grandi con un singolo set di credenziali utente, e quindi offre URL di accesso e informazioni sull'audio al richiedente il meeting. In questo caso, l'uso di un URL diverso per accedere a ogni riunione funziona bene.

  - Accettarsi che la casella di controllo **Consenti utenti anonimi per impostazione predefinita** non è selezionata a meno che non sia necessario. Questa impostazione influisce sul tipo di accesso alla riunione personalizzato pianificato da componente aggiuntivo per riunioni online per Lync 2013 quando non si usa una conferenza assegnata. L'opzione appropriata per questa impostazione dipende dalle esigenze dell'organizzazione. Se la maggior parte delle riunioni di grandi dimensioni nell'organizzazione è interna, non selezionare questa opzione. Se per la maggior parte delle riunioni di grandi dimensioni è prevista la partecipazione di utenti esterni, selezionare questa opzione.

