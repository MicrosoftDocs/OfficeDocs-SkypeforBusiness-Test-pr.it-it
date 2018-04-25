---
title: Opzioni globali di bypass multimediale in Lync Server 2013
TOCTitle: Opzioni globali di bypass multimediale in Lync Server 2013
ms:assetid: 1bd35f90-8587-48a1-b0c2-095a4053fc77
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398255(v=OCS.15)
ms:contentKeyID: 49299849
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Opzioni globali di bypass multimediale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-04_


> [!NOTE]
> In questo argomento si presuppone che il bypass multimediale sia già stato configurato per qualsiasi trunk di connessione a un peer, ovvero un gateway PSTN (Public Switched Telephone Network), un IP-PBX o un Session Border Controller (SBC) presso un provider di servizi di telefonia Internet ITSP, per un sito o un servizio specifico per il quale si desidera ignorare il Mediation Server.



Oltre ad abilitare il bypass multimediale per le singole connessioni trunk associate a un peer, è necessario abilitarlo globalmente. Nelle impostazioni di bypass multimediale globali è possibile specificare di tentare sempre il bypass multimediale per le chiamate alla rete PSTN o di utilizzarlo in base al mapping tra le subnet e i siti e le aree di rete, in modo analogo a quanto viene effettuato dal controllo di ammissione di chiamata, un'altra funzionalità vocale avanzata. Se il bypass multimediale e il controllo di ammissione di chiamata sono entrambi abilitati, per determinare se applicare il bypass multimediale vengono automaticamente utilizzate le informazioni delle aree di rete, dei siti di rete e delle subnet specificate per il controllo di ammissione di chiamata. Se pertanto il controllo di ammissione di chiamata è abilitato, non è possibile specificare di tentare sempre il bypass multimediale per le chiamate alla rete PSTN.

In questo argomento viene illustrato come utilizzare il Pannello di controllo di Lync Server e Lync Server Management Shell insieme per configurare le impostazioni di bypass multimediale globali.


> [!NOTE]
> Quando si utilizzano queste procedure per configurare il bypass multimediale, si presuppone che si disponga di una buona connettività tra i client e il peer Mediation Server, ad esempio un gateway PSTN, un sistema IP-PBX o un SBC (Session Border Controller) in un provider di trunking SIP. Se sono previsti limiti di larghezza di banda sul collegamento, non è possibile applicare il bypass multimediale alla chiamata. Il bypass multimediale non funziona con tutti i gateway PSTN, i sistemi IP-PBX e i Session Border Controller. Microsoft ha testato una serie di gateway PSTN e SBC con partner certificati e ha eseguito alcuni test con i sistemi IP-PBX Cisco. Il bypass multimediale è supportato solo con i prodotti e le versioni elencati nella pagina Web Unified Communications Open Interoperability Program - Lync Server all'indirizzo <A class=uri href="http://go.microsoft.com/fwlink/?linkid=214406%26clcid=0x410">http://go.microsoft.com/fwlink/?linkid=214406&amp;clcid=0x410</A>.



## Passaggi successivi: scegliere le impostazioni di bypass multimediale globali

Dopo aver abilitato il bypass multimediale sulle connessioni trunk a un peer per siti o servizi specifici, utilizzare il contenuto indicato di seguito per eseguire una delle operazioni seguenti:

  - Abilitare sempre il bypass multimediale come descritto in [Configurare la funzionalità bypass multimediale in modo che Mediation Server venga sempre ignorato](lync-server-2013-configure-media-bypass-to-always-bypass-the-mediation-server.md).

  - In alternativa, configurare il bypass multimediale per l'utilizzo delle informazioni sui siti e sulle aree come descritto in [Configurare le impostazioni globali di bypass multimediale per l'utilizzo delle informazioni del sito e dell'area geografica](lync-server-2013-configure-media-bypass-global-settings-to-use-site-and-region-information.md).

## Vedere anche

#### Attività

[Configurare un trunk con bypass multimediale in Lync Server 2013](lync-server-2013-configure-a-trunk-with-media-bypass.md)  
[Associare una subnet a un sito di rete in Lync Server 2013](lync-server-2013-associate-a-subnet-with-a-network-site.md)  

#### Concetti

[Configurare il bypass multimediale in Lync Server 2013](lync-server-2013-configure-media-bypass.md)  
[Bypass multimediale e Mediation Server in Lync Server 2013](lync-server-2013-media-bypass-and-mediation-server.md)

