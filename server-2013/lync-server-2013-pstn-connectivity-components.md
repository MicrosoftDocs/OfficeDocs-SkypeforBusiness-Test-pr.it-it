---
title: 'Lync Server 2013: Componenti di connettività PSTN'
TOCTitle: Componenti di connettività PSTN
ms:assetid: 6b2a3f7d-760f-4f09-8432-312c98a7e6b7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398504(v=OCS.15)
ms:contentKeyID: 49300878
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Componenti di connettività PSTN in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-04_

Una soluzione VoIP di livello aziendale deve essere in grado di garantire le chiamate da e verso la rete PSTN (Public Switched Telephone Network) senza alcun decadimento della qualità del servizio (QoS). Gli utenti non devono inoltre preoccuparsi della tecnologia sottostante quando effettuano e ricevono chiamate. Dal punto di vista dell'utente, una chiamata tra l'infrastruttura VoIP aziendale e la rete PSTN deve risultare del tutto analoga a qualsiasi altra sessione SIP.

Per le connessioni PSTN, è possibile distribuire un trunk SIP o un gateway PSTN (con un PBX, denominato anche collegamento Direct SIP, o senza un PBX).

## Trunking SIP

Come alternativa all'utilizzo di gateway PSTN, è possibile connettere la soluzione VoIP aziendale alla rete PSTN tramite trunking SIP. Il trunking SIP consente gli scenari seguenti:

  - Un utente aziendale interno o esterno al firewall aziendale può effettuare una chiamata locale o interurbana tramite un numero compatibile con E.164, che viene terminata nella rete PSTN come servizio del provider di servizi corrispondente.

  - Qualsiasi sottoscrittore PSTN può contattare un utente aziendale interno o esterno al firewall aziendale componendo un numero DID (Direct Inward Dialing) associato a tale utente.

Per l'utilizzo di questa soluzione di distribuzione è necessario un provider di servizi di trunking SIP.

## Gateway PSTN

I gateway PSTN sono dispositivi di terze parti che convertono i segnali e i contenuti multimediali tra l'infrastruttura VoIP aziendale e una rete PSTN o un PBX. I gateway PSTN operano con Mediation Server per presentare una chiamata PSTN o PBX a un client VoIP aziendale. Mediation Server presenta inoltre le chiamate da client VoIP aziendale al gateway PSTN per il routing alla rete PSTN o al PBX. Per un elenco di partner che collaborano con Microsoft per offrire dispositivi in grado di funzionare con Lync Server, vedere il sito Web Microsoft Unified Communications Partners all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=202836](http://go.microsoft.com/fwlink/p/?linkid=202836).

## Centralini

Se è disponibile un'infrastruttura vocale esistente che utilizza un centralino (PBX, Private Branch Exchange), è possibile utilizzare il PBX con VoIP aziendale di Lync Server.

Gli scenari di integrazione tra VoIP aziendale e PBX supportati sono i seguenti:

  - IP-PBX che supporta il bypass multimediale, con un server Mediation Server.

  - IP-PBX che richiede un gateway PSTN autonomo.

  - PBX TDM (Time Division Multiplexing), con un gateway PSTN autonomo.


> [!NOTE]
> La funzionalità di bypass multimediale non funziona con tutti i gateway PSTN, i sistemi IP-PBX e i servizi SBC. Microsoft ha testato una serie di gateway PSTN e i servizi SBC con partner certificati e ha eseguito alcuni test con i sistemi IP-PBX di Cisco. Il bypass multimediale è supportato solo con le versioni e i prodotti elencati nel sito Web relativo al programma Unified Communications Open Interoperability Program - Lync Server all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=214406">http://go.microsoft.com/fwlink/p/?linkId=214406</A>.



Per informazioni dettagliate sui partner che offrono soluzioni VoIP aziendale, vedere il sito Web Microsoft Unified Communications Partners all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=202836](http://go.microsoft.com/fwlink/p/?linkid=202836).

Per informazioni dettagliate sui partner che offrono soluzioni hardware VoIP aziendale, inclusi gateway PSTN, vedere il sito Web Microsoft Unified Communications Partners all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=202836](http://go.microsoft.com/fwlink/p/?linkid=202836).

