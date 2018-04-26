---
title: 'Lync Server 2013: Configurare il bypass multimediale'
TOCTitle: Configurare il bypass multimediale
ms:assetid: f50a7a13-c6a0-48f1-bee1-e45fa2b2f9b8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg413028(v=OCS.15)
ms:contentKeyID: 49302470
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare il bypass multimediale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-24_

In questa sezione si presuppone che sia stata già pubblicata e configurata almeno un'istanza di Mediation Server oppure più di una (come descritto in [Definire un Mediation Server in Generatore di topologie in Lync Server 2013](lync-server-2013-define-a-mediation-server-in-topology-builder.md) e [Pubblicare la topologia in Lync Server 2013](lync-server-2013-publish-the-topology.md) oppure in [Definire e configurare un pool Front End o un server Standard Edition in Lync Server 2013](lync-server-2013-define-and-configure-a-front-end-pool-or-standard-edition-server.md) e [Pubblicare la topologia in Lync Server 2013](lync-server-2013-publish-the-topology.md), rispettivamente, tutti nella documentazione relativa alla distribuzione).

In questa sezione si presuppone inoltre che sia stato definito almeno un peer gateway per fornire connettività PSTN, come descritto in [Definire un gateway in Generatore di topologie in Lync Server 2013](lync-server-2013-define-a-gateway-in-topology-builder.md). Se il peer a cui ci si connette è l'SBC di un provider di servizi di trunking SIP, assicurarsi che il provider sia qualificato e che supporti il bypass multimediale. Ad esempio, molti provider di servizi di trunking SIP consentono solo al relativo SBC di ricevere traffico da Mediation Server. In questo caso, il bypass non deve essere abilitato per il trunk in questione. Inoltre, non è possibile abilitare il bypass multimediale a meno che la propria organizzazione non riveli i propri indirizzi IP di rete interni al provider di servizi di trunking SIP.


> [!NOTE]
> La funzionalità di bypass multimediale non funziona con tutti i gateway PSTN, i sistemi IP-PBX e i servizi SBC. Microsoft ha testato una serie di gateway PSTN e i servizi SBC con partner certificati e ha eseguito alcuni test con i sistemi IP-PBX di Cisco. Il bypass multimediale è supportato solo con le versioni e i prodotti elencati nel sito Web relativo al programma Unified Communications Open Interoperability Program - Lync Server all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=214406">http://go.microsoft.com/fwlink/p/?linkId=214406</A>.



In questa sezione viene descritto come abilitare il bypass multimediale per ridurre l'elaborazione richiesta di Mediation Server. Prima di abilitare il bypass multimediale, assicurarsi che l'ambiente soddisfi le condizioni richieste per supportarlo, come descritto in [Pianificazione del bypass multimediale in Lync Server 2013](lync-server-2013-planning-for-media-bypass.md) nella documentazione relativa alla pianificazione. Assicurarsi inoltre di utilizzare le informazioni in [Pianificazione del bypass multimediale in Lync Server 2013](lync-server-2013-planning-for-media-bypass.md) per decidere se abilitare le impostazioni globali del bypass multimediale per ignorare sempre Mediation Server oppure utilizzare le informazioni sul sito e sul paese per determinare se ignorare Mediation Server.

Se si è già configurato facoltativamente il controllo di ammissione di chiamata (CAC), un'altra funzionalità avanzata di VoIP aziendale, notare che la larghezza di banda riservata dal controllo di ammissione di chiamata non si applica ad alcuna chiamata per cui viene impiegato il bypass multimediale. Viene innanzitutto verificato se impiegare il bypass multimediale e, in caso venga impiegato, il controllo di ammissione di chiamata non viene utilizzato per la chiamata. Solo se la verifica del bypass multimediale dà esito negativo, viene eseguita la verifica per il controllo di ammissione di chiamata. Le due funzionalità si escludono a vicenda per qualsiasi chiamata specifica instradata al PSTN. Questa logica è dovuta al fatto che il bypass multimediale presuppone l'assenza di vincoli di larghezza di banda tra gli endpoint multimediali in una chiamata. Non è possibile eseguire il bypass multimediale su collegamenti con larghezza di banda limitata. Di conseguenza, alle chiamate PSTN è applicabile una delle seguenti alternative: a) viene applicato il bypass multimediale di Mediation Server e il controllo di ammissione di chiamata non riserva larghezza di banda per la chiamata oppure b) il controllo di ammissione di chiamata riserva la larghezza di banda per la chiamata e il supporto multimediale viene elaborato dall'istanza di Mediation Server interessata dalla chiamata.

## Passaggi successivi: abilitare il bypass multimediale sulla connessione trunk

Dopo aver configurato le impostazioni iniziali per la connettività PSTN (dial plan, criteri vocali, record utilizzo PSTN, route chiamate in uscita e regole di conversione), iniziare il processo di abilitazione del bypass multimediale seguendo la procedura riportata in [Configurare un trunk con bypass multimediale in Lync Server 2013](lync-server-2013-configure-a-trunk-with-media-bypass.md).

## Vedere anche

#### Attività

[Configurare un trunk con bypass multimediale in Lync Server 2013](lync-server-2013-configure-a-trunk-with-media-bypass.md)  
[Configurare la funzionalità bypass multimediale in modo che Mediation Server venga sempre ignorato](lync-server-2013-configure-media-bypass-to-always-bypass-the-mediation-server.md)  
[Configurare le impostazioni globali di bypass multimediale per l'utilizzo delle informazioni del sito e dell'area geografica](lync-server-2013-configure-media-bypass-global-settings-to-use-site-and-region-information.md)  

#### Concetti

[Opzioni globali di bypass multimediale in Lync Server 2013](lync-server-2013-global-media-bypass-options.md)  

#### Ulteriori risorse

[Pianificazione del bypass multimediale in Lync Server 2013](lync-server-2013-planning-for-media-bypass.md)

