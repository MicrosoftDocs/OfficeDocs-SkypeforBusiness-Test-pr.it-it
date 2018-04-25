---
title: "Lync Server 2013: Posizione dell'utente"
TOCTitle: Posizione dell'utente
ms:assetid: ce57941d-086b-448e-8ada-c7d636a2a1c9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994073(v=OCS.15)
ms:contentKeyID: 52062276
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Posizione dell'utente in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-03-09_

Il routing in base alla posizione sfrutta le stesse aree di rete, i siti e le subnet definiti in Lync Server e usati dal servizio Enhanced 9-1-1, da CAC e dal bypass multimediale per applicare limitazioni al routing delle chiamate ed evitare il bypass delle chiamate a tariffa PSTN. La posizione di un utente è determinata dalla subnet IP dell'endpoint Lync da cui l'utente è connesso. Ogni subnet IP è associata a un sito di rete, che è aggregato in un'area di rete definita dall'amministratore. Il routing in base alla posizione viene applicato in base al sito di rete dell'utente.

Le regole del routing in base alla posizione vengono applicate in base al sito di rete, vale a dire che un dato set di regole verrà applicato a tutti gli endpoint abilitati per il routing in base alla posizione che si trovano nello stesso sito di rete. Gli amministratori possono applicare il routing in base alla posizione ai siti di rete che lo richiedono.

È possibile definire i criteri di routing vocale in base al sito di rete per definire uno specifico gateway PSTN che deve essere utilizzato da tutti gli utenti che si trovano in tale sito per chiamare numeri di telefono PSTN. Tali criteri di routing vocale avranno la precedenza rispetto al routing definito dai criteri vocali dell'utente quando quest'ultimo si trova in un sito di rete abilitato per il routing in base alla posizione, ed eviteranno che le chiamate vengano instradate attraverso altri gateway PSTN abilitati per il routing in base alla posizione. Quando un utente Lync effettua una chiamata PSTN, i criteri vocali associati all'utente determinano se è autorizzato a effettuare la chiamata. In caso affermativo, il routing in base alla posizione determina il gateway PSTN di uscita della chiamata in base alla posizione dell'utente.

La posizione dell'utente può essere classificata come segue:

  - L'utente si trova in un sito di rete conosciuto abilitato per il routing in base alla posizione e il suo numero DID (Direct Inward Dialing) termina in un gateway PSTN situato nello sito di rete, ad esempio in ufficio. Il routing delle chiamate in uscita verrà eseguito in base ai criteri di routing vocale del sito di rete in cui l'utente si trova. Le chiamate PSTN in arrivo al'utente verranno instradate agli endpoint situati nello stesso sito di rete del gateway PSTN.

  - L'utente si trova in un sito di rete conosciuto diverso dal sito di rete in cui è situato il gateway PSTN, ad esempio l'utente si è spostato in un'altra sede aziendale. Il routing delle chiamate in uscita verrà eseguito in base ai criteri di routing vocale del sito di rete in cui l'utente si trova. Le chiamate PSTN in arrivo all'utente non verranno instradate agli endpoint situati in siti diversi rispetto al gateway PSTN per evitare il bypass delle chiamate a tariffa PSTN.

  - Quando un utente si trova in un sito di rete sconosciuto alla distribuzione di Lync Server, il routing delle chiamate in uscita verrà eseguito in base ai criteri vocali assegnati all'utente per i gateway PSTN non associati alle limitazioni del routing in base alla posizione. Le chiamate PSTN in arrivo non verranno instradate a endpoint situati in siti di rete sconosciuti per evitare il bypass delle chiamate a tariffa PSTN.

## Vedere anche

#### Ulteriori risorse

[Linee guida per il routing in base alla posizione in Lync Server 2013](lync-server-2013-guidance-for-location-based-routing.md)

