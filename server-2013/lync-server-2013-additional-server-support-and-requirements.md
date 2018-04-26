---
title: 'Lync Server 2013: Requisiti e supporto per i server aggiuntivi'
TOCTitle: Requisiti e supporto per i server aggiuntivi
ms:assetid: 7622986b-abd6-4f45-8b5b-d5e2368521e8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398577(v=OCS.15)
ms:contentKeyID: 49301014
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti e supporto per i server aggiuntivi in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-12-09_

Oltre al supporto software descritto in altre sezioni di questa documentazione relativa al supporto, in Lync Server 2013 vengono applicate le limitazioni seguenti:

  - Lync Server 2013 supporta bilanciamento del carico di rete DNS (Domain Name System) e hardware per ruoli del server specifici. Laddove appropriato, è inoltre supportato il bilanciamento del carico delle applicazioni per Mediation Server. Per informazioni dettagliate su quando utilizzare ciascun tipo di bilanciamento del carico, vedere la documentazione relativa alla pianificazione.

  - Lync Server 2013 utilizza il protocollo DLX (Distribution List Expansion) per espandere le liste di distribuzione. Questo protocollo specifica inoltre il metodo del servizio Web utilizzato per ottenere i membri di una lista di distribuzione. Microsoft Exchange Server supporta gruppi dinamici a cui non sono assegnati membri staticamente. In tali gruppi sono invece archiviate query valutate durante l'espansione del gruppo. Il protocollo DLX non supporta le liste di distribuzione dinamiche.

  - Poiché la procedura guidata Abilita utenti non supporta la conversione automatica di caratteri non inglesi in un URI compatibile con SIP, è necessario modificare l'indirizzo SIP manualmente.

  - Per i server che eseguono software antivirus, fare riferimento a [Esclusioni dall'analisi antivirus per Lync Server 2013](lync-server-2013-antivirus-scanning-exclusions.md) per suggerimenti sulle esclusioni e per altre raccomandazioni correlate alla sicurezza.

  - Se si utilizza IPsec, è consigliabile disabilitarlo negli intervalli di porte utilizzati per il traffico audio e video. Per informazioni dettagliate, vedere [Eccezioni Ipsec in Lync Server 2013](lync-server-2013-ipsec-exceptions.md) nella documentazione relativa alla pianificazione.

  - Se l'organizzazione utilizza un'infrastruttura Qualità del servizio (QoS), il sottosistema multimediale è progettato per il funzionamento all'interno di questa infrastruttura esistente. Per informazioni dettagliate sull'implementazione di QoS, vedere [Gestione della qualità del servizio (QoS) in Lync Server 2013](lync-server-2013-managing-quality-of-service-qos.md) nella documentazione relativa alle operazioni.

  - L'utilizzo del firewall del sistema operativo è supportato. Lync Server 2013 gestisce le eccezioni per il firewall del sistema operativo, ma non per quello del software per database Microsoft SQL Server. Per informazioni dettagliate sui requisiti del firewall di SQL Server, vedere la documentazione di SQL Server.

  - Le interfacce esterne utilizzate per implementare il supporto per l'accesso utente esterno devono trovarsi in una subnet distinta e *non* nella stessa rete delle interfacce interne.

  - La funzionalità XMPP di Lync Server 2013 è testata e supportata da Microsoft per la federazione di messaggistica istantanea con Google Talk. Per altri sistemi XMPP, contattare il fornitore di terze parti per verificare l'eventuale supporto della federazione con Lync Server 2013 e per indicazioni per la distribuzione o la risoluzione dei problemi.

  - Con il rilascio degli aggiornamenti cumulativi per Lync Server 2013 di giugno 2013, Lync Server 2013 supporta ora l'autenticazione a due fattori. Per altre informazioni, vedere [Pianificazione e distribuzione dell'autenticazione a due fattori in Lync Server 2013](lync-server-2013-planning-for-and-deploying-two-factor-authentication.md).

  - La maggior parte dei server interni richiede un tipo di certificato definito come **Open Authentication** (OAuth). È necessario richiedere e assegnare il certificato OAuth durante la fase **Richiesta, installazione o assegnazione dei certificati** di Distribuzione guidata di Lync Server. La dimensione minima di una chiave del certificato OAuth è pari a 1.024 bit. Se si richiede un certificato la cui chiave ha una lunghezza minore di 2.048 bit, potrebbe essere visualizzato un messaggio di avvertimento. Per evitare problemi potenziali qualora venisse applicata una chiave di 2.048 bit senza che sia ricevuto un avvertimento, è consigliabile utilizzare sempre una chiave da 2.048 bit per i certificati OAuth.

  - Lync Server 2013 e Microsoft Exchange Server 2010 Service Pack 1 (SP1) supportano gli algoritmi FIPS (Federal Information Processing Standard) 140-2 se i sistemi operativi Windows Server 2008 R2 sono configurati per l'utilizzo degli algoritmi FIPS 140-2 per la crittografia di sistema. Per implementare il supporto FIPS, è necessario configurare a tale scopo ogni server che esegue Lync Server 2013. Per informazioni dettagliate sugli algoritmi compatibili con FIPS e su come implementare il supporto FIPS, vedere l'articolo 811833 della Microsoft Knowledge Base, "Crittografia di sistema: utilizzare FIPS algoritmi compatibili per crittografia, hash e firma' effetti di impostazione di protezione in Windows XP e versioni successive di Windows" all'indirizzo <http://support.microsoft.com/kb/811833>. Per informazioni dettagliate sul supporto FIPS 140-2 e le limitazioni in Exchange 2010, vedere "Exchange 2010 SP1 e supporto per gli algoritmi compatibili con FIPS" all'indirizzo <http://go.microsoft.com/fwlink/?linkid=205335>.

Lync Server 2013 richiede l'installazione di altro software in componenti specifici prima o durante la distribuzione. Tale software include quello disponibile con il sistema operativo, software scaricabile e software installato automaticamente durante l'installazione di Lync Server 2013. Di seguito è disponibile un elenco di software aggiuntivo che può essere necessario:

  - Windows Update

  - Windows Identity Foundation

  - Microsoft .NET 4.5 Framework

  - Microsoft Visual C++ 2012 Redistributable
    

    > [!NOTE]
    > Microsoft Visual C++ 2012 Redistributable è installato automaticamente quando si installa Lync Server 2013. Non installare o utilizzare una versione diversa.



  - URL Rewrite Module 2.0 Redistributable

  - Runtime formato Windows Media

  - Windows PowerShell versione 3,0

  - Plug-in del browser Microsoft Silverlight 4 (Silverlight 4.0.50524.0 o la versione più recente per il Pannello di controllo di Lync Server)

  - Strumenti per Servizi di dominio Active Directory

Alcuni di questi requisiti software si applicano solo a ruoli del server o componenti specifici. Per informazioni dettagliate su questi requisiti software, vedere [Requisiti software aggiuntivi per Lync Server 2013](lync-server-2013-additional-software-requirements.md) nella documentazione relativa alla pianificazione.

