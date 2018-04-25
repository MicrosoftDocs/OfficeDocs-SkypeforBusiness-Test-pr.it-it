---
title: 'Lync Server 2013: Installazione di software facoltativo'
TOCTitle: Installazione di software facoltativo
ms:assetid: b95b3301-fa1e-4b96-9af4-05b43d39db8d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615032(v=OCS.15)
ms:contentKeyID: 52062297
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Installazione di software facoltativo in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

Microsoft Lync Server 2013, Strumento di pianificazione è stato progettato per l'esportazione in Microsoft Excel e Microsoft Visio. Benché queste applicazioni non siano obbligatorie per il funzionamento di Strumento di pianificazione, aggiungono valore alla distribuzione e documentazione della progettazione.

## Software facoltativo

## Microsoft Excel

L'esportazione del progetto in Microsoft Excel consente di creare un rapporto con sette schede nel foglio di calcolo:

  - Riepilogo: visualizza informazioni sulla configurazione del sito, tra cui numero di utenti, impostazioni di capacità, e informazioni sul profilo del server.

  - Profilo hardware: visualizza un rapporto delle configurazioni hardware consigliate per i server specificati nella topologia, inclusi disco, CPU, memoria, e interfaccia di rete. Sono inoltre incluse la quantità e le specifiche consigliate per i componenti del server. Ogni server è inoltre definito in base al sito, per fornire una rappresentazione completa dei requisiti del server per ogni sito.

  - Requisiti porte: visualizza un rapporto di tutte le porte abilitate e l'associazione al bilanciamento del carico DNS (DNS LB) e ai dispositivi di bilanciamento del carico hardware (HLB). È consigliabile utilizzare questo rapporto per pianificare le configurazioni di firewall, bilanciamento del carico DNS e bilanciamento del carico hardware.

  - Rapporto riepilogativo: visualizza il riepilogo generale delle impostazioni obbligatorie per configurare la rete del server perimetrale.

  - Rapporto certificati: visualizza il nome soggetto e i nomi soggetto alternativi obbligatori per i certificati necessari per l'esecuzione dei server perimetrali.

  - Rapporto firewall: visualizza le porte di origine e di destinazione e gli indirizzi IP per le interfacce sia esterne che interne.

  - Rapporto DNS: visualizza il nome di dominio completo (FQDN) e gli indirizzi IP/VIP obbligatori per ogni voce DNS creata.

## Microsoft Visio

L'esportazione del progetto in Microsoft Visio consente di creare un diagramma da usare per la documentazione della topologia e dell'infrastruttura configurate. Il diagramma importato può essere modificato e riorganizzato in base alle specifiche esigenze per la documentazione. Il diagramma di Visio tipico includerà:


> [!NOTE]
> Se le dimensioni della progettazione sono tali da richiedere più di tre Front End Server, verrà creata una pagina aggiuntiva per il pool Front End, i Front End Server, il computer che esegue SQL Server, gli indirizzi IP e i nomi FQDN.



  - Topologia globale: diagramma dei siti Lync Server 2013 configurati.

  - Scheda Nome sito: visualizza la topologia di configurazione del sito con server perimetrale, firewall, PSTN con gateway e la distribuzione dei server interna. La distribuzione interna è costituita dai server e pool configurati, inclusi pool Front End, server basati su SQL Server, Servizi di dominio Active Directory, Director, server di messaggistica unificata Exchange, server delle cassette postali di Exchange, server Office Web Apps, Mediation Server e server Chat persistente.

  - Diagramma rete perimetrale: diagramma che rappresenta in dettaglio la configurazione del server perimetrale con gli indirizzi IP e i nomi FQDN associati. Sono inoltre inclusi il bilanciamento del carico DNS e i dispositivi di bilanciamento del carico hardware. Sono visualizzati anche i Director e il Front End Server o il pool Front End con il bilanciamento del carico DNS o hardware associato e l'indirizzo IP (lo Strumento di pianificazione supporta sia gli indirizzi IPv4 che IPv6) e gli FQDN assegnati.

## Vedere anche

#### Attività

[Installazione dello strumento di pianificazione in Lync Server 2013](lync-server-2013-installing-the-planning-tool.md)

