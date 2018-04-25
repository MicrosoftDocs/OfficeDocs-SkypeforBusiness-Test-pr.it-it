---
title: Siti di Lync Server 2013
TOCTitle: Siti
ms:assetid: 022cb6dd-37e2-4882-a53e-5ddfdbc6f53a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398076(v=OCS.15)
ms:contentKeyID: 49299495
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Siti di Lync Server per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-16_

Nel Lync Server è possibile definire nella rete *siti* contenenti componenti di Lync Server. Un sito è un insieme di computer connessi attraverso una rete a bassa latenza e alta velocità, come una singola rete LAN o due reti connesse tramite una rete a fibra ottica ad alta velocità. Si noti che i siti di Lync Server sono concettualmente diversi dai siti Servizi di dominio Active Directory e di Microsoft Exchange Server. I propri siti di Lync Server non devono necessariamente corrispondere ai propri siti Active Directory.

## Tipi di sito

Ogni sito è un *sito centrale* , contenente almeno un pool Front End o un server Standard Edition oppure un *sito di succursale* . Ogni sito di succursale è associato esattamente a un sito centrale e gli utenti del sito di succursale ottengono gran parte delle funzionalità di Lync Server dai server presso il sito centrale associato.

Ogni sito di succursale contiene uno degli elementi seguenti:

  - Un *Survivable Branch Appliance (SBA)* , che è un blade server standard del settore con un server di registrazione Lync Server e un Mediation Server in esecuzione su Windows Server. Nel Survivable Branch Appliance è inoltre incluso un gateway PSTN (Public Switched Telephone Network. Il Survivable Branch Appliance è progettato per siti di succursale aventi da 25 a 1000 utenti.

  - Un *Survivable Branch Server (SBS)* , che è un server che esegue Windows Server, che soddisfa i requisiti hardware specificati e in cui è installato il software per la funzione di registrazione e il Mediation Server di Lync Server. Deve connettersi a un gateway PSTN o a un trunk SIP verso un provider di servizi telefonici. Il Survivable Branch Server è progettato per siti di succursale aventi da 1000 a 5000 utenti.

  - Un gateway PSTN e, facoltativamente, un *Mediation Server* . Per informazioni dettagliate su questo e altri ruoli server, vedere [Ruoli del server in Lync Server 2013](lync-server-2013-server-roles.md).

In un sito di succursale con un collegamento WAN (Wide Area Network) resiliente a un sito centrale è possibile utilizzare la terza opzione, ovvero un gateway PSTN e facoltativamente un Mediation Server. Nei siti di succursale con collegamenti meno resilienti è consigliabile utilizzare un Survivable Branch Appliance o un Survivable Branch Server, che garantiscono resilienza in caso di problemi della rete WAN. Ad esempio, in un sito in cui è distribuito un Survivable Branch Appliance o un Survivable Branch Server, gli utenti possono effettuare e ricevere chiamate di VoIP aziendale anche se la rete WAN che connette il sito di succursale al sito centrale è inattiva. Per informazioni dettagliate sul Survivable Branch Appliance, sul Survivable Branch Server e sulla resilienza, vedere [Pianificazione della resilienza di VoIP aziendale in Lync Server 2013](lync-server-2013-planning-for-enterprise-voice-resiliency.md) nella documentazione relativa alla pianificazione.

## Topologie di siti

La distribuzione deve includere almeno un sito centrale e può includere da zero a numerosi siti di succursale. Ogni sito di succursale è affiliato a un sito centrale. Il sito centrale fornisce i servizi di Lync Server che non sono disponibili in locale nel sito di succursale, ad esempio i servizi di presenza e conferenza.

Se sono disponibili più siti, sarà possibile accoppiare i pool Front End su siti diversi per abilitare le funzionalità di ripristino di emergenza. Per informazioni dettagliate, vedere [Supporto per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013](lync-server-2013-high-availability-and-disaster-recovery-support.md).

## Vedere anche

#### Concetti

[Ruoli del server in Lync Server 2013](lync-server-2013-server-roles.md)  
[Supporto per la disponibilità elevata e il ripristino di emergenza in Lync Server 2013](lync-server-2013-high-availability-and-disaster-recovery-support.md)  

#### Ulteriori risorse

[Pianificazione della resilienza di VoIP aziendale in Lync Server 2013](lync-server-2013-planning-for-enterprise-voice-resiliency.md)

