---
title: 'Lync Server 2013: Linee guida per la distribuzione di VoIP aziendale'
TOCTitle: Linee guida per la distribuzione di VoIP aziendale
ms:assetid: 8985bd93-7613-4cef-9c89-51df6049ed9b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398694(v=OCS.15)
ms:contentKeyID: 49301237
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Linee guida per la distribuzione di VoIP aziendale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

In questo argomento vengono descritti i prerequisiti e altre linee guida che è consigliabile considerare quando si pianifica la distribuzione del carico di lavoro di Lync Server 2013 e di VoIP aziendale.

## Prerequisiti per la distribuzione

Per distribuire VoIP aziendale in modo ottimale, verificare che l'infrastruttura IT, la rete e i sistemi soddisfino i prerequisiti seguenti:

  - Lync Server 2013 Standard Edition o Enterprise Edition è installato e funzionante nella rete.

  - Tutti i server perimetrali sono distribuiti e funzionanti nella rete perimetrale, inclusi i server perimetrali con servizio Access Edge, servizio A/V Edge, servizio Web Conferencing Edge e un proxy inverso.

  - Uno o più utenti sono stati creati e abilitati per Lync Server.

  - Microsoft Exchange Server 2007 Service Pack 1 (SP1) o Service Pack più recente oppure Microsoft Exchange Server 2010 è necessario per l'integrazione della Messaggistica unificata di Exchange con Lync Server e per fornire funzionalità avanzate di notifica e informazioni dei registri chiamate agli endpoint client.

  - Per ogni utente da abilitare per VoIP aziendale è stato designato, normalizzato e copiato nell'attributo **msRTCSIP-line** un numero di telefono primario.
    

    > [!NOTE]
    > Lync Server supporta i numeri E.164 e non DID (Direct Inward Dialing). I numeri non DID possono essere rappresentati nel formato <STRONG>&lt;E.164&gt;;ext=&lt;extension&gt;</STRONG> o come stringa di cifre, con il requisito che l'estensione privata sia univoca nell'organizzazione. Un numero privato 1001 può ad esempio essere rappresentato come <STRONG>+1425550100;ext=1001</STRONG> o come <STRONG>1001</STRONG>. Quando rappresentato come <STRONG>1001</STRONG>, tale numero deve essere univoco nell'organizzazione.



  - Gli amministratori che distribuiscono VoIP aziendale devono essere membri del gruppo RTCUniversalServerAdmins.

  - Almeno Office Communicator 2007 è distribuito correttamente. Per utilizzare le nuove caratteristiche introdotte in questa versione, è necessario Lync 2013.

  - L'infrastruttura MKI (Managed Key Infrastructure) è distribuita e configurata mediante un'infrastruttura Microsoft o di un'Autorità di certificazione (CA, Certification Authority) di terze parti.

  - Ogni computer in cui si installa Mediation Server deve avere le caratteristiche seguenti:
    
      - Essere un server membro di un dominio e preparato per Servizi di dominio Active Directory. Per le procedure di preparazione di Servizi di dominio Active Directory, vedere [Preparazione di Servizi di dominio Active Directory per Lync Server 2013](lync-server-2013-preparing-active-directory-domain-services.md) nella documentazione relativa alla distribuzione.
    
      - Eseguire uno dei sistemi operativi seguenti:
        
          -   
            Windows Server 2008 Standard a 64 bit
        
          -   
            Windows Server 2008 Enterprise a 64 bit

  - Se la connessione alla rete PSTN o al sistema PBX viene eseguita tramite una connessione TDM (Time Division Multiplexing), sono disponibili uno o più gateway PSTN per la distribuzione. Se la connessione avviene tramite un trunk SIP, non è necessario un gateway PSTN.

## Interruzioni dell'alimentazione, della rete o del servizio telefonico

Se si verifica un'interruzione, un disturbo o un decadimento di altro tipo dell'alimentazione, della rete o del servizio telefonico, è possibile che i servizi di comunicazione vocale, messaggistica istantanea e presenza nonché le altre caratteristiche di Lync Server e di qualsiasi dispositivo collegato a Lync Server non funzionino correttamente.

## VoIP aziendale dipende dalla disponibilità del server e dall'operatività hardware e dei client vocali

Le comunicazioni vocali tramite Lync Server dipendono dalla disponibilità del software server e dal corretto funzionamento dei client vocali o dei dispositivi telefonici connessi al software server.

## Metodi alternativi di accesso ai servizi di emergenza

Per le posizioni in cui si installa un client vocale, ad esempio un PC che esegue Lync o un dispositivo Lync Phone Edition, è consigliabile mantenere un'opzione di backup per gli utenti che chiamano i servizi di emergenza, ad esempio il 113, in caso di interruzione dell'alimentazione, decadimento della connettività di rete, interruzione del servizio telefonico o problemi di altro tipo che potrebbero impedire il funzionamento di Lync Server, Lync o dei dispositivi Lync Phone Edition. Tali opzioni alternative possono includere un telefono connesso a una linea PSTN (Public Switched Telephone Network) standard o un telefono cellulare.

## Chiamate di emergenza e sistemi telefonici multilinea

L'utilizzo di un sistema telefonico multilinea (MTLS, Multiline Telephone System) può essere soggetto alle leggi statali e/o federali degli Stati Uniti e di altri paesi che obbligano a mostrare in chiaro ai servizi di emergenza il numero di telefono, l'interno e/o la località del chiamante quando quest'ultimo effettua una chiamata di emergenza (ad esempio, il 113). In questa versione, è possibile configurare Lync Server per fornire la posizione fisica del chiamante a un provider di servizi di emergenza, come descritto in [Pianificazione per i servizi di emergenza (E9-1-1) in Lync Server 2013](lync-server-2013-planning-for-emergency-services-e9-1-1.md). La conformità con le leggi per i sistemi MTLS è esclusivamente di responsabilità dell'acquirente di Lync Server, del client Lync e di dispositivi Lync Phone Edition.

