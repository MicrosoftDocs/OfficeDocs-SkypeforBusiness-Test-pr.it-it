---
title: Impostazione dei criteri di gruppo per Lync 2013
TOCTitle: Impostazione dei criteri di gruppo per Lync 2013
ms:assetid: 5917a52b-dae0-4ec0-8548-a68dc20ab71c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204924(v=OCS.15)
ms:contentKeyID: 49300626
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Impostazione dei criteri di gruppo per Lync 2013

 

_**Ultima modifica dell'argomento:** 2012-10-03_

Nelle versioni precedenti di Lync e Office Communicator era disponibile il modello amministrativo autonomo Communicator.adm per la configurazione delle impostazioni client di Criteri di gruppo. Lync 2013 include nuovi modelli amministrativi (file con estensione admx e adml) insieme al modello amministrativo di Criteri di gruppo di Office. La disponibilità dei file con estensione admx e adml di Lync 2013 consente di scaricare modelli e di gestire in modo centralizzato le impostazioni di Criteri di gruppo per tutti i programmi e i language pack di Office. Per informazioni dettagliate, vedere “File dei modelli amministrativi di Office 2013 (ADMX, ADML)” nella documentazione di Office 2013 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=267516\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=267516%26clcid=0x410).

## Criteri di avvio automatico del client

Sono disponibili diversi criteri di avvio automatico del client che è consigliabile configurare prima che gli utenti accedano al server per la prima volta. Poiché questi criteri sono effettivi prima che il client esegua l'accesso e inizi a ricevere impostazioni di provisioning di tipo in-band dal server, è possibile usare Criteri di gruppo per configurarli. Per ulteriori informazioni, vedere [Configurazione dei criteri di avvio dei client in Lync Server 2013](lync-server-2013-configuring-client-bootstrapping-policies.md) nella documentazione relativa alla distribuzione.

