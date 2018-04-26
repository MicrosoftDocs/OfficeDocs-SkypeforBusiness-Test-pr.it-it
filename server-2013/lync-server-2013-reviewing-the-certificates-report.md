---
title: Esame del rapporto sui certificati in Lync Server 2013
TOCTitle: Esame del rapporto sui certificati in Lync Server 2013
ms:assetid: 549cfc9b-3cc5-4483-a93c-fc0738c7f622
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg558651(v=OCS.15)
ms:contentKeyID: 52062155
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Esame del rapporto sui certificati in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

Il Rapporto certificati include tutti i certificati necessari nella distribuzione di Lync Server 2013 consigliata. Lo Strumento di pianificazione tiene conto dei nomi soggetto e dei nomi alternativi soggetto immessi. Il testo predefinito lasciato invariato potrebbe rappresentare una sfida per il team responsabile della richiesta e del rilascio dei certificati. Nelle informazioni sui certificati sono inoltre incluse informazioni sull'origine da cui in genere viene emesso il certificato. Se l'infrastruttura non dispone di un'infrastruttura a chiave pubblica (PKI) interna, tutti i certificati possono essere richiesti tramite un provider di certificati pubblico. I campi EKU e Assegna a nel rapporto sono molto utili per comprendere lo scopo e il percorso di ogni certificato.

![Rapporto di amministrazione certificati](images/Gg558651.63a29335-d9e4-41ae-97ec-3c9d9fd30d8a(OCS.15).jpg "Rapporto di amministrazione certificati")

Esaminare accuratamente e comprendere pienamente gli scopi e gli utilizzi di ogni certificato nella distribuzione. In caso di dubbi sulle funzioni di un certificato, stabilire quale server o servizio interagisce con quale altra entità. I certificati in Lync Server 2013 vengono utilizzati per due scopi primari:

  - MTLS (Mutual Transport Layer Security): i computer coinvolti nella comunicazione presentano ognuno un certificato per provare la rispettiva identità, processo noto come autenticazione del server. La comunicazione non può avere inizio fino a quando ogni computer non considera attendibile l'identità degli altri computer coinvolti.

  - Crittografia: la crittografia (Secure Sockets Layer, o SSL e Transport Layer Security, o TLS) è uno strumento fondamentale per la protezione delle comunicazioni, per assicurare la privacy e per creare un sistema di comunicazioni e collaborazione attendibile.

## Vedere anche

#### Ulteriori risorse

[Esame dei rapporti amministratore in Lync Server 2013](lync-server-2013-reviewing-the-administrator-reports.md)

