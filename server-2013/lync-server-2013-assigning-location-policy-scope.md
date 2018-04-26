---
title: "Lync Server 2013: Assegnazione dell'ambito dei criteri percorso"
TOCTitle: Assegnazione dell'ambito dei criteri percorso
ms:assetid: e4c66517-c593-4253-b900-7b4dd8bddf2f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205360(v=OCS.15)
ms:contentKeyID: 49302269
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Assegnazione dell'ambito dei criteri percorso in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-06-06_

Come per altri criteri di Lync Server, anche i criteri di percorso possono essere assegnati su più livelli di ambito, ovvero globale, sito e utente. L'ambito dei criteri di percorso a livello utente, tuttavia, presenta un comportamento leggermente diverso rispetto ad altri criteri di Lync Server. I criteri di percorso per utente non solo possono essere applicati a oggetti endpoint, come gli oggetti contatto per utenti o telefoni di area comune, ma posso essere applicati anche ai siti di rete di Lync Server. I siti di rete sono raggruppamenti delle subnet client associate a una posizione geografica, ma non necessariamente tutte le subnet di un intero sito centrale o sito di succursale. Qualsiasi client connesso alle subnet in un sito di rete recupera automaticamente i criteri di percorso assegnati al sito di rete. Nei casi in cui un criterio di percorso a livello utente viene assegnato sia a un utente che a un sito di rete, i criteri di percorso basati sul sito di rete sono prioritari rispetto a qualsiasi impostazione di criteri per utente.

A ogni sito di rete vengono assegnati criteri di percorso e ai singoli criteri vengono assegnati valori diversi per gli utilizzi PSTN, gli URI di notifica e gli URI conferenza.


> [!NOTE]
> Esiste un motivo per questo comportamento speciale relativo agli ambiti dei criteri. In questo modo, infatti, quando un utente ospitato in un pool in un sito dell'ufficio visita un altro sito e deve effettuare una chiamata di emergenza, vengono applicate le impostazioni di routing delle chiamate E9-1-1 appropriate per tale sito di rete, indipendentemente dal pool o dal sito a cui è assegnato l'utente.


