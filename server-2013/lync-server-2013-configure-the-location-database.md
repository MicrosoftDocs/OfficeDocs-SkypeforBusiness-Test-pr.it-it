---
title: Configurare il database delle posizioni in Lync Server 2013
TOCTitle: Configurare il database delle posizioni in Lync Server 2013
ms:assetid: 8544be31-6958-47ef-b926-fdc80d56191c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398679(v=OCS.15)
ms:contentKeyID: 49301202
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare il database delle posizioni in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-17_

Per consentire ai client di individuare automaticamente la propria posizione in una rete, è necessario innanzitutto configurare il database delle posizioni. Se non si configura un database delle posizioni e l'opzione **Posizione necessaria** nei criteri percorso è impostata su **Sì** o su **Dichiarazione di non responsabilità**, verrà chiesto all'utente di immettere manualmente una posizione.

Per configurare un database delle posizioni, eseguire le operazioni seguenti:

1.  Popolare il database con il mapping degli elementi di rete ai percorsi. Se si utilizza un gateway ELIN (Emergency Location Identification Number), è necessario aggiungerlo al campo \<NomeSocietà\>.

2.  Convalidare gli indirizzi in base allo stradario generale gestito dal provider di servizi di emergenza.

3.  Pubblicare il database aggiornato.


> [!NOTE]
> In alternativa, è possibile definire un database di origine delle posizioni secondario che può essere utilizzato al posto del database delle posizioni. Per informazioni dettagliate, vedere <A href="lync-server-2013-configure-a-secondary-location-information-service.md">Configurare un servizio Informazioni percorso secondario</A>.



## Argomenti della sezione

  - [Popolare il database delle posizioni](lync-server-2013-populate-the-location-database.md)

  - [Convalidare gli indirizzi](lync-server-2013-validate-addresses.md)

  - [Pubblicare il database delle posizioni](lync-server-2013-publish-the-location-database.md)

