---
title: Gestione della qualità del servizio (QoS) in Lync Server 2013
TOCTitle: Gestione della qualità del servizio (QoS) in Lync Server 2013
ms:assetid: ab1051c3-8380-4d72-86df-37a61b1e4a41
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg405409(v=OCS.15)
ms:contentKeyID: 49301625
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Gestione della qualità del servizio (QoS) in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-11-07_

La qualità del servizio (QoS) è una tecnologia di rete utilizzata in alcune organizzazioni per garantire agli utenti finali un'esperienza ottimale per le comunicazioni audio e video. QoS viene utilizzata più comunemente nelle reti in cui la larghezza di banda è limitata. Poiché in questi casi un numero elevato di pacchetti di rete si contende una quantità relativamente ridotta di larghezza di banda disponibile, la qualità del servizio consente agli amministratori di assegnare priorità più alte ai pacchetti che trasportano dati audio o video. Assegnando a questi pacchetti una priorità maggiore, è probabile che le comunicazioni audio e video abbiano luogo più rapidamente e con meno interruzioni rispetto alle sessioni di rete che prevedono trasferimenti di file, l'esplorazione del Web o l'esecuzione di backup di database. Ai pacchetti di rete utilizzati per i trasferimenti di file o i backup di database viene infatti assegnata la maggiore priorità consentita dalla situazione.


> [!NOTE]
> Come regola generale, la qualità del servizio si applica solo alle sessioni di comunicazione nella rete interna. Quando viene implementata, si configurano i server e i router in modo che supportino i pacchetti contrassegnati. È tuttavia possibile configurare questi dispositivi per supportare l'utilizzo di contrassegni nei pacchetti in modo specifico. Non è possibile presupporre che la qualità del servizio sia supportata in Internet o in altre reti. Anche se è supportata in altre reti, non è garantito che sia configurata nello stesso modo in cui il servizio è stato configurato nella propria rete.



Microsoft Lync Server 2013 non richiede la qualità del servizio. Se attualmente non viene utilizzata, non è necessario installare il servizio prima di installare Lync Server 2013. Se va persa una quantità considerevole di pacchetti nella rete, è consigliabile ovviare al problema aggiungendo ulteriore larghezza di banda. Se non è possibile aggiungere larghezza di banda, è opportuno implementare la qualità del servizio.

Lync Server 2013 offre il supporto completo per la qualità del servizio, pertanto le organizzazioni in cui QoS è già in uso possono facilmente integrare Lync Server nell'infrastruttura di rete esistente. A tale scopo, è necessario eseguire le attività seguenti:

  - [Abilitazione di QoS per dispositivi non basati su Windows](lync-server-2013-enabling-qos-for-devices-that-are-not-based-on-windows.md). Per impostazione predefinita, la qualità del servizio è disabilitata per i computer e altri dispositivi, come gli iPhone, che eseguono altri sistemi operativi. Benché sia possibile utilizzare Lync Server per abilitare e disabilitare la qualità del servizio per i dispositivi, in genere non è possibile utilizzare il prodotto per modificare i codici DSCP utilizzati da tali dispositivi.

  - [Configurazione degli intervalli di porte per Conferencing Server, server applicazioni e Mediation Server](lync-server-2013-configuring-port-ranges-for-your-conferencing-application-and-mediation-servers.md). È necessario riservare un set univoco di porte per diversi tipi di pacchetti, ad esempio audio e video. Con Lync Server 2013 non è possibile abilitare o disabilitare la qualità del servizio, ad esempio, impostando su True o False il valore di una proprietà. Per abilitare la qualità del servizio, è invece necessario configurare intervalli di porte e quindi creare e applicare Criteri di gruppo. Se successivamente si decide di non utilizzare più la qualità del servizio, è possibile "disabilitarla" semplicemente rimuovendo gli oggetti Criteri di gruppo appropriati.

  - [Configurazione degli intervalli di porte per i server perimetrali](lync-server-2013-configuring-port-ranges-for-your-edge-servers.md). Sebbene non sia necessario, è possibile configurare i server perimetrali per l'utilizzo degli stessi intervalli di porte degli altri server.

  - [Configurazione degli intervalli di porte per i client Microsoft Lync](lync-server-2013-configuring-port-ranges-for-your-microsoft-lync-clients.md). Questi intervalli di porte si applicano solo ai computer client e in genere sono diversi dagli intervalli di porte configurati nei server.

  - [Configurazione dei criteri di Qualità del servizio (QoS) in Lync Server 2013 per server per conferenze, server applicazioni e Mediation Server](lync-server-2013-configuring-a-quality-of-service-policy-for-your-conferencing-application-and-mediation-servers.md). Questi criteri determinano i codici DSCP applicati ai diversi tipi di pacchetti.

  - [Configurazione di criteri qualità del servizio per i server A/V Edge](lync-server-2013-configuring-a-quality-of-service-policy-for-your-a-v-edge-servers.md). Questa attività deve essere eseguita esclusivamente per il lato interno dei server perimetrali, in quanto la qualità del servizio è progettata per l'utilizzo nella rete interna e non in Internet.

  - [Configurazione dei criteri di qualità del servizio per i client in esecuzione in Windows 7 o Windows 8](lync-server-2013-configuring-quality-of-service-policies-for-clients-running-on-windows-7-or-windows-8.md). Microsoft Lync Server 2013 non supporta la qualità del servizio per altri sistemi operativi Windows, come Windows Vista o Windows XP.

  - [Configurazione di Qualità del servizio (QoS) nei dispositivi Microsoft Lync Phone Edition](lync-server-2013-configuring-quality-of-service-on-microsoft-lync-phone-edition-devices.md). Per impostazione predefinita, la qualità del servizio è abilitata per i dispositivi Lync Phone Edition. È tuttavia possibile modificare il valore DSCP predefinito per essere certi che per tutti i pacchetti audio dell'organizzazione venga utilizzato lo stesso codice DSCP.


> [!NOTE]
> Se si utilizza Microsoft Windows Server 2012 o Windows Server 2012 R2, potrebbe essere utile conoscere il nuovo set di cmdlet di Windows PowerShell disponibile per la gestione di Qualità del servizio nella piattaforma. Per ulteriori informazioni, vedere l'articolo Cmdlet di Qualità del servizio di rete in Windows PowerShell all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=285379">http://go.microsoft.com/fwlink/p/?LinkId=285379</A>.


