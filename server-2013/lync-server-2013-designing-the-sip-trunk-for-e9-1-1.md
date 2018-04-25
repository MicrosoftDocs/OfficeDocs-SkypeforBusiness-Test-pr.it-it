---
title: 'Lync Server 2013: Progettazione del trunk SIP per i servizi di emergenza'
TOCTitle: Progettazione del trunk SIP per i servizi di emergenza
ms:assetid: 4f93b974-b460-45c7-a4a8-6f38e34840f5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398323(v=OCS.15)
ms:contentKeyID: 49300506
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Progettazione del trunk SIP per i servizi di emergenza in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-03_

Lync Server usa trunk SIP per connettere una chiamata di emergenza al provider del servizio E9-1-1. È possibile configurare trunk SIP per il servizio di emergenza per E9-1-1 in un solo sito centrale, in più siti centrali oppure presso ogni sito di succursale. Se il collegamento WAN tra il sito del chiamante e il sito che ospita il trunk SIP del servizio di emergenza non è disponibile, tuttavia, una chiamata effettuata da un utente del sito disconnesso richiederà nei criteri vocali dell'utente uno speciale record di utilizzo telefonico che instradi la chiamata al centro di inoltro delle chiamate di emergenza (ECRC, Emergency Call Relay Center) attraverso il gateway PSTN (Public Switched Telephone Network) locale. Lo stesso vale se sono applicati limiti per le chiamate simultanee del servizio Controllo di ammissione di chiamata.


> [!NOTE]
> Esistono due modi per implementare un trunk SIP in un ambiente Lync Server: 
> <UL>
> <LI>
> <P>Utilizzare Mediation Server multihomed che comunichino con il provider di trunk SIP mediante le interfacce instradate pubblicamente rivolte verso l'esterno.</P>
> <LI>
> <P>Utilizzare un Session Border Controller (SBC) locale per fornire un punto di demarcazione sicuro tra i Mediation Server e i servizi del provider di trunk SIP.</P></LI></UL>Se si sceglie quest'ultimo metodo, accertarsi che la marca e il modello del controller SBC prescelto siano certificati e supportino la trasmissione di dati sulla posizione PIDF-LO (Presence Information Data Format Location Object) all'interno delle richieste SIP INVITE. In caso negativo, le chiamate raggiungeranno il provider di servizi di emergenza prive delle informazioni relative alla posizione. Per informazioni dettagliate sugli SBC certificati, vedere "Infrastruttura qualificata per Microsoft Lync" all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=248425">http://go.microsoft.com/fwlink/p/?LinkId=248425</A>.<BR>I provider del servizio E9-1-1 offrono l'accesso a una coppia di SBC per garantire ridondanza. È necessario prendere varie decisioni in merito alla topologia del Mediation Server e alla configurazione del routing delle chiamate. Sarà necessario stabilire se considerare entrambi i controller SBC come peer e usare l'instradamento round robin delle chiamate tra questi oppure se designare un controller SBC come primario e l'altro come secondario.



Per informazioni dettagliate sulla distribuzione di un trunk SIP in Lync Server, vedere [Come implementare il trunking SIP in Lync Server 2013](lync-server-2013-how-do-i-implement-sip-trunking.md). Per facilitare la distribuzione dei trunk SIP per i servizi E9-1-1, è consigliabile rispondere prima di tutto alle domande seguenti.

  - **Il trunk SIP deve essere distribuito su una connessione con linea dedicata o una connessione Internet condivisa?**  
    È importante che la connessione sia sempre disponibile per le chiamate di emergenza. Una linea dedicata offre una connessione che non viene compromessa da altro traffico in rete e offre la possibilità di implementare QoS (Quality of Service). Ricordarsi che se la connessione ai provider di servizi di emergenza viene effettuata tramite la rete Internet pubblica ed è necessario garantire la riservatezza delle chiamate di emergenza, è necessario implementare la crittografia IPSec.

<!-- end list -->

  - **La distribuzione dei servizi E9-1-1 è progettata per situazioni di emergenza?**  
    Trattandosi di una soluzione per le emergenze, la resilienza è importante. Distribuire i Mediation Server primario e secondario e i trunk SIP in posizioni protette. È consigliabile distribuire il Mediation Server primario più vicino agli utenti che supporta e instradare le chiamate di failover sul Mediation Server secondario, collocato in una posizione geografica diversa.

<!-- end list -->

  - **È necessario distribuire un trunk SIP separato per ogni succursale?**  
    Lync Server offre varie strategie per gestire la resilienza dei servizi vocali nelle succursali, tra le quali la disponibilità di reti dati resilienti, la distribuzione di un trunk SIP in ogni succursale o il push delle chiamate fuori dal gateway locale in caso di interruzioni. Per informazioni dettagliate, vedere [Trunking SIP dei siti di succursale in Lync Server 2013](lync-server-2013-branch-site-sip-trunking.md).

<!-- end list -->

  - **È abilitato il controllo di ammissione di chiamata?**  
    Lync Server gestisce le chiamate di emergenza nello stesso modo delle chiamate ordinarie. Per questo motivo, la gestione della larghezza di banda o del servizio Controllo di ammissione di chiamata può avere effetti negativi sulla configurazione del servizio E9-1-1. Se è abilitato il servizio Controllo di ammissione di chiamata e viene superato il limite configurato su un collegamento usato per il routing delle chiamate di emergenza, le chiamate di emergenza vengono bloccate o instradate su un gateway PSTN locale. Come indicato in precedenza in questo argomento, per queste chiamate non saranno disponibili dati sulla posizione e sarà necessario instradarle manualmente verso il centro ECRC.

