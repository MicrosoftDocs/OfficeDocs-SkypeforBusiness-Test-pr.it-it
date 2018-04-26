---
title: 'Lync Server 2013: Definizione di regole di normalizzazione'
TOCTitle: Definizione di regole di normalizzazione
ms:assetid: ed31d56c-00b5-4f72-bd9f-beb4100d441f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399071(v=OCS.15)
ms:contentKeyID: 49302371
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definizione di regole di normalizzazione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-04-22_

Le regole di normalizzazione di Lync Server 2013 utilizzano le espressioni regolari di .NET Framework per convertire i numeri di telefono composti nel formato E.164. In altri termini, le regole di normalizzazione convertono il numero di telefono composto da un utente nel formato usato internamente da Lync Server. A ogni dial plan devono essere assegnate una o più regole di normalizzazione.

Per informazioni dettagliate sulle regole di normalizzazione, vedere [Dial plan e regole di normalizzazione in Lync Server 2013](lync-server-2013-dial-plans-and-normalization-rules.md) nella documentazione relativa alla pianificazione.

Per informazioni dettagliate su come scrivere espressioni regolari, vedere "Espressioni regolari di .NET Framework" all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=140927](http://go.microsoft.com/fwlink/p/?linkid=140927).

È possibile utilizzare uno dei metodi seguenti per definire o modificare una regola di normalizzazione:

  - Utilizzare lo strumento **Crea regola di normalizzazione** per specificare i valori per le cifre iniziali, la lunghezza, le cifre da rimuovere e quelle da aggiungere, quindi lasciare che il formato e la regola di conversione corrispondenti vengano generati automaticamente dal Pannello di controllo di Lync Server.

  - Scrivere manualmente espressioni regolari per definire il formato corrispondente e la regola di conversione.

## Argomenti della sezione

  - [Creare o modificare una regola di normalizzazione utilizzando Crea regola di normalizzazione in Lync Server 2013](lync-server-2013-create-or-modify-a-normalization-rule-by-using-build-a-normalization-rule.md)

  - [Creare o modificare manualmente una regola di normalizzazione in Lync Server 2013](lync-server-2013-create-or-modify-a-normalization-rule-manually.md)

## Vedere anche

#### Attività

[Creare un dial plan in Lync Server 2013](lync-server-2013-create-a-dial-plan.md)  
[Modificare un dial plan in Lync Server 2013](lync-server-2013-modify-a-dial-plan.md)

