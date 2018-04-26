---
title: 'Lync Server 2013: Servizi di emergenza avanzati e Mediation Server'
TOCTitle: Servizi di emergenza avanzati e Mediation Server
ms:assetid: d231221f-5596-4a87-a463-269f5bcce65f
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398903(v=OCS.15)
ms:contentKeyID: 49302050
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Servizi di emergenza avanzati e Mediation Server in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-29_

Il Mediation Server dispone di funzionalità estese che consentono di interagire correttamente con i provider di servizi chiamate di emergenza (Enhanced 9-1-1). Non è necessaria alcuna configurazione speciale nel Mediation Server. Le estensioni SIP necessarie per l'interazione con il servizio chiamate di emergenza (E9-1-1) sono incluse per impostazione predefinita nel protocollo SIP del Mediation Server per le interazioni con un peer gateway (gateway PSTN, IP-PBX oppure SBC di un provider di servizi di telefonia Internet, inclusi i provider di servizi E9-1-1).

L'eventualità che il trunk SIP per un provider di servizi chiamate di emergenza (E9-1-1) termini su un pool Mediation Server esistente o richieda Mediation Server autonomi dipende dalla possibilità o meno che il servizio SBC E9-1-1 interagisca con un pool di Mediation Server. Per informazioni dettagliate, vedere [Trunk con relazioni molti-a-molti in Lync Server 2013](lync-server-2013-m-n-trunk.md).

