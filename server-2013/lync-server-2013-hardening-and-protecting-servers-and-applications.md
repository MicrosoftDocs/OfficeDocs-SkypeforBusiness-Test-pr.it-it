---
title: 'Lync Server 2013: Protezione avanzata e sicurezza di server e applicazioni'
TOCTitle: Protezione avanzata e sicurezza di server e applicazioni per Lync Server 2013
ms:assetid: 9ca2b233-26f1-4d72-96e7-81a82c727806
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn518331(v=OCS.15)
ms:contentKeyID: 60490916
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Protezione avanzata e sicurezza di server e applicazioni per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-12-05_

È consigliabile configurare la sicurezza e la protezione avanzata del sistema operativo e delle applicazioni in base alle procedure consigliate per ogni specifico componente. Le informazioni in questa sezione descrivono come migliorare la protezione dei server applicazioni e usare Criteri di gruppo per implementare blocchi di sicurezza.


> [!NOTE]
> È anche possibile configurare la sicurezza e la protezione avanzata dei database usati per la distribuzione di Microsoft Lync Server 2013. Per informazioni dettagliate, vedere <A href="lync-server-2013-hardening-and-protecting-databases.md">Protezione avanzata e sicurezza dei database di Lync Server 2013</A>.



## Protezione dei server applicazioni

Nel caso dei server applicazioni è consigliabile configurare la protezione avanzata del sistema operativo e delle applicazioni. Per un computer Windows Server 2008 dedicato all'esecuzione di Microsoft Internet Security and Acceleration (ISA) Server 2006, ad esempio, è necessario impostare la protezione avanzata dalla prospettiva del sistema operativo e da quella dell'applicazione. La riduzione del numero di servizi in esecuzione e forniti dal server dovrebbe essere un obiettivo prioritario.

## Protezione dei server virtuali

Gli snapshot di server virtuali contengono copie dei dischi dei dati del server oltre a dump dei dati in memoria. Entrambi questi elementi possono contenere dati crittografici sensibili, potenzialmente esposti ad attacchi. Per i server di produzione implementati tramite virtualizzazione è consigliabile disabilitare tutti gli snapshot del server o gestirli in modo molto controllato. Per informazioni dettagliate sulla protezione dei server virtuali Hyper-V, vedere la guida alla sicurezza di Hyper-V all'indirizzo: [http://go.microsoft.com/fwlink/p/?LinkId=214176](http://go.microsoft.com/fwlink/p/?linkid=214176).

## Criteri di gruppo

In Windows Server 2008 e Windows Server 2008 R2, Criteri di gruppo consente di gestire la configurazione dei desktop in base alla directory. È possibile usare Criteri di gruppo per implementare blocchi di sicurezza definendo impostazioni del computer e dell'utente nell'ambito di un oggetto Criteri di gruppo (GPO) per quanto segue:

  - Criteri basati sul Registro di sistema

  - Sicurezza

  - Installazione di software

  - Script

  - Reindirizzamento delle cartelle

  - Servizi di installazione remota

Per offrire all'amministratore un'interfaccia utente per la configurazione di queste impostazioni, vengono forniti modelli amministrativi con i sistemi operativi, i Service Pack e alcune applicazioni, tra le quali Lync Server 2013.

Il file Communicator.adm è un modello amministrativo fornito con Lync Server 2013 e installato nella directory *%windir%*\\inf\\, che offre un'interfaccia per la configurazione delle impostazioni di Criteri di gruppo. Ogni impostazione in Communicator.adm corrisponde a un'impostazione nel Registro di sistema che influisce sul comportamento dell'applicazione.

Le impostazioni sono accessibili da GPedit.dll, disponibile dalla console Utenti e computer di Active Directory e dalla Console Gestione Criteri di gruppo.

## Impostazioni di sicurezza di Criteri di gruppo

Criteri di gruppo include impostazioni di sicurezza per un oggetto Criteri di gruppo in Configurazione computer/Impostazioni di Windows/Impostazioni sicurezza, in caso di accesso da GPedit.dll. È possibile importare modelli di sicurezza per configurare le impostazioni di sicurezza per l'oggetto Criteri di gruppo. La guida alla sicurezza di Windows Server 2008 all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=145186](http://go.microsoft.com/fwlink/p/?linkid=145186) e il toolkit per la gestione della conformità per la sicurezza di Windows Server 2008 R2 all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=211882](http://go.microsoft.com/fwlink/p/?linkid=211882) contengono numerosi modelli di esempio personalizzabili in base alle specifiche esigenze.

## Procedure consigliate

  - Configurare la protezione avanzata per tutti i sistemi operativi e tutte le applicazioni.

  - Proteggere gli snapshot dei server e ottimizzare la sicurezza di tutti i server virtuali.

  - Usare Criteri di gruppo per implementare blocchi di sicurezza.

