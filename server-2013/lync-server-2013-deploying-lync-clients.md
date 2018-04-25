---
title: Distribuzione di client Lync
TOCTitle: Distribuzione di client Lync
ms:assetid: 3d10abf2-d484-4fa0-8f10-4a5f9dfba4f5
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204827(v=OCS.15)
ms:contentKeyID: 49300273
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuzione di client Lync

 

_**Ultima modifica dell'argomento:** 2012-10-03_

Lync 2013 introduce un approccio diverso alla distribuzione client. A differenza delle versioni precedenti, Lync 2013 non dispone più di uno specifico programma di installazione. Lync è invece incluso nel programma di installazione di Office 2013. Per distribuire Lync 2013 agli utenti è possibile utilizzare i metodi di installazione e gli strumenti di personalizzazione di Office 2013.

  - **Office 2013 Windows Installer** è un pacchetto di installazione basato su Windows Installer composto da più file MSI. La creazione di un prodotto completo si basa sulla combinazione di un pacchetto MSI principale indipendente dalla lingua con uno o più pacchetti specifici della lingua. I singoli pacchetti vengono assemblati durante l'installazione mentre le attività di personalizzazione e manutenzione vengono eseguite durante e dopo l'installazione di Office nei computer degli utenti. Gli argomenti di questa sezione descrivono come utilizzare e personalizzare Office 2013 Windows Installer per distribuire Lync 2013.

  - **Office 2013 a portata di clic** è un programma di installazione che scarica i file di installazione di Office per l'utente dal portale di Microsoft Office 365. Gli amministratori possono personalizzare l'installazione utilizzando lo strumento di distribuzione di Office per i prodotti a portata di clic. Poiché Office 2013 a portata di clic viene utilizzato principalmente nell'ambiente Microsoft Office 365, questo metodo di installazione non viene descritto nei dettagli in questa sezione. Informazioni dettagliate sull'utilizzo e sulla personalizzazione dell'installazione dei prodotti a portata di clic sono disponibili nella documentazione dell'Office 2013 Resource Kit. Gli amministratori possono anche scaricare i file di origine della lingua e del programma Office 2013 a portata di clic in una posizione locale. Ciò è utile quando si desidera ridurre il numero di richieste nella rete o impedire l'installazione del software da Internet a causa dei requisiti di sicurezza aziendale.

Gli argomenti di questa sezione sono incentrati sulla distribuzione dei client mediante l'utilizzo del programma di installazione basato su MSI di Office 2013. Il riferimento principale consigliato è la documentazione dell'Office 2013 Resource Kit, che descrive in dettaglio come preparare un'infrastruttura, personalizzare l'installazione e distribuire Office 2013. La documentazione di Office deve essere tuttavia utilizzata insieme agli argomenti di questa sezione che riportano considerazioni sulla distribuzione specifiche di Lync 2013.


> [!NOTE]
> <UL>
> <LI>
> <P>Il componente aggiuntivo per riunioni online per Lync 2013, che supporta la gestione di riunioni dal client di collaborazione e messaggistica di Outlook, viene installato automaticamente con Lync 2013.</P>
> <LI>
> <P>Il programma di installazione di Office 2013 non disinstalla le versioni precedenti di Lync o Office Communicator. Il client Lync 2013 viene installato side-by-side con altri client Lync o Office Communicator</P></LI></UL>



## Contenuto della sezione

  - [Personalizzazione dell'installazione dei client](lync-server-2013-customizing-client-installation.md)

  - [Personalizzazione del comportamento e dell'interfaccia utente di Lync](lync-server-2013-customizing-lync-behavior-and-the-user-interface.md)

  - [Personalizzazione del componente aggiuntivo per riunioni online](lync-server-2013-customizing-the-online-meeting-add-in.md)

  - [Configurazione della pagina di partecipazione alle riunioni in Lync Server 2013](lync-server-2013-configuring-the-meeting-join-page.md)

  - [Configurazione delle versioni client supportate](lync-server-2013-configuring-supported-client-versions.md)

  - [Configurazione della modalità privacy della presenza avanzata](lync-server-2013-configuring-enhanced-presence-privacy-mode.md)

