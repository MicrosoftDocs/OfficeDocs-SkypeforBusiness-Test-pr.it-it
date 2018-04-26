---
title: 'Lync Server 2013: Supporto per più trunk'
TOCTitle: Supporto per più trunk
ms:assetid: a1309c09-ad9a-4c54-9650-4e3f5b2a4a00
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205127(v=OCS.15)
ms:contentKeyID: 49301509
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Supporto per più trunk in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

La funzionalità di Lync Server 2013 supporta più associazioni tra gateway e Mediation Server. Queste associazioni vengono effettuate definendo un trunk, che è un'associazione logica tra un pool di Mediation Server e un gateway PSTN (Public Switched Telephone Network), un Session Border Controller (SBC) o un sistema IP-PBX. Utilizzare Generatore di topologie per associare gateway a Mediation Server, ovvero trunk.

  - Per assegnare o rimuovere un trunk in Lync Server 2013, è necessario innanzitutto definire un trunk in Generatore di topologie. Un trunk è costituito dall'associazione seguente: il nome di dominio completo (FQDN) del Mediation Server, la porta di attesa del Mediation Server, l'FQDN del gateway e la porta di attesa del gateway.

  - Per configurare più trunk, è possibile creare più associazioni tra lo stesso gateway e il Mediation Server. Ciò conferisce una maggiore resilienza all'infrastruttura di VoIP aziendale, aspetto particolarmente utile negli scenari interoperativi con centralini (PBX).

Dopo essere stato definito, il trunk deve essere associato a una route. A tale scopo, è possibile definire un nome semplice per il trunk in Generatore di topologie. Tale nome semplice viene utilizzato come nome del trunk nel Pannello di controllo di Lync Server, dove i trunk possono essere associate alle route. Il nome semplice del trunk viene utilizzato come nome del gateway da Lync Server Management Shell.

    New-CsVoiceRoute -Identity <RouteId> -NumberPattern <String> -PstnUsages @{add="<UsageString>"} -PstnGatewayList @{add="<TrunkSimpleName>"}

L'amministratore deve selezionare un trunk predefinito associato a un Mediation Server. In Generatore di topologie fare clic con il pulsante destro del mouse sul Mediation Server associato e quindi scegliere **Proprietà** . Specificare il gateway predefinito per il Mediation Server.

Nella figura seguente vengono illustrati i diversi trunk definiti per ogni Mediation Server e gateway.

**Routing con trunk M-N**

![Assegnazioni di più trunk.](images/JJ205127.c61cd9a7-d8d9-4e02-83b9-ab62519a48c4(OCS.15).jpg "Assegnazioni di più trunk.")

