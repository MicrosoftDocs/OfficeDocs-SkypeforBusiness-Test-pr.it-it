---
title: 'Lync Server 2013: Tecnologie di virtualizzazione supportate e limitazioni note'
TOCTitle: Tecnologie di virtualizzazione supportate e limitazioni note
ms:assetid: 6d3d749d-e840-4c05-afae-d6e69e7616aa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204982(v=OCS.15)
ms:contentKeyID: 49300905
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Tecnologie di virtualizzazione supportate e limitazioni note in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-01-26_

Il plug-in VDI di Lync consente l'utilizzo di chiamate audio e video per le tecnologie di virtualizzazione supportate. Questo permette di estendere la funzionalità illustrata per Microsoft Lync Server 2010 nel white paper [Virtualizzazione client in Microsoft Lync 2010](http://go.microsoft.com/fwlink/?linkid=330447). In conformità con le normative telefoniche standard, è incluso anche il supporto per E911. Nelle sezioni seguenti vengono descritte le tecnologie di virtualizzazione supportate dal plug-in VDI di Lync e le limitazioni note delle funzionalità.

## Supporto per le tecnologie di virtualizzazione

Il plug-in VDI di Lync supporta la comunicazione remota desktop completa nello scenario desktop virtuale personale, ma non nello scenario sessione desktop remoto. Questi scenari possono essere descritti come segue:

  - **Supportati: desktop virtuali personalizzati o Virtual Desktop Infrastructure (VDI).**   In questo scenario, ogni utente esegue l'accesso a un desktop virtuale personalizzabile ed è in grado di salvare i file sul desktop che persiste tra le sessioni. Servizi Desktop remoto Microsoft, VMware Horizon View e Citrix XenDesktop sono esempi di implementazioni testate per l'utilizzo con Lync. Per ulteriori informazioni sugli hardware client e gli ambienti VDI per fornitori specifici testati da Microsoft, vedere [Infrastruttura qualificata per Microsoft Lync](http://go.microsoft.com/fwlink/?linkid=313435).

  - **Non supportati: sessioni desktop remoto.**   In questo scenario, ogni utente esegue l'accesso a una sessione desktop virtuale generica che non può essere personalizzata. Le implementazioni di esempio includono sessione desktop remoto Microsoft e Citrix XenApp combinato con Citrix Receiver.

Il plug-in VDI di Lync non supporta altre tecnologie di virtualizzazione, ad esempio la virtualizzazione di applicazioni, che consente l'utilizzo di un'applicazione senza richiedere l'installazione dell'applicazione completa in locale. Le implementazioni di esempio includono Citrix XenApp e Microsoft Application Virtualization (App-V). Lo streaming di applicazioni, la comunicazione remota applicazioni e le modalità miste di virtualizzazione (ad esempio, la comunicazione remota applicazioni in una comunicazione remota desktop completa) non sono supportati.

Per consentire l'estendibilità, il plug-in VDI di Lync è stato progettato per utilizzare API indipendenti dalla piattaforma chiamate canali virtuali dinamici. Per gli scenari non esplicitamente supportati da Lync, fare riferimento alle indicazioni di supporto del provider di soluzioni VDI.

## Limitazioni note delle funzionalità

Le seguenti sono limitazioni note dell'utilizzo di Lync 2013 in un ambiente VDI:

  - Supporto limitato per le funzioni di Delega delle chiamate e Agent Anonymization di Response Group.

  - Non è previsto supporto per le seguenti caratteristiche:
    
      - Pagine di regolazione dispositivi audio e video integrati.
    
      - Video con visualizzazioni multiple.
    
      - Registrazione delle conversazioni.
    
      - Partecipazione anonima alle riunioni (ovvero, partecipazione e riunioni di Lync ospitate da un'organizzazione non federata con la propria).
    
      - Utilizzo del plug-in VDI di Lync insieme a un dispositivo di Lync Phone Edition.
    
      - Continuità di chiamata in caso di problemi di rete.
    
      - Suonerie personalizzate e musica di attesa.

  - Il plug-in VDI di Lync non è supportato nell'ambiente Office 365.

