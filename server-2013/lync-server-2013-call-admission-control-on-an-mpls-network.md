---
title: 'Lync Server 2013: Controllo di ammissione di chiamata in una rete MPLS'
TOCTitle: Controllo di ammissione di chiamata in una rete MPLS
ms:assetid: 0beec6be-2431-4255-a3d2-512dd030e66a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398168(v=OCS.15)
ms:contentKeyID: 49299665
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Controllo di ammissione di chiamata in una rete MPLS con Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-22_

In una rete MPLS (Multiprotocol Label Switching) tutti i siti sono connessi tramite full mesh, ovvero tutti i siti sono connessi direttamente alla dorsale MPLS del provider di servizi Internet e a ogni sito viene assegnata una larghezza di banda da utilizzare nel cloud MPLS attraverso un collegamento WAN. Non è presente alcun hub di rete o sito centrale per controllare il routing IP. Nella figura seguente viene illustrata una rete semplice basata sulla tecnologia MPLS.

**Rete MPLS di esempio**

![Controllo di ammissione di chiamata con MPLS](images/Gg398168.54602e6e-ec11-4dae-936d-b01acda8a179(OCS.15).jpg "Controllo di ammissione di chiamata con MPLS")

Per distribuire il controllo di ammissione di chiamata in una rete MPLS, è necessario creare un'area di rete che rappresenti il cloud MPLS e un sito di rete che rappresenti ogni sito satellite MPLS. Nella figura seguente viene illustrato come è consigliabile configurare l'area di rete e i siti di rete per rappresentare la rete MPLS di esempio della figura precedente. I limiti di larghezza di banda totali e quelli di sessione sono quindi basati sulla capacità del collegamento WAN che va da ogni sito di rete all'area di rete che rappresenta il cloud MPLS.

**Area di rete e siti di rete per una rete MPLS**

![Diagramma del controllo di ammissione di chiamata con MPLS](images/Gg398168.f8f76283-5c0c-4133-8a78-3fbbfd016dc4(OCS.15).jpg "Diagramma del controllo di ammissione di chiamata con MPLS")

