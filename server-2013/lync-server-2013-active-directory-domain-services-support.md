---
title: 'Lync Server 2013: Supporto per Servizi di dominio Active Directory'
TOCTitle: Supporto per Servizi di dominio Active Directory
ms:assetid: aeb62d5e-e424-473a-b795-9452150c98dd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412831(v=OCS.15)
ms:contentKeyID: 49301666
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Supporto per Servizi di dominio Active Directory in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-11-07_

Lync Server 2013 utilizza l' archivio di gestione centrale per archiviare i dati di configurazione per i server e i servizi invece di basarsi su Servizi di dominio Active Directory per queste informazioni come in passato. Lync Server 2013 continua ad archiviare quanto segue in Servizi di dominio Active Directory:

  - **Estensioni dello schema**
    
      - Estensioni degli oggetti utente
    
      - Estensioni delle classi di Lync Server 2010 e Office Communications Server 2007 R2 per garantire la compatibilità con le versioni precedenti supportate

  - **Dati** (archiviati nello schema esteso di Lync Server 2013 e nelle classi esistenti)
    
      - URI SIP dell'utente e altre impostazioni utente
    
      - Oggetti contatto per applicazioni, ad esempio applicazione Response Group e applicazione Operatore Conferenza
    
      - Dati pubblicati per la compatibilità con le versioni precedenti
    
      - Punto di controllo del servizio (SCP, Service Control Point) per l' archivio di gestione centrale
    
      - Account di autenticazione Kerberos (un oggetto computer facoltativo)

In questa sezione vengono descritti i requisiti di supporto di Servizi di dominio Active Directory per Lync Server 2013. Per informazioni dettagliate sul supporto della topologia, vedere [Topologie di Active Directory supportate in Lync Server 2013](lync-server-2013-supported-active-directory-topologies.md) nella documentazione relativa al supporto.

## Sistemi operativi del controller di dominio supportati

In Lync Server 2013 sono supportati i controller di dominio che eseguono i sistemi operativi seguenti:

  - Sistema operativo Windows Server 2012 R2

  - Sistema operativo Windows Server 2012

  - sistema operativo Windows Server 2008 R2

  - sistema operativo Windows Server 2008

  - Windows Server 2008 Enterprise a 32 bit

  - Versioni a 32 bit o a 64 bit del sistema operativo Windows Server 2003 R2

  - Versioni a 32 bit o a 64 bit del sistema operativo Windows Server 2003

## Livello funzionale di dominio e di foresta

È necessario elevare tutti i domini in cui si distribuisce Lync Server 2013 a un livello funzionale di dominio corrispondente a Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008 o almeno Windows Server 2003.

Tutte le foreste in cui si distribuisce Lync Server 2013 devono essere elevate a un livello funzionale di foresta corrispondente a Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008 o almeno Windows Server 2003.

## Supporto per controller di dominio in sola lettura

Lync Server 2013 supporta le distribuzioni di Servizi di dominio Active Directory che includono controller di dominio o server di catalogo globale di sola lettura, a condizione che siano disponibili controller di dominio scrivibili.

## Nomi di dominio

Lync Server non supporta domini a etichetta singola. Ad esempio è supportata una foresta con un dominio radice denominato **contoso.local** ma non è supportato un dominio radice denominato **local**. Per informazioni dettagliare, vedere l'articolo 300684 della Microsoft Knowledge Base “Informazioni sulla configurazione di Windows per domini con nomi DNS con etichetta singola” all'indirizzo <http://go.microsoft.com/fwlink/?linkid=143752>.


> [!NOTE]
> Lync Server non supporta la ridenominazione dei domini. Per rinominare un dominio in cui è distribuito Lync Server, è innanzitutto necessario disinstallare Lync Server, quindi rinominare il dominio e infine reinstallare Lync Server.



## Ambienti Servizi di dominio Active Directory bloccati

In un ambiente Servizi di dominio Active Directory bloccato gli oggetti utente e computer vengono spesso inseriti in unità organizzative specifiche in cui l'ereditarietà delle autorizzazioni è disabilitata per semplificare la protezione della delega dell'amministrazione e consentire l'utilizzo di oggetti Criteri di gruppo per l'applicazione di criteri di sicurezza. Lync Server 2013 può essere distribuito in un ambiente Active Directory bloccato. Per informazioni dettagliate sugli elementi necessari per la distribuzione di Lync Server in un ambiente bloccato, vedere [Preparazione di un ambiente Servizi di dominio Active Directory bloccato in Lync Server 2013](lync-server-2013-preparing-a-locked-down-active-directory-domain-services.md) nella documentazione relativa alla distribuzione.

