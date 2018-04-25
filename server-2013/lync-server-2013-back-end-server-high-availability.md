---
title: 'Lync Server 2013: Disponibilità elevata del server back-end'
TOCTitle: Disponibilità elevata del server back-end
ms:assetid: c559aacb-4e1d-4e78-9582-41f966ad418d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205248(v=OCS.15)
ms:contentKeyID: 49301931
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Disponibilità elevata del server back-end in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-08-12_

Per garantire la disponibilità elevata dei server back-end, è possibile usare il mirroring SQL sincrono o il clustering SQL. L'uso di una di queste soluzioni è facoltativo, ma è consigliato per garantire la continuità aziendale dell'organizzazione. Il mirroring SQL asincrono non è supportato per la disponibilità elevata dei server back-end in Lync Server 2013. Nel resto del documento qualsiasi riferimento al mirroring SQL sottintende il mirroring SQL sincrono, a meno che non venga specificato diversamente.

Il mirroring SQL può essere configurato facilmente con la Generatore di topologie. Per configurare il clustering di failover SQL è necessario usare SQL Server.

Se si usa il mirroring SQL o il clustering SQL in un pool abbinato a un altro pool Front End per il ripristino di emergenza, è necessario usare la stessa soluzione per la disponibilità elevata dei server back-end in entrambi i pool. Non è consentito abbinare un pool che usa il mirroring SQL con un pool che usa il clustering SQL.

Quando si distribuisce il mirroring SQL, viene eseguito il mirroring di tutti i database di Lync Server del pool, incluso l' archivio di gestione centrale, se presente nel pool. Viene eseguito il mirroring anche del database dell'applicazione Response Group e del database dell'applicazione Parcheggio di chiamata, se queste applicazioni sono in esecuzione nel pool.

Con il mirroring SQL, non è necessario utilizzare l'archiviazione condivisa per i server. Ogni server mantiene la propria copia dei database nello spazio di archiviazione locale.

È possibile scegliere di distribuire il mirroring SQL con o senza controllo. È consigliabile utilizzare un server di controllo poiché consente il failover automatico del server back-end. In caso contrario, un amministratore deve richiamare manualmente il failover. Se noti che anche se è distribuito un server di controllo, un amministratore può comunque richiamare manualmente il failover del server back-end, se necessario.

Se si dispone di un server di controllo, è possibile utilizzare un singolo server di controllo per più coppie di server back-end. Non esiste una corrispondenza esatta tra server di controllo e coppie di server back-end. Le distribuzioni in cui viene utilizzato un singolo server di controllo per più coppie di server back-end non sono resilienti quanto le topologie con un server di controllo separato per ogni coppia di server back-end.

Per altre informazioni sul supporto del clustering SQL, vedere [Supporto per il software di database in Lync Server 2013](lync-server-2013-database-software-support.md). Per informazioni dettagliate sulla distribuzione del clustering SQL, vedere [Configurare il clustering di SQL Server per Lync Server 2013](lync-server-2013-configure-sql-server-clustering.md).

## Tempo di ripristino per il failover automatico di server back-end con mirroring SQL

Per il failover automatico di server back-end con mirroring SQL, l'obiettivo in termini di tempo di ripristino (RTO, Recovery Time Objective) è 5 minuti. Grazie al mirroring SQL sincrono, non è prevista una perdita di dati in caso di errori di server back-end, eccetto in rari casi in cui si verifica un problema simultaneo dei server front-end e del server back-end durante il trasferimento di dati tra i server. L'obiettivo in termini di punto di ripristino (RPO, Recovery Point Objective) è 5 minuti.

## Esperienza utente durante un errore del server back-end con mirroring SQL

L'esperienza utente durante un errore dipende dalla natura dell'errore e dalla topologia.

Se si usa il mirroring SQL con un server di controllo configurato e si verifica un errore del server principale, viene automaticamente eseguito il failover del server back-end in tempi brevi. Gli utenti attivi non dovrebbero osservare un'interruzione delle sessioni in corso.

Se invece non è configurato alcun server di controllo, l'amministratore necessiterà del tempo previsto per richiamare manualmente il failover. Durante questo intervallo è possibile che gli utenti attivi subiscano alcuni disagi. Continueranno a utilizzare normalmente le sessioni per circa 30 minuti. Se nel frattempo il server primario non è stato ancora ripristinato o un amministratore non ha eseguito il failover al backup, gli utenti passeranno alla modalità resilienza e pertanto non potranno eseguire attività che richiedono una modifica persistente in Lync Server, ad esempio l'aggiunta di un contatto.

Se si verifica un errore sia del server principale che dei server back-end mirror oppure di uno di questi server e del server di controllo, il server back-end non sarà disponibile (anche se il server principale è ancora in funzione). In questo caso, gli utenti attivi passano alla modalità resilienza dopo un intervallo di tempo.

