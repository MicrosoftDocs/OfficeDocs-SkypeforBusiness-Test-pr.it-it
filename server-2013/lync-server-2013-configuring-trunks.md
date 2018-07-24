---
title: 'Lync Server 2013: Configurazione di trunk'
TOCTitle: Configurazione di trunk
ms:assetid: 0c339511-a185-484e-94f0-dbe918b7e48a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398170(v=OCS.15)
ms:contentKeyID: 49299653
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione di trunk in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Durante la distribuzione di VoIP aziendale, configurare un trunk tra un Mediation Server e uno o più dei peer seguenti per garantire la connettività PSTN per i dispositivi e i client di VoIP aziendale nell'organizzazione:

  - Connessione con trunk SIP a un provider di servizi di telefonia Internet (ITSP)

  - Gateway PSTN

  - Centralino (PBX)

Per informazioni dettagliate, vedere [Pianificazione per la connettività PSTN in Lync Server 2013](lync-server-2013-planning-for-pstn-connectivity.md) nella documentazione relativa alla pianificazione.

> [!important]  
> Prima di iniziare la configurazione del trunk, verificare che la topologia sia stata creata e che il Mediation Server e il relativo peer siano stati configurati e associati l'uno all'altro. Per informazioni dettagliate, vedere <a href="lync-server-2013-define-a-gateway-in-topology-builder.md">Definire un gateway in Generatore di topologie in Lync Server 2013</a> nella documentazione relativa alla distribuzione.


> [!NOTE]
> Durante la configurazione del trunk, è possibile abilitare la funzionalità di bypass multimediale di Lync Server 2013, che consente ai dati multimediali di ignorare il Mediation Server. I trunk possono essere configurati con o senza il bypass multimediale abilitato, ma è consigliabile abilitarlo. Per informazioni dettagliate, vedere <A href="lync-server-2013-planning-for-media-bypass.md">Pianificazione del bypass multimediale in Lync Server 2013</A> nella documentazione relativa alla pianificazione.



## Argomenti della sezione

  - [Supporto per più trunk in Lync Server 2013](lync-server-2013-multiple-trunk-support.md)

  - [Routing tra trunk in Lync Server 2013](lync-server-2013-inter-trunk-routing.md)

  - [Visualizzare le informazioni sulla configurazione dei trunk](lync-server-2013-view-trunk-configuration-information.md)

  - [Configurare un trunk con bypass multimediale in Lync Server 2013](lync-server-2013-configure-a-trunk-with-media-bypass.md)

  - [Configurare un trunk senza bypass multimediale in Lync Server 2013](lync-server-2013-configure-a-trunk-without-media-bypass.md)

  - [Creare una nuova raccolta di impostazioni di configurazione trunk](lync-server-2013-create-a-new-collection-of-trunk-configuration-settings.md)

  - [Eliminare una raccolta esistente di impostazioni di configurazione di trunk SIP](lync-server-2013-delete-an-existing-collection-of-sip-trunk-configuration-settings.md)

  - [Modificare le impostazioni di configurazione dei trunk SIP](lync-server-2013-modify-sip-trunk-configuration-settings.md)

  - [Testare le impostazioni di configurazione dei trunk SIP](lync-server-2013-test-sip-trunk-configuration-settings.md)

  - [Visualizzare informazioni sui singoli trunk SIP](lync-server-2013-view-information-about-individual-sip-trunks.md)

## Vedere anche

#### Attività

[Definire un gateway in Generatore di topologie in Lync Server 2013](lync-server-2013-define-a-gateway-in-topology-builder.md)  

#### Ulteriori risorse

[Pianificazione per la connettività PSTN in Lync Server 2013](lync-server-2013-planning-for-pstn-connectivity.md)  
[Pianificazione del bypass multimediale in Lync Server 2013](lync-server-2013-planning-for-media-bypass.md)

