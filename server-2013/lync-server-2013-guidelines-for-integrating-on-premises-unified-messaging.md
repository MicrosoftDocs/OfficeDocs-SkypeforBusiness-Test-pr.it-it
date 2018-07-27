---
title: "Lync Server 2013: Linee guida per l'integrazione della messaggistica unificata locale"
TOCTitle: Linee guida per l'integrazione della messaggistica unificata locale con Lync Server
ms:assetid: 829ac017-6907-40f9-be22-787a28eae0ac
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398656(v=OCS.15)
ms:contentKeyID: 49301164
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Linee guida per l'integrazione della messaggistica unificata locale con Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-25_

Di seguito sono elencate le linee guida e le procedure consigliate da prendere in considerazione quando si distribuisce VoIP aziendale:

> [!IMPORTANT]  
> Messaggistica unificata di Exchange supporta IPv6 solo se si utilizza anche UCMA 4.

  - Distribuire un Lync Server 2013 Standard Edition o un pool Front End. Per informazioni dettagliate sull'installazione, vedere [Distribuzione di Lync Server 2013](lync-server-2013-deploying-lync-server.md) nella documentazione relativa alla distribuzione.

  - Collaborare con gli amministratori di Exchange per verificare le attività che verranno eseguite da ognuno al fine di assicurare un'integrazione agevole e corretta.

  - Distribuire i ruoli del server di Cassetta postale di Exchange in ogni foresta di Messaggistica unificata di Exchange in cui si desidera abilitare gli utenti per Messaggistica unificata di Exchange. Per informazioni sull'installazione dei ruoli dei server di Exchange, vedere la documentazione di Microsoft Exchange Server 2013.
    
    > [!IMPORTANT]  
    > Quando la Messaggistica unificata di Exchange è installata, è configurata per l'utilizzo di un certificato autofirmato.<br />    Il certificato autofirmato, tuttavia, non consente una relazione di trust tra Lync Server 2013 e la Messaggistica unificata di Exchange e per questo motivo è necessario richiedere un certificato distinto a un'Autorità di certificazione considerata attendibile da entrambi i server.

  - Se Lync Server 2013 e la Messaggistica unificata di Exchange sono installati in foreste diverse, configurare ogni foresta di Exchange in modo da considerare attendibile la foresta di Lync Server 2013 e configurare la foresta di Lync Server 2013 in modo da considerare attendibile ogni foresta di Exchange. Impostare inoltre le impostazioni di Messaggistica unificata di Exchange sugli oggetti utente nella foresta di Lync Server 2013, in genere utilizzando uno script o uno strumento tra foreste, ad esempio Identity Lifecycle Manager (ILM).

  - Se necessario, installare Exchange Management Console per gestire i server di messaggistica unificata.

  - Ottenere numeri di telefono validi per Outlook Voice Access e l'operatore automatico.

  - Se si utilizza una versione di Messaggistica unificata di Exchange precedente a Microsoft Exchange Server 2010 Service Pack 1 (SP1), coordinare i nomi per i dial plan URI SIP di Messaggistica unificata di Exchange e i dial plan VoIP aziendale.

## Distribuzione di server di messaggistica unificata di Exchange ridondanti

> [!IMPORTANT]  
> È consigliabile distribuire almeno due server su cui è eseguita la messaggistica unificata di Exchange per ogni dial plan URI SIP di Messaggistica unificata di Exchange configurato per l'organizzazione. Oltre a garantire maggiori funzionalità, la distribuzione di server ridondanti garantisce una disponibilità elevata. In caso di errore di un server, è possibile configurare Lync Server 2013 per il failover a un altro server.

Le configurazioni di esempio seguenti garantiscono resilienza della messaggistica unificata di Exchange.

**Esempio 1: resilienza della messaggistica unificata di Exchange**

![Esempio 1 di messaggistica unificata di Exchange](images/Gg398656.3644b847-0847-4550-a989-e3fc51de5c4b(OCS.15).jpg "Esempio 1 di messaggistica unificata di Exchange")

Nell'esempio 1 i server di messaggistica unificata di Exchange 1 e 2 sono abilitati nel data center di Tukwila e i server di messaggistica unificata di Exchange 3 e 4 sono abilitati nel data center di Dublino. In caso di interruzione della messaggistica unificata di Exchange a Tukwila, i record A DNS per i server 1 e 2 devono essere configurati per puntare, rispettivamente, ai server 3 e 4. In caso di interruzione della messaggistica unificata a Dublino, i record A DNS per i server 3 e 4 devono essere configurati per puntare, rispettivamente, ai server 1 e 2.


> [!NOTE]
> Per l'esempio 1, è anche necessario assegnare uno dei certificati seguenti in ogni server di messaggistica unificata di Exchange: 
> <UL>
> 
> 
> 
> <li>
> <P>Utilizzare un certificato con un carattere jolly nel nome alternativo del soggetto.</P>
> 
> 
> 
> <li>
> <P>Inserire il nome di dominio completo (FQDN) di ciascuno dei quattro server di messaggistica unificata di Exchange nella rete SAN.</P></LI></UL>



**Esempio 2: resilienza della messaggistica unificata di Exchange**

![Esempio 2 di messaggistica unificata di Exchange](images/Gg398656.15754273-306e-448d-b258-84bc2936a2e8(OCS.15).jpg "Esempio 2 di messaggistica unificata di Exchange")

Nell'esempio 2, in condizioni operative standard, i server di messaggistica unificata di Exchange 1 e 2 sono abilitati nel data center di Tukwila e i server di messaggistica unificata di Exchange 3 e 4 sono abilitati nel data center di Dublino. Tutti e quattro i server sono inclusi nel dial plan URI SIP degli utenti Tukwila, tuttavia, i server 3 e 4 sono disabilitati. In caso di interruzione della messaggistica unificata di Exchange a Tukwila, ad esempio, i server 1 e 2 di messaggistica unificata di Exchange devono essere disabilitati e i server 3 e 4 di messaggistica unificata di Exchange devono essere abilitati in modo che il traffico di messaggistica unificata di Exchange di Tukwila venga instradato ai server di Dublino.

Per informazioni dettagliate su come abilitare o disabilitare la messaggistica unificata in Exchange 2013, vedere "Integrare la messaggistica unificata di Exchange 2013 con Lync Server" all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=265372](http://go.microsoft.com/fwlink/p/?linkid=265372).

Per informazioni dettagliate su come abilitare o disabilitare la messaggistica unificata in Microsoft Exchange Server 2010, vedere

  - "Abilitazione della messaggistica unificata in Exchange 2010" all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=204418](http://go.microsoft.com/fwlink/p/?linkid=204418).

  - "Disabilitazione della messaggistica unificata in Exchange 2010" all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=204416](http://go.microsoft.com/fwlink/p/?linkid=204416).

## Vedere anche

#### Concetti

[Processo di distribuzione per l'integrazione della messaggistica unificata locale con Lync Server 2013](lync-server-2013-deployment-process-for-integrating-on-premises-unified-messaging.md)

