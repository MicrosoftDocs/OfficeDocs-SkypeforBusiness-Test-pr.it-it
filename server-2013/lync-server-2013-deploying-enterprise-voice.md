---
title: 'Lync Server 2013: Distribuzione di VoIP aziendale'
TOCTitle: Distribuzione di VoIP aziendale
ms:assetid: b5b593a6-ac30-461c-8c8c-0041e2c9ab04
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412876(v=OCS.15)
ms:contentKeyID: 49301729
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuzione di VoIP aziendale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-03_

VoIP aziendale di Lync Server 2013 fa parte dell'infrastruttura di Lync Server 2013.

Per distribuire VoIP aziendale, è necessario eseguire le operazioni seguenti:

1.  Leggere la sezione [Pianificazione di VoIP aziendale in Lync Server 2013](lync-server-2013-planning-for-enterprise-voice.md) della documentazione relativa alla pianificazione.

2.  Finalizzare i piani per le funzionalità e i componenti da distribuire con questo carico di lavoro.

3.  Eseguire Strumento di pianificazione per progettare una topologia che rispecchi le decisioni a livello di distribuzione.

4.  Aprire il progetto della topologia in Generatore di topologie, come descritto in [Definizione e configurazione della topologia in Lync Server 2013](lync-server-2013-defining-and-configuring-the-topology.md) nella documentazione relativa alla distribuzione.
    

    > [!NOTE]
    > L'installazione di Generatore di topologie fa parte del processo di distribuzione per il pool interno. Per informazioni dettagliate, vedere <A href="lync-server-2013-install-lync-server-administrative-tools.md">Installare gli strumenti di amministrazione di Lync Server 2013</A> nella documentazione relativa alla distribuzione.



È inoltre necessario avere già distribuito Lync Server Enterprise Edition nei siti centrali e nei siti di succursale corrispondenti alla topologia di riferimento scelta per la distribuzione. Non è possibile distribuire componenti di VoIP aziendale fino a quando non si completano la definizione, la pubblicazione e l'installazione dei file per almeno un pool interno ed è necessario utilizzare Generatore di topologie per definire e pubblicare un pool interno.

Per visualizzare le topologie di riferimento con esempi delle posizioni in cui è possibile distribuire i ruoli del server di VoIP aziendale, nonché la relazione reciproca tra i ruoli e con altri ruoli del server di Lync Server 2013, vedere [Topologie di riferimento in Lync Server 2013](lync-server-2013-reference-topologies.md) nella documentazione relativa alla pianificazione.

Per visualizzare una topologia di riferimento che illustra e spiega una semplice distribuzione di controllo di ammissione di chiamata, inclusi siti di rete, aree di rete e subnet, vedere [Esempio: raccolta dei requisiti dell'organizzazione per il controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-example-of-gathering-your-requirements-for-call-admission-control.md) nella documentazione relativa alla pianificazione.

> [!IMPORTANT]  
> Per distribuire VoIP aziendale in un sito centrale, continuare con la lettura degli argomenti in questa sezione. Per distribuire VoIP aziendale in un sito di succursale, passare a <a href="lync-server-2013-deploying-branch-sites.md">Distribuzione di siti di succursale in Lync Server 2013</a> nella documentazione relativa alla distribuzione.

In questa sezione sono incluse le procedure per le distribuzioni con un Mediation Server collocato in ogni Front End Server o server Standard Edition, come consigliato, nonché per le distribuzioni con un pool Mediation Server autonomo.

È possibile ignorare il contenuto seguente se è stato utilizzato Generatore di topologie per definire e pubblicare una topologia con collocazione di un Mediation Server in ogni Front End Server o server Standard Edition, perché i file per il Mediation Server sono già stati installati automaticamente dalla Distribuzione guidata durante l'installazione dei file per il pool Front End Server o il server Standard Edition:

  - [Configurazione di trunk in Lync Server 2013](lync-server-2013-configuring-trunks.md)

Se è stato utilizzato Generatore di topologie per definire e pubblicare un Mediation Server in un pool autonomo, è possibile utilizzare il contenuto seguente:

  - Verificare che la topologia soddisfi i prerequisiti a livello di software e ambiente, come descritto in [Prerequisiti di VoIP aziendale per Lync Server 2013](lync-server-2013-enterprise-voice-prerequisites.md).

## Contenuto della sezione

  -   
    [Prerequisiti di VoIP aziendale per Lync Server 2013](lync-server-2013-enterprise-voice-prerequisites.md)

  -   
    [Distribuzione di Mediation Server e definizione di peer in Lync Server 2013](lync-server-2013-deploying-mediation-servers-and-defining-peers.md)

  -   
    [Configurazione di trunk in Lync Server 2013](lync-server-2013-configuring-trunks.md)

  -   
    [Configurazione dei dial plan in Lync Server 2013](lync-server-2013-configuring-dial-plans.md)

  -   
    [Configurazione di criteri vocali, record di utilizzo PSTN e route vocali in Lync Server 2013](lync-server-2013-configuring-voice-policies-pstn-usage-records-and-voice-routes.md)

  -   
    [Esportazione e importazione della configurazione di route vocali in Lync Server 2013](lync-server-2013-exporting-and-importing-voice-routing-configuration.md)

  -   
    [Testare il routing vocale in Lync Server 2013](lync-server-2013-test-voice-routing.md)

  -   
    [Pubblicare le modifiche in sospeso alla configurazione del routing vocale in Lync Server 2013](lync-server-2013-publish-pending-changes-to-the-voice-routing-configuration.md)

  -   
    [Distribuzione della messaggistica unificata di Exchange in locale per fornire la funzionalità di segreteria telefonica di Lync Server 2013](lync-server-2013-deploying-on-premises-exchange-um-to-provide-lync-server-2013-voice-mail.md)

  -   
    [Fornire agli utenti di Lync Server 2013 la segreteria telefonica nella messaggistica unificata di Exchange ospitata](lync-server-2013-providing-lync-server-users-voice-mail-on-hosted-exchange-um.md)

  -   
    [Configurazione dell'integrazione di Lync Server 2013 locale con Exchange Online](lync-server-2013-configuring-on-premises-lync-server-integration-with-exchange-online.md)

  -   
    [Distribuzione delle funzionalità di VoIP aziendale avanzate in Lync Server 2013](lync-server-2013-deploying-advanced-enterprise-voice-features.md)
    
      - [Informazioni su aree di rete, siti e subnet in Lync Server 2013](lync-server-2013-about-network-regions-sites-and-subnets.md)
    
      - [Creare o modificare un'area di rete in Lync Server 2013](lync-server-2013-create-or-modify-a-network-region.md)
    
      - [Creare o modificare un sito di rete in Lync Server 2013](lync-server-2013-create-or-modify-a-network-site.md)
    
      - [Associare una subnet a un sito di rete in Lync Server 2013](lync-server-2013-associate-a-subnet-with-a-network-site.md)
    
      - [Configurare il controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-configure-call-admission-control.md)
    
      - [Configurare i servizi di emergenza avanzati in Lync Server 2013](lync-server-2013-configure-enhanced-9-1-1.md)
    
      - [Configurare il bypass multimediale in Lync Server 2013](lync-server-2013-configure-media-bypass.md)

  -   
    [Abilitare gli utenti per VoIP aziendale in Lync Server 2013](lync-server-2013-enable-users-for-enterprise-voice.md)

## Vedere anche

#### Ulteriori risorse

[Distribuzione di siti di succursale in Lync Server 2013](lync-server-2013-deploying-branch-sites.md)  
[Configurazione di conferenze telefoniche con accesso esterno in Lync Server 2013](lync-server-2013-configuring-dial-in-conferencing.md)  
[Configurazione del parcheggio di chiamata in Lync Server 2013](lync-server-2013-configuring-call-park.md)  
[Configurazione degli annunci per i numeri non assegnati in Lync Server 2013](lync-server-2013-configuring-announcements-for-unassigned-numbers.md)  
[Distribuzione del monitoraggio in Lync Server 2013](lync-server-2013-deploying-monitoring.md)

