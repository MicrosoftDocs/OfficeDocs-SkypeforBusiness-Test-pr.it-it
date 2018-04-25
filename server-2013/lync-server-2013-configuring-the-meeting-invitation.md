---
title: Configurazione della convocazione di riunione in Lync Server 2013
TOCTitle: Configurazione della convocazione di riunione in Lync Server 2013
ms:assetid: 7faa4797-0344-418b-9fa3-59dfb9c2baf7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398638(v=OCS.15)
ms:contentKeyID: 49301129
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione della convocazione di riunione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-07-16_

È possibile personalizzare gli inviti alle riunioni inviati da componente aggiuntivo per riunioni online per Lync 2013 includendo i seguenti elementi opzionali nel corpo dell'invito:

  - **Logo dell'organizzazione** È possibile aggiungere il logo della propria organizzazione agli inviti, tramite l'opzione URL logo. Se gli inviti sono inviati a utenti esterni all'organizzazione, l'immagine deve trovarsi presso un URL disponibile al pubblico. I formati supportati sono GIF e JPG. Sebbene Lync Server 2013 archivi l'URL senza limiti di dimensione per l'immagine, per ottenere risultati ottimali è consigliabile che le dimensioni dell'immagine non superino 30 pixel in altezza e 188 pixel in larghezza.

  - **Guida personalizzata o collegamento al supporto** È possibile aggiungere un URL alla guida o al sito del team di supporto dell'organizzazione. Se gli inviti sono inviati a utenti esterni all'organizzazione, l'URL disponibile al pubblico.. La lunghezza massima dell'URL è 1 KB.

  - **Testo della dichiarazione di non responsabilità** È possibile aggiungere un URL al testo della dichiarazione di non responsabilità visualizzato negli inviti. Se gli inviti sono inviati a utenti esterni all'organizzazione, l'URL disponibile al pubblico.. La lunghezza massima dell'URL è 1 KB.

  - **Piè di pagina personalizzato** Aggiungere testo da visualizzare come piè di pagina. La lunghezza massima del testo che può essere aggiunto è 2 KB.

È possibile configurare queste opzioni utilizzando Pannello di controllo di Lync Server o Lync Server Management Shell.


**Per personalizzare gli inviti alle riunioni utilizzando Pannello di controllo di Lync Server**

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsServerAdministrator o CsAdministrator, accedere a un computer nella rete in cui è stato distribuito Lync Server 2013.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Servizio di conferenza** e quindi su **Configurazione riunione**.

4.  Nella pagina **Configurazione riunione** fare clic su **Nuovo** e quindi eseguire una delle operazioni seguenti:
    
      - Per creare un criterio a livello di sito, fare clic su **Configurazione sito**. Nel campo di ricerca **Seleziona un sito** digitare il nome del sito per cui si desidera definire le impostazioni di partecipazione alle riunioni, per intero o in parte. Fare clic sul sito desiderato nell'elenco dei siti e quindi fare clic su **OK**.
    
      - Per creare un criterio a livello di pool, fare clic su **Configurazione pool**. Nel campo di ricerca **Seleziona un servizio** digitare il nome del pool per cui si desidera definire le impostazioni di partecipazione alle riunioni, per intero o in parte. Fare clic su un pool desiderato nell'elenco di servizi e quindi su **OK**.

5.  Effettuare una delle operazioni seguenti:
    
      - Nel campo **URL logo**, digitare l'URL relativo all'immagine del logo dell'organizzazione.
    
      - Nel campo **URL guida**, digitare l'URL della guida o del sito di supporto dell'organizzazione.
    
      - Nel campo **Testo legale**, digitare l'URL del testo legale o della dichiarazione di non responsabilità che si desidera includere negli inviti alle riunioni.
    
      - Nel campo **Testo piè di pagina personalizzato**, digitare un testo per il piè di pagina, di massimo 2 KB.

**Per personalizzare gli inviti alle riunioni utilizzando Lync Server Management Shell**

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Eseguire il cmdlet **New-CsMeetingConfiguration** o **Set-CsMeetingConfiguration** per creare o configurare le opzioni degli inviti alle riunioni. Ad esempio, eseguire:
    
        New-CsMeetingConfiguration -Identity site:Redmond -EnableInviteCustomization $True -LogoURL "http://www.contoso.com/logo/contosobanner.gif" -HelpURL "http://www.contoso.com/support" -LegalURL "http://www.contoso.com/disclaimer" -CustomFooterText "Communications may be monitored or recorded."

