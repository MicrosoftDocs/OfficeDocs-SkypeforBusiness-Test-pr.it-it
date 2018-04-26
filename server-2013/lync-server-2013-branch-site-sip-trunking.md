---
title: 'Lync Server 2013: Trunking SIP dei siti di succursale'
TOCTitle: Trunking SIP dei siti di succursale
ms:assetid: c4d9dfcd-8baa-41ea-9677-48b0e429429d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412974(v=OCS.15)
ms:contentKeyID: 49301895
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Trunking SIP dei siti di succursale in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-21_

In alcuni casi potrebbe essere necessario implementare in siti di succursale selezionati il trunking SIP distribuito. Per determinare se è necessario un trunk SIP per un sito di succursale, leggere le informazioni contenute in [Come implementare il trunking SIP in Lync Server 2013](lync-server-2013-how-do-i-implement-sip-trunking.md)

Per informazioni dettagliate sulle opzioni di tipologia supportate per la distribuzione di trunk SIP in siti di succursale, vedere [Soluzioni di resilienza dei siti di succursale in Lync Server 2013](lync-server-2013-branch-site-resiliency-solutions.md).

## Analisi dei requisiti di un trunk SIP per un sito di succursale di esempio

Se si decide di distribuire un trunk SIP per un sito di succursale, è necessario condurre un'analisi dei costi specifica per il sito. Un'organizzazione con un sito centrale a Milano e un sito di succursale a Roma ad esempio dovrebbe eseguire un'analisi per stabilire se implementare un trunk SIP dal sito di Roma a un provider di sevizi locale.

Per stabilire se l'implementazione nel sito di Roma di un trunk SIP distribuito è una soluzione conveniente, identificare i numeri DID (Direct Inward Dialing) che utilizzeranno il trunk SIP e quindi analizzare il numero di chiamate effettuate dal sito di Roma ad aree diverse da Milano. È possibile optare per la terminazione DID per il sito di succursale nel sito centrale. Il sito centrale di Milano ad esempio può ospitare numeri DID per il sito di succursale di Roma. Se il costo dell'implementazione di un trunk SIP distribuito è inferiore al costo di queste chiamate, prendere in considerazione l'implementazione di un trunk SIP nel sito di succursale di Roma.

## Altri requisiti per il trunk SIP di un sito di succursale

La scelta tra la distribuzione di un trunk SIP anziché di un gateway si basa sulla differenza tra i costi delle chiamate interurbane PSTN per ogni opzione. Se si distribuisce un trunk SIP per un sito di succursale, è inoltre necessario determinare i requisiti a livello di resilienza e larghezza di banda. Se il collegamento tra il sito di succursale e il sito centrale è resiliente e dispone di larghezza di banda sufficiente, è possibile distribuire un trunk SIP o un gateway. Non è necessario distribuire un Survivable Branch Appliance presso il sito di succursale. Se il collegamento tra il sito di succursale e il sito centrale non è resiliente, distribuire un Survivable Branch Appliance oppure un Survivable Branch Server con un gateway o un trunk SIP presso il sito di succursale.

