---
title: 'Lync Server 2013: Topologie di Active Directory supportate'
TOCTitle: Topologie di Active Directory supportate
ms:assetid: 0c76b778-7652-4eb0-b161-86f2d4a94ccf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398173(v=OCS.15)
ms:contentKeyID: 49299660
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Topologie di Active Directory supportate in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-10-02_

Lync Server 2013 supporta le stesse topologie Servizi di dominio Active Directory di Microsoft Lync Server 2010 e Microsoft Office Communications Server 2007 R2. Le topologie supportate sono:

  - Foresta singola con singolo dominio

  - Foresta singola con albero singolo e più domini

  - Foresta singola con più alberi e spazi dei nomi disgiunti

  - Più foreste in una topologia di foreste centralizzate

  - Più foreste in una topologia di foresta di risorse

  - Più foreste in una topologia di foreste delle risorse Lync con Exchange Online

Nella figura seguente vengono identificate le icone utilizzate nelle illustrazioni di questa sezione.

**Legenda per le illustrazioni relative alle topologie**

![Legenda per le illustrazioni relative alle topologie](images/Gg398173.0c3cc89f-6c43-4bc8-b2ec-61d89e391ee9(OCS.15).jpg "Legenda per le illustrazioni relative alle topologie")

## Foresta singola, dominio singolo

La topologia di Active Directory più semplice supportata da Lync Server, una foresta a dominio singolo, è molto diffusa.

Nella figura seguente viene illustrata una distribuzione di Lync Server in una topologia di Active Directory a dominio singolo.

**Topologia a un solo dominio**

![Topologia a un solo dominio](images/Gg398173.258b3b3f-0558-4a36-a4c2-031be7299668(OCS.15).jpg "Topologia a un solo dominio")

## Foresta singola, più domini

Un'altra topologia di Active Directory supportata da Lync Server è una foresta singola costituita da un dominio radice e uno o più domini figlio. In questo tipo di topologia di Active Directory il dominio in cui vengono creati gli utenti può essere diverso dal dominio in cui viene distribuito Lync Server. Se però si distribuisce un pool Front End, sarà necessario distribuire tutti i Front End Server del pool in un singolo dominio. Il supporto di Lync Server per i gruppi di amministratori universali di Windows consente l'amministrazione tra domini.

Nella figura seguente viene illustrata una distribuzione in una foresta singola con più domini. In questa figura un'icona utente indica il dominio in cui si trova l'account utente e la freccia punta al dominio in cui risiede il pool di Lync Server. Gli account utente includono i seguenti:

  - Account utente all'interno dello stesso dominio del pool di Lync Server

  - Account utente in un dominio diverso da quello del pool di Lync Server

  - Account utente in un dominio figlio del dominio con il pool di Lync Server

**Foresta singola con più domini**

![Foresta singola con più domini](images/Gg398173.2b809c72-c3cd-4fad-afe6-8c2dae779750(OCS.15).jpg "Foresta singola con più domini")

## Foresta singola, più alberi

Una topologia di foresta a più alberi è costituita da due o più domini che definiscono strutture ad albero indipendenti e spazi dei nomi di Active Directory separati.

Nella figura seguente viene illustrata una foresta singola con più alberi. In questa figura un'icona utente indica il dominio in cui si trova l'account utente, una linea continua punta a un pool di Lync Server che si trova nello stesso dominio o in uno diverso e una linea tratteggiata punta a un pool di Lync Server che si trova in un albero diverso. Gli account utente includono i seguenti:

  - Account utente all'interno dello stesso dominio del pool di Lync Server

  - Account utente in un dominio diverso da quello del pool di Lync Server (ma nello stesso albero)

  - Account utente in un albero diverso da quello del pool di Lync Server

**Foresta singola con più alberi**

![Foresta singola con più alberi](images/Gg398173.db30fa49-174a-4974-8695-41dd78e39432(OCS.15).jpg "Foresta singola con più alberi")

## Più foreste, foresta centralizzata

Lync Server supporta più foreste configurate in una topologia a foresta centralizzata. Le topologie a foresta centralizzata utilizzano oggetti contatto nella foresta centralizzata per rappresentare gli utenti delle altre foreste. La foresta centralizzata inoltre ospita gli account di qualsiasi utente di questa foresta. Un prodotto di sincronizzazione della directory, come Microsoft Identity Integrati Server (MIIS), Microsoft Forefront Identity Manager (FIM) 2010 o Microsoft Identity Lifecycle Manager (ILM) 2007 Feature Pack 1 (FP1), gestisce il ciclo di vita degli account utente all'interno dell'organizzazione. Quando perciò viene creato un nuovo account utente in una delle foreste o viene eliminato un account utente da una foresta, il prodotto di sincronizzazione della directory sincronizza il contatto corrispondente nella foresta centralizzata.

Una foresta centralizzata presenta i vantaggi seguenti:

  - I server che eseguono Lync Server sono centralizzati all'interno di una singola foresta.

  - Gli utenti possono cercare altri utenti e comunicare con loro in qualsiasi foresta.

  - Gli utenti possono visualizzare la presenza di altri utenti in qualsiasi foresta.

  - Il prodotto di sincronizzazione della directory automatizza l'aggiunta e l'eliminazione di oggetti contatto nella foresta centralizzata durante la creazione o la rimozione di account utente.

Nella figura seguente viene illustrata una topologia a foresta centralizzata. In questa figura sono presenti due relazioni di trust bidirezionali tra il dominio che ospita Lync Server, che si trova nella foresta centralizzata, e ogni dominio di soli utenti, che si trova in una foresta separata. Non è necessario estendere lo schema nelle foreste degli utenti separate.

**Topologia a foresta centralizzata**

![Topologia a foresta centralizzata](images/Gg398173.7feb049a-453b-4134-9128-873b83ee1755(OCS.15).jpg "Topologia a foresta centralizzata")

## Più foreste, foresta delle risorse

In una topologia con foresta delle risorse una foresta è dedicata all'esecuzione delle applicazioni server, ad esempio Microsoft Exchange Server e Lync Server. La foresta delle risorse ospita le applicazioni server e una rappresentazione sincronizzata dell'oggetto utente attivo, ma non contiene alcun account utente abilitato per l'accesso. La foresta delle risorse funge da ambiente dei servizi condivisi per le altre foreste in cui risiedono gli oggetti utente. Le foreste degli utenti presentano una relazione di trust a livello di foresta con la foresta delle risorse. Quando si distribuisce Lync Server in questo tipo di topologia, si crea un oggetto utente disabilitato nella foresta delle risorse per ogni account utente nelle foreste degli utenti. Se Microsoft Exchange è già distribuito nella foresta delle risorse, gli account utente disabilitati potrebbero già esistere. Un prodotto di sincronizzazione della directory, come MIIS, Microsoft Forefront Identity Manager (FIM) 2010 o Microsoft Identity Lifecycle Manager (ILM) 2007 Feature Pack 1 (FP1), gestisce il ciclo di vita degli account utente. Quando un nuovo account utente viene creato in una delle foreste degli utenti o un account utente viene eliminato da una foresta, il prodotto di sincronizzazione della directory sincronizza la rappresentazione dell'utente corrispondente nella foresta delle risorse.

Questa topologia può essere utilizzata per fornire un'infrastruttura condivisa per i servizi in organizzazioni che gestiscono più foreste o per separare l'amministrazione degli oggetti di Active Directory da un'altra amministrazione. Si tratta della scelta più frequente da parte delle società che hanno la necessità di isolare l'amministrazione di Active Directory per motivi di sicurezza.

Questa topologia offre il vantaggio di limitare la necessità di estendere lo schema di Active Directory a una singola foresta, ovvero la foresta delle risorse.

Nella figura seguente viene illustrata la topologia con foresta delle risorse.

**Topologia con foresta delle risorse**

![Topologia con foresta delle risorse di Active Directory](images/Gg398173.54ab82f1-e9e5-40f0-a54e-86e340b65c2a(OCS.15).jpg "Topologia con foresta delle risorse di Active Directory")

## Più foreste in una topologia di foreste delle risorse Lync con Exchange Online

In questa topologia una o più foreste si trovano in locale e ospitano account utente Active Directory. La foresta delle risorse si trova non in locale ed è gestita da un provider di hosting di terze parti. La foresta delle risorse contiene soltanto la distribuzione Lync Server e una replica sincronizzata degli account utente dalle foreste degli account utente in locale. La foresta non contiene account utente abilitati per l'accesso. Exchange viene distribuito nelle foreste degli account utente in locale integrate con Exchange Online (configurazione ibrida). In alternativa, i servizi di posta elettronica per gli account utente in locale vengono forniti esclusivamente da Exchange Online.

La foresta delle risorse funge da ambiente dei servizi condivisi per le foreste di Active Directory in locale in cui risiedono gli oggetti utente. Le foreste di account utente presentano una relazione di trust a livello di foresta unidirezionale con la foresta delle risorse. Quando si distribuisce Lync Server in questo tipo di topologia, si crea un oggetto utente disabilitato nella foresta delle risorse per ogni account utente nelle foreste degli utenti. Un prodotto di sincronizzazione della directory, come MIIS, Microsoft Forefront Identity Manager (FIM) 2010 o Microsoft Identity Lifecycle Manager (ILM) 2007 Feature Pack 1 (FP1), gestisce il ciclo di vita degli account utente. Quando viene creato un nuovo account utente in una delle foreste degli utenti o viene eliminato un account utente da una foresta, il prodotto di sincronizzazione della directory sincronizza la rappresentazione dell'utente corrispondente nella foresta delle risorse. Per ulteriori informazioni sulla configurazione di una distribuzione a più foreste, vedere [Deploying Lync in a Multi-Forest Architecture (Partner Hosted Lync with Exchange Hybrid)](http://go.microsoft.com/fwlink/p/?linkid=513216).

