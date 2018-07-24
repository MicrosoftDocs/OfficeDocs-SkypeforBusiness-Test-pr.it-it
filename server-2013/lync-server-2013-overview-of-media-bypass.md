---
title: 'Lync Server 2013: Panoramica del bypass multimediale'
TOCTitle: Panoramica del bypass multimediale
ms:assetid: 9ea090b3-f607-46f7-97dd-2510052524e5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412740(v=OCS.15)
ms:contentKeyID: 49301480
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Panoramica del bypass multimediale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

La funzionalità bypass multimediale è utile se si desidera ridurre il numero dei Mediation Server distribuiti. Un pool Mediation Server viene in genere distribuito in un sito centrale e controlla i gateway nei siti di succursale. Abilitando il bypass multimediale, gli elementi multimediali per chiamate PSTN da client dei siti di succursale possono attraversare direttamente i gateway di tali siti. Le route delle chiamate in uscita e i criteri VoIP aziendale di Lync Server 2013 devono essere configurati correttamente in modo che le chiamate PSTN dai client nel sito di succursale vengano instradate verso il gateway appropriato.

Nelle reti Wi-Fi in genere si verificano più perdite di pacchetti rispetto alle reti cablate. Il recupero da queste perdite di pacchetti non può solitamente essere supportato dai gateway. Pertanto, è consigliabile valutare la qualità di una rete Wi-Fi prima di stabilire se abilitare il bypass per una subnet wireless. È inoltre necessario valutare il compromesso tra la riduzione della latenza e la perdita di pacchetti. RTAudio, un codec non disponibile per le chiamate che non aggirano il Mediation Server, è più indicato per la gestione della perdita di pacchetti.

Dopo l'implementazione della struttura di VoIP aziendale, la pianificazione del bypass multimediale è semplice.

  - Se si dispone di una topologia centralizzata senza collegamenti WAN ai siti di succursale, è possibile abilitare un bypass multimediale globale, perché non è necessario un controllo capillare.

  - Se si dispone di una topologia distribuita costituita da una o più aree di rete e relativi siti di succursale affiliati, verificare quanto segue:
    
      - Se i peer di Mediation Server sono in grado di supportare le funzionalità necessarie per il bypass multimediale.
    
      - Quali siti in ogni area di rete sono ben connessi.
    
      - Quale combinazione di bypass multimediale e controllo di ammissione di chiamata è appropriato per la rete.

Quando si abilita il bypass multimediale, viene generato automaticamente un ID bypass univoco per un'area della rete e per tutti i siti della rete senza vincoli di larghezza di banda nell'ambito di tale area. Ai siti con vincoli di larghezza di banda nell'ambito dell'area e ai siti connessi a tale area tramite collegamenti WAN con vincoli di larghezza di banda vengono assegnati ID di bypass univoci specifici.

Quando un utente effettua una chiamata alla rete PSTN, il Mediation Server confronta l'ID bypass della subnet del client con l'ID bypass della subnet del gateway. Se i due ID combaciano, per la chiamata viene utilizzato il bypass multimediale. In caso contrario, i contenuti multimediali della chiamata devono passare attraverso il Mediation Server.

Quando un utente riceve una chiamata dalla rete PSTN, il client dell'utente confronta il proprio ID bypass a quello del gateway PSTN. Se i due ID coincidono, i contenuti multimediali vengono trasmessi direttamente dal gateway al client, ignorando il Mediation Server.

Solo client e dispositivi Lync 2010 o superiori supportano interazioni di bypass multimediale con un Mediation Server.

> [!important]  
> Oltre che a livello globale, il bypass multimediale deve essere abilitato singolarmente in ogni trunk PSTN. Se il bypass viene abilitato globalmente ma non per un determinato trunk PSTN, non verrà richiamato per le chiamate che coinvolgono questo trunk PSTN. Inoltre, se il bypass multimediale è impostato per l'utilizzo delle informazioni del sito e dell'area geografica, è necessario associare tutte le subnet instradabili ai siti in cui si trovano. Se in un sito sono presenti subnet instradabili per cui non si desidera il bypass, sarà necessario raggruppare queste subnet in un nuovo sito prima di abilitare il bypass multimediale. In questo modo, le subnet non instradabili verranno assegnate a un ID bypass diverso.

## Vedere anche

#### Concetti

[Modalità di bypass multimediale in Lync Server 2013](lync-server-2013-media-bypass-modes.md)  
[Bypass multimediale e controllo di ammissione di chiamata in Lync Server 2013](lync-server-2013-media-bypass-and-call-admission-control.md)  
[Requisiti tecnici per il bypass multimediale in Lync Server 2013](lync-server-2013-technical-requirements-for-media-bypass.md)

