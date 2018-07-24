---
title: 'Lync Server 2013: Supporto di dispositivi hardware'
TOCTitle: Supporto di dispositivi hardware
ms:assetid: ba07ca91-32b4-49cf-801c-47a2d1d96e18
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412908(v=OCS.15)
ms:contentKeyID: 49301777
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Supporto di dispositivi hardware in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-12-14_

Prima di distribuire telefoni IP e dispositivi analogici, è necessario implementare configurazioni hardware specifiche.

I telefoni IP che eseguono Lync Phone Edition supportano LLDP-MED (Link Layer Discovery Protocol-Media Endpoint Discovery) e PoE (Power over Ethernet). Per poter utilizzare LLDP-MED, il commutatore deve supportare IEEE802.1AB e ANSI/TIA-1057. Per poter utilizzare PoE, il commutatore deve supportare PoE802.3AF o 802.3at.

Per abilitare LLDP-MED, l'amministratore deve abilitare LLDP tramite la finestra della console del commutatore e impostare i criteri di rete LLDP-MED con l'ID VLAN voce corretto.

Se inoltre la distribuzione include dispositivi analogici, è necessario configurare il gateway analogico per l'utilizzo di Lync Server e il gateway deve essere uno degli elementi seguenti:

  - Un adattatore telefonico analogico (ATA, Analog Telephone Adapter)

  - Un gateway analogico PSTN

  - Un Survivable Branch Appliance che include un gateway analogico PSTN

  - Un Survivable Branch Appliance che include un gateway PSTN che comunica con un adattatore telefonico analogico

Per informazioni su come configurare un gateway analogico, vedere "Pianificazione per la distribuzione di dispositivi analogici" all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=268537](http://go.microsoft.com/fwlink/p/?linkid=268537) nella libreria TechNet di Lync Server 2010. I dispositivi analogici in Lync Server 2013 funzionano come in Lync Server 2010.

> [!important]  
> È possibile configurare il commutatore per Enhanced 9-1-1 (E9-1-1), se supportato dal commutatore.
