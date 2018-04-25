---
title: Principali funzionalità di sicurezza in Lync Server 2013
TOCTitle: Principali funzionalità di sicurezza in Lync Server 2013
ms:assetid: bf2a3b8f-73c6-47e1-8c9e-ca1dc1a502bf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn342829(v=OCS.15)
ms:contentKeyID: 56269973
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Principali funzionalità di sicurezza in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-07-18_

Lync Server 2013 include diverse funzionalità di sicurezza, tra cui l'autenticazione da server a server, il controllo degli accessi in base al ruolo e l'archiviazione centralizzata dei dati di configurazione.

Questo articolo fornisce una panoramica generale delle funzionalità di sicurezza di Lync Server 2013.

## Principali funzionalità di sicurezza in Lync Server 2013

La sicurezza è un argomento molto vasto, che riguarda tutte le funzionalità di Lync Server 2013 così come i database, i servizi e l'hardware che costituiscono un ecosistema di Lync. Questo articolo illustra in particolare alcune delle funzionalità di Lync Server 2013 progettate per la sicurezza.

## Strumenti di pianificazione e progettazione

Lync Server 2013 offre due strumenti che hanno lo scopo di facilitare la pianificazione e la progettazione e di ridurre le probabilità di configurare in modo errato i componenti di Lync Server.

  - Lo **strumento di pianificazione della topologia** automatizza buona parte del processo di progettazione della topologia. È possibile esportare i risultati dallo strumento di pianificazione a Generatore di topologie, che è lo strumento necessario per installare ogni server che esegue Lync Server 2013.

  - **Generatore di topologie** archivia tutte le informazioni di configurazione nell'archivio di gestione centrale.

Per informazioni dettagliate su questi strumenti, vedere [Pianificazione per Lync Server 2013](lync-server-2013-planning.md).

## Archivio di gestione centrale

In Lync Server 2013 i dati di configurazione relativi a server e servizi fanno parte dell'archivio di gestione centrale, un potente spazio di archiviazione schematizzato dei dati necessari per definire, configurare, gestire, amministrare, descrivere e far funzionare una distribuzione di Lync Server. L'archivio di gestione centrale esegue anche la convalida dei dati per assicurare la coerenza della configurazione. Tutte le modifiche a questi dati di configurazione avvengono nell'archivio di gestione centrale, eliminando i problemi di sincronizzazione.

Le copie di sola lettura dei dati sono replicate in tutti i server della topologia, inclusi i server perimetrali e Survivable Branch Appliance. La replica viene gestita da un servizio eseguito per impostazione predefinita nel contesto del servizio Rete, riducendo i diritti e le autorizzazioni a quelli di un semplice utente del computer.

## Autenticazione da server a server

In Lync Server 2013 è possibile configurare l'autenticazione tra server mediante il protocollo Open Authorization (OAuth). Ad esempio, è possibile configurare Lync Server 2013 per l'autenticazione con un server che esegue Exchange Server 2013. Grazie al protocollo OAuth, il server Lync e il server Exchange possono considerarsi reciprocamente attendibili, permettendo di integrare i prodotti senza problemi. Per altre informazioni, vedere [Gestione dell'autenticazione da server a server (Oauth) e applicazioni partner in Lync Server 2013](lync-server-2013-managing-server-to-server-authentication-oauth-and-partner-applications.md)

## Gestione basata su Windows PowerShell e interfaccia di gestione basata sul Web

Lync Server 2013 offre un'efficace interfaccia di gestione basata sull'interfaccia della riga di comando di Windows PowerShell che include cmdlet per la gestione della sicurezza. Le funzionalità di sicurezza di Windows PowerShell sono inoltre abilitate per impostazione predefinita, per impedire agli utenti di eseguire script alla leggera o inconsapevolmente. Questo significa che le impostazioni predefinite del software rafforzano automaticamente la sicurezza e riducono la superficie di attacco. Per informazioni dettagliate sul supporto per la gestione di Windows PowerShell in Lync Server 2013, vedere [Lync Server Management Shell](lync-server-2013-lync-server-management-shell.md).

## Controllo degli accessi in base al ruolo

La funzionalità di controllo degli accessi in base al ruolo di Microsoft Lync Server 2013 consente di delegare le attività amministrative continuando a mantenere standard di sicurezza elevati. È possibile usarla per seguire il principio dei "privilegi minimi", in base al quale agli utenti vengono concessi solo i diritti amministrativi necessari per svolgere le proprie mansioni. In Lync Server 2013 è ora possibile creare un nuovo ruolo e modificare un ruolo esistente. Per informazioni, vedere [Pianificazione del controllo di accesso basato sui ruoli in Lync Server 2013](lync-server-2013-planning-for-role-based-access-control.md).

## Network Address Translation (NAT)

Lync Server 2013 non supporta l'uso di Network Address Translation (NAT) nell'interfaccia interna del server perimetrale, ma supporta il posizionamento dell'interfaccia esterna dei servizi Access Edge, Web Conferencing Edge e A/V Edge dietro un router o un firewall che esegue NAT per le topologie di server perimetrale consolidato sia singolo che con scalabilità implementata. Più server perimetrali dietro un servizio di bilanciamento del carico hardware non possono usare NAT. Se più server perimetrali usano NAT nelle rispettive interfacce esterne, è necessario il bilanciamento del carico DNS (Domain Name System). A sua volta, il bilanciamento del carico DNS consente di ridurre il numero di indirizzi IP pubblici per server perimetrale in un pool di server perimetrali. Per informazioni, vedere [Pianificazione dell'accesso degli utenti esterni in Lync Server 2013](lync-server-2013-planning-for-external-user-access.md).


> [!NOTE]
> Se si attua una federazione con un'azienda in cui è distribuito Microsoft Office Communications Server 2007 e occorre usare le funzionalità audio/video tra la propria azienda e l'azienda federata, i requisiti per le porte saranno gli stessi della versione precedente dei server perimetrali distribuiti. Ad esempio, gli intervalli di porte necessari per le versioni precedenti devono essere aperti per entrambe le aziende finché il partner federato non aggiorna i propri server perimetrali a Lync Server 2013. A quel punto i requisiti per le porte potranno essere rivisti e ridotti in base alla nuova configurazione.



## Certificati più semplici per i server perimetrali

La Distribuzione guidata consente di inserire automaticamente i nomi del soggetto e i nomi alternativi del soggetto, riducendo le probabilità di includere voci non necessarie e potenzialmente non sicure.

## Trustworthy Computing Security Development Lifecycle (SDL)

Lync Server 2013 è progettato e sviluppato in conformità con Microsoft Trustworthy Computing Security Development Lifecycle (SDL), di cui è disponibile una descrizione all'indirizzo <http://go.microsoft.com/fwlink/?linkid=68761>.

  - **Attendibile da progettazione**   La prima fase del processo di creazione di un sistema per le comunicazioni unificate più sicuro è consistita nella progettazione di modelli di rischio e nel testing di ogni funzionalità in fase di progettazione. Microsoft esegue inoltre il testing oltre i limiti del funzionamento progettato allo scopo di individuare le vulnerabilità di protezione risultanti da un comportamento imprevisto del prodotto. Nelle procedure e nel processo di codifica sono stati incorporati diversi miglioramenti a livello di sicurezza. Gli strumenti di compilazione rilevano i sovraccarichi del buffer e altri potenziali rischi per la sicurezza prima che il codice venga compilato nel prodotto finale. Naturalmente, una progettazione che tenga conto di tutti i rischi per la sicurezza sconosciuti è impensabile. Nessun sistema è in grado di garantire una completa sicurezza. Tuttavia, poiché il prodotto è stato sviluppato in base ai principi della progettazione sicura fin dall'inizio, Lync Server 2013 incorpora tecnologie di sicurezza standard come componente fondamentale della sua architettura.

  - **Attendibile per impostazione predefinita**   Per impostazione predefinita, le comunicazioni di rete in Lync Server 2013 sono crittografate. Poiché tutti i server usano certificati e l'autenticazione Kerberos, TLS, Secure Real-Time Transport Protocol (SRTP) e altre tecniche di crittografia standard, tra cui la crittografia AES (Advanced Encryption Standard) a 128 bit, praticamente tutti i dati di Lync Server sono protetti in rete. Inoltre, grazie al controllo degli accessi in base al ruolo è possibile distribuire server che eseguono Lync Server 2013 in modo che ogni ruolo del server esegua solo i servizi appropriati, con autorizzazioni limitate a quei servizi.

  - **Attendibile in fase di distribuzione**   Tutta la documentazione di Lync Server 2013 contiene procedure consigliate e suggerimenti che aiutano a determinare e configurare i livelli di sicurezza ottimali per la propria distribuzione e a valutare i rischi per la sicurezza impliciti nell'attivazione di opzioni non predefinite.

