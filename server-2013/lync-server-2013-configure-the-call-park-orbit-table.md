---
title: 'Lync Server 2013: Configurare la tabella di codici orbit del parcheggio di chiamata'
TOCTitle: Configurare la tabella di codici orbit del parcheggio di chiamata
ms:assetid: e5cc0c19-7b2c-48e7-a21d-cfb23c842f0f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg399020(v=OCS.15)
ms:contentKeyID: 49302301
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare la tabella di codici orbit del parcheggio di chiamata in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-10_

Parcheggio di chiamata si basa sui codici orbit per parcheggiare le chiamate. Prima che gli utenti possano parcheggiare e recuperare le chiamate, è necessario configurare la tabella di codici orbit di Parcheggio di chiamata. È necessario specificare gli intervalli dei numeri di interno (codici orbit) che verranno riservati dall'organizzazione per parcheggiare le chiamate e definire il routing per gli intervalli specificando il pool di Parcheggio di chiamata che gestisce ogni intervallo. Quando si definiscono gli intervalli di codici orbit, l'obiettivo è quello di disporre di un numero sufficiente di codici orbit tale da evitare che uno stesso codice orbit venga riutilizzato troppo rapidamente, ma senza eccedere limitando il numero di interni disponibili per gli utenti o altri servizi. È possibile creare più intervalli di codici orbit di Parcheggio di chiamata per ogni pool di Lync Server in cui è distribuita l' applicazione Parcheggio di chiamata. A ogni intervallo di codici orbit di Parcheggio di chiamata deve essere associato un nome univoco globale e un set di estensioni univoco.

> [!IMPORTANT]  
> Un intervallo di codici orbit include in genere al massimo 100 codici orbit. Ogni intervallo può essere più grande, purché sia più piccolo del massimo di 10.000 codici orbit per intervallo e ogni pool includa meno di 50.000 codici orbit. Se un intervallo è troppo piccolo, i codici orbit vengono riutilizzati più rapidamente.

Utilizzare blocchi di estensioni virtuali, ovvero a cui non sono assegnati utenti o telefoni, per gli intervalli di codici orbit.


> [!NOTE]
> L'assegnazione di numeri DID (Direct Inward Dialing) come codici orbit nella tabella di codici orbit di Parcheggio di chiamata non è supportata.



## Argomenti della sezione

[Creare o modificare un intervallo di codici orbit del parcheggio di chiamata in Lync Server 2013](lync-server-2013-create-or-modify-a-call-park-orbit-range.md)

