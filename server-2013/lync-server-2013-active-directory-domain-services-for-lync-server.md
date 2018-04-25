---
title: Servizi di dominio Active Directory per Lync Server 2013
TOCTitle: Servizi di dominio Active Directory per Lync Server 2013
ms:assetid: 5483afd5-d8af-4825-ae95-a82dbe941dbf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn481129(v=OCS.15)
ms:contentKeyID: 59679239
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Servizi di dominio Active Directory per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Servizi di dominio Active Directory viene utilizzato come servizio directory per le reti Windows Server 2003, Windows Server 2008, Windows Server 2012 e Windows Server 2012 R2. Servizi di dominio Active Directory costituisce inoltre la base su cui viene creata l'infrastruttura di sicurezza di Microsoft Lync Server 2013. In questa sezione viene descritto in che modo Lync Server 2013 utilizza Servizi di dominio Active Directory per creare un ambiente affidabile per la messaggistica istantanea, le conferenze Web e le sessioni vocali e multimediali. Per informazioni dettagliate sulle estensioni di Lync Server per Servizi di dominio Active Directory e sulla preparazione dell'ambiente per Servizi di dominio Active Directory, vedere [Preparazione di Servizi di dominio Active Directory per Lync Server 2013](lync-server-2013-preparing-active-directory-domain-services.md) nella documentazione relativa alla distribuzione. Per informazioni dettagliate sul ruolo di Servizi di dominio Active Directory nelle reti Windows Server, vedere la documentazione per la versione del sistema operativo in uso.

Lync Server 2013 utilizza Servizi di dominio Active Directory per archiviare:

  - Impostazioni globali necessarie per tutti i server che eseguono Lync Server 2013 in una foresta.

  - Informazioni sui servizi che identificano i ruoli di tutti i server che eseguono Lync Server 2013 in una foresta.

  - Alcune impostazioni utente.

## Infrastruttura di Active Directory

I requisiti di infrastruttura per Active Directory includono:

  - Requisiti del sistema operativo per i controller di dominio

  - Requisiti del livello di funzionalità del dominio e della foresta

  - Requisiti di dominio del catalogo globale

Per informazioni dettagliate, vedere [Requisiti dell'infrastruttura di Active Directory per Lync Server 2013](lync-server-2013-active-directory-infrastructure-requirements.md) nella documentazione relativa alla distribuzione.

## Preparazione di Servizi di dominio Active Directory


> [!NOTE]
> È consigliabile distribuire le impostazioni globali nel contenitore di configurazione invece che nel contenitore di sistema. Questa operazione non aumenta il livello di sicurezza, ma può determinare dei miglioramenti in termini di scalabilità per alcune topologie di Servizi di dominio Active Directory. Se si sta eseguendo la migrazione da Microsoft Office Communications Server 2007 utilizzando il contenitore di sistema, ma in seguito si intende utilizzare il contenitore di configurazione, è NECESSARIO spostare le impostazioni nel contenitore di sistema PRIMA di eseguire qualsiasi preparazione per l'aggiornamento. Per eseguire la migrazione delle impostazioni dal contenitore di sistema al contenitore di configurazione, vedere Strumento di migrazione delle impostazioni globali di Office Communications Server 2007 all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=145236">http://go.microsoft.com/fwlink/p/?LinkId=145236</A>.



Durante la distribuzione di Lync Server 2013, è innanzitutto necessario preparare Servizi di dominio Active Directory. La preparazione di Servizi di dominio Active Directory per Lync Server 2013 prevede i seguenti tre passaggi:

  - **Preparare lo schema**. Questa attività estende lo schema in Servizi di dominio Active Directory per includere le classi e gli attributi specifici di Lync Server 2013. Per informazioni dettagliate sulla preparazione dello schema, vedere [Esecuzione della preparazione dello schema in Lync Server 2013](lync-server-2013-running-schema-preparation.md) nella documentazione relativa alla distribuzione. Per ulteriori informazioni, vedere [Migrazione da Office Communications Server 2007 R2 a Lync Server 2013](migration-from-office-communications-server-2007-r2-to-lync-server-2013.md).

  - **Preparare la foresta**. Questa attività consente di creare oggetti e impostazioni globali nel dominio radice della foresta, nonché il servizio universale e i gruppi amministrativi che gestiscono l'accesso a tali oggetti e impostazioni. Per informazioni dettagliate sulla preparazione della foresta, vedere [Esecuzione della preparazione della foresta per Lync Server 2013](lync-server-2013-running-forest-preparation.md) nella documentazione relativa alla distribuzione.

  - **Preparare il dominio**. Questa attività consente di aggiungere le voci di controllo di accesso necessarie ai gruppi universali che concedono autorizzazioni per ospitare e gestire gli utenti nell'ambito del dominio. È necessario completare l'attività in tutti i domini in cui si desidera distribuire i server che eseguono Lync Server 2013 e nei domini in cui risiedono gli utenti di Lync Server. Per informazioni dettagliate sulla preparazione del dominio, vedere [Esecuzione della preparazione del dominio per Lync Server 2013](lync-server-2013-running-domain-preparation.md) nella documentazione relativa alla distribuzione.

Per visualizzare una panoramica dell'intero processo di preparazione di Active Directory e dei diritti e delle autorizzazioni richiesti per eseguire ogni passaggio, vedere [Requisiti dell'infrastruttura di Active Directory per Lync Server 2013](lync-server-2013-active-directory-infrastructure-requirements.md) nella documentazione relativa alla distribuzione.

## Gruppi universali

Durante la preparazione della foresta, Lync Server 2013 crea vari gruppi universali all'interno di Servizi di dominio Active Directory che dispongono dell'autorizzazione per l'accesso e la gestione dei servizi e delle impostazioni globali. Tali gruppi universali includono:

  - **Gruppi amministrativi**. Questi gruppi definiscono i principali ruoli di amministratore per una rete Lync Server. Durante la preparazione della foresta, tali gruppi di amministratori vengono aggiunti ai gruppi di infrastruttura di Lync Server.

  - **Gruppi di servizio**. Questi gruppi sono account di servizio necessari per accedere ai diversi servizi forniti da Lync Server.

  - **Gruppi di infrastruttura**. Questi gruppi forniscono le autorizzazioni per accedere ad aree specifiche dell'infrastruttura di Lync Server. Operano come componenti dei gruppi amministrativi ed è consigliabile non modificarli né aggiungervi utenti direttamente. Durante la preparazione della foresta, specifici gruppi amministrativi e di servizio vengono aggiunti ai gruppi di infrastruttura appropriati.

Per informazioni dettagliate sugli specifici gruppi universali creati durante la preparazione di Active Directory per Lync Server, nonché sui gruppi amministrativi e di servizio aggiunti ai gruppi di infrastruttura, vedere [Modifiche apportate durante la preparazione della foresta in Lync Server 2013](lync-server-2013-changes-made-by-forest-preparation.md) nella documentazione relativa alla distribuzione.


> [!NOTE]
> Lync Server 2013 supporta i gruppi universali in Windows Server 2012 per i server che eseguono Lync Server 2013, nonché nei sistemi operativi Windows Server 2003 per i controller di dominio. Ai membri dei gruppi universali, che possono includere altri gruppi e account di qualsiasi dominio della foresta o dell'albero del dominio, è possibile assegnare autorizzazioni in qualsiasi dominio della foresta o dell'albero del dominio. Il supporto dei gruppi universali, insieme alla delega dell'amministratore, semplifica la gestione di una distribuzione di Lync Server. Non è ad esempio necessario aggiungere un dominio a un altro per consentire a un amministratore di gestirli entrambi.



## Controllo degli accessi in base al ruolo

Oltre alla creazione di gruppi amministrativi e di servizio universali e all'aggiunta di gruppi amministrativi e di servizio ai gruppi universali appropriati, la preparazione della foresta permette anche la creazione di gruppi di controllo degli accessi in base al ruolo (RBAC). Per informazioni dettagliate sugli specifici gruppi RBAC creati durante la preparazione della foresta, vedere [Modifiche apportate durante la preparazione della foresta in Lync Server 2013](lync-server-2013-changes-made-by-forest-preparation.md) nella documentazione relativa alla distribuzione. Per ulteriori informazioni sui gruppi RBAC, vedere [Controllo degli accessi in base al ruolo (RBAC) per Lync Server 2013](lync-server-2013-role-based-access-control-rbac.md).

## Ereditarietà e voci di controllo di accesso (ACE)

Con la preparazione della foresta vengono create ACE pubbliche e private e ACE aggiuntive per i gruppi universali creati. Le voci di controllo di accesso private vengono create nel contenitore di impostazioni globali utilizzato da Lync Server. Questo contenitore viene utilizzato solo da Lync Server ed è posizionato nel contenitore di configurazione o nel contenitore di sistema del dominio radice, a seconda del percorso di archiviazione delle impostazioni globali.

La preparazione del dominio comporta l'aggiunta delle voci di controllo di accesso necessarie ai gruppi universali che concedono autorizzazioni per ospitare e gestire gli utenti nell'ambito del dominio. Con la preparazione del dominio vengono create voci di controllo di accesso nella radice del dominio e tre contenitori predefiniti per utenti, computer e controller di dominio.

Per informazioni dettagliate sulle voci di controllo di accesso pubbliche create e aggiunte durante la preparazione della foresta e del dominio, vedere [Modifiche apportate durante la preparazione della foresta in Lync Server 2013](lync-server-2013-changes-made-by-forest-preparation.md) e [Modifiche apportate durante la preparazione del dominio in Lync Server 2013](lync-server-2013-changes-made-by-domain-preparation.md) nella documentazione relativa alla distribuzione.

Le organizzazioni spesso bloccano Servizi di dominio Active Directory (AD DS) per ridurre i rischi per la sicurezza. Tuttavia, un ambiente di Active Directory bloccato può limitare le autorizzazioni necessarie per Lync Server 2013. Ciò può includere la rimozione delle voci di controllo di accesso dai contenitori e dalle unità organizzative e la disattivazione dell'ereditarietà delle autorizzazioni negli oggetti User, Contact, InetOrgPerson o Computer. In un ambiente di Active Directory bloccato, è necessario impostare manualmente le autorizzazioni nei contenitori e nelle unità organizzative che le richiedono. Per informazioni dettagliate, vedere [Preparazione di un ambiente Servizi di dominio Active Directory bloccato in Lync Server 2013](lync-server-2013-preparing-a-locked-down-active-directory-domain-services.md) nelle documentazione relativa alla distribuzione.

## Informazioni sul server

Durante l'attivazione, Lync Server 2013 pubblica le informazioni sul server nelle tre posizioni seguenti in Servizi di dominio Active Directory:

  - Un punto di connessione del servizio (SCP) in ogni oggetto computer di Active Directory corrispondente al computer fisico in cui è installato Lync Server 2013.

  - Oggetti server creati nel contenitore della classe **msRTCSIP-Pools**.

  - Server attendibili specificati nel Generatore di topologie.

## Punti di connessione del servizio

Ogni oggetto di Lync Server 2013 in Servizi di dominio Active Directory presenta un SCP chiamato Servizi RTC, che a sua volta contiene diversi attributi che identificano ogni computer e specificano i relativi servizi forniti. Alcuni dei più importanti attributi SCP sono *serviceDNSName*, *serviceDNSNameType*, *serviceClassname* e *serviceBindingInformation*. Le applicazioni di gestione delle risorse di terze parti possono recuperare le informazioni sul server in una distribuzione eseguendo query su questi e altri attributi SCP.

## Oggetti server di Active Directory

Ogni ruolo server di Lync Server 2013 presenta un oggetto Active Directory corrispondente, i cui attributi definiscono i servizi forniti da tale ruolo. Inoltre, quando si attiva un Server Standard Edition o quando si crea un pool Enterprise Edition, Lync Server 2013 crea un nuovo oggetto **msRTCSIP-Pool** nel contenitore **msRTCSIP-Pools**. La classe **msRTCSIP-Pool** specifica il nome di dominio completo (FQDN) del pool, oltre all'associazione tra componenti front-end e back-end del pool. Un Server Standard Edition viene considerato come un pool logico in cui i componenti front-end e back-end sono collocati in un unico computer.

## Server attendibili

In Lync Server 2013, i server attendibili sono quelli specificati durante l'esecuzione del Generatore di topologie e la pubblicazione della topologia. La topologia pubblicata, incluse tutte le informazioni sul server, viene archiviata nell'archivio di gestione centrale. Solo i server definiti nell'archivio di gestione centrale vengono ritenuti attendibili. In Lync Server 2013, viene ritenuto attendibile un server che soddisfa i seguenti requisiti:

  - L'FQDN del server è presente nella topologia archiviata nell'archivio di gestione centrale.

  - Il server presenta un certificato valido di una CA attendibile. Per informazioni dettagliate, vedere [Requisiti dell'infrastruttura dei certificati per Lync Server 2013](lync-server-2013-certificate-infrastructure-requirements.md).

Se uno di questi requisiti non viene soddisfatto, il server non viene ritenuto attendibile e la connessione viene rifiutata. Questo doppio requisito impedisce eventuali attacchi in cui un server non autorizzato tenta di controllare l'FQDN di un server valido.

Inoltre, per consentire alle distribuzioni di Microsoft Office Communications Server 2007 R2 e Microsoft Office Communications Server 2007 di comunicare con i server di Lync Server 2013, durante la preparazione della foresta Lync Server 2013 crea contenitori che includono gli elenchi dei server attendibili per le versioni precedenti. Nella seguente tabella vengono descritti i contenitori creati per consentire la compatibilità con le distribuzioni precedenti.

### Elenchi server attendibili e relativi contenitori di Active Directory per la compatibilità con le versioni precedenti

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Elenco server attendibili</th>
<th>Contenitore di Active Directory</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Server Standard Edition e server Front End del pool Enterprise</p></td>
<td><p>Servizio RTC/Impostazioni globali</p></td>
</tr>
<tr class="even">
<td><p>Server per conferenze</p></td>
<td><p>Servizio RTC/MCU attendibili</p></td>
</tr>
<tr class="odd">
<td><p>Server componenti Web</p></td>
<td><p>Servizio RTC/TrustedWebComponentsServers</p></td>
</tr>
<tr class="even">
<td><p>Mediation Server e server Communicator Web Access, server applicazioni, registrazione con QoE, servizio A/V Conferencing (anche server SIP di terze parti)</p></td>
<td><p>Servizio RTC/Servizi attendibili</p></td>
</tr>
<tr class="odd">
<td><p>Server proxy</p></td>
<td><p>Lync Server 2013 non supporta la compatibilità con le versioni precedenti per i server proxy</p></td>
</tr>
</tbody>
</table>


Per supportare i server attendibili delle versioni precedenti, è necessario eseguire lo strumento Best Practices Analyzer. Per informazioni dettagliate sull'esecuzione di Best Practices Analyzer, vedere [http://go.microsoft.com/fwlink/p/?LinkId=330633](http://go.microsoft.com/fwlink/p/?linkid=330633).

