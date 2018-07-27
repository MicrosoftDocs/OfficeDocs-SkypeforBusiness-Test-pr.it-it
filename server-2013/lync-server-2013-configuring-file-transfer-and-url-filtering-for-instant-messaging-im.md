---
title: Configurazione del filtro per trasferimento di file e URL per la messaggistica istantanea in Lync Server 2013
TOCTitle: Configurazione del filtro per trasferimento di file e URL per la messaggistica istantanea in Lync Server 2013
ms:assetid: 115a1a2c-599f-474c-a063-52f7144b5246
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg520952(v=OCS.15)
ms:contentKeyID: 49299715
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione del filtro per trasferimento di file e URL per la messaggistica istantanea in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Il filtro di protezione per messaggi istantanei consente di proteggere la distribuzione di Lync Server 2013 dalla diffusione delle forme più comuni di virus con ripercussioni minime sull'esperienza utente. Utilizzare il filtro di protezione per messaggi istantanei per configurare filtri per bloccare i messaggi istantanei indesiderati o potenzialmente pericolosi provenienti da endpoint sconosciuti esterni al firewall aziendale. È possibile configurare i filtri specificando i criteri da utilizzare per determinare gli elementi da bloccare, ad esempio i messaggi istantanei contenenti collegamenti ipertestuali con prefissi specifici e file con estensioni specifiche.

Il filtro di protezione per messaggi istantanei offre le funzionalità seguenti:

  - Filtro avanzato per gli URL

  - Filtro avanzato per il trasferimento di file

La configurazione del filtro di protezione per messaggi istantanei prevede quanto segue:

  - Configurazione del filtro per gli URL

  - Configurazione del filtro per il trasferimento di file

## Modalità di applicazione delle opzioni di filtro ai messaggi istantanei

Prima di distribuire il filtro di protezione per messaggi istantanei, è necessario acquisire familiarità con le modalità di applicazione delle opzioni di filtro quando i messaggi vengono instradati da un server Lync Server 2013 a un altro. Il modo in cui queste opzioni di filtro vengono applicate è coerente, indipendentemente dal fatto che i server si trovino in una singola organizzazione oppure oltre i limiti dell'organizzazione. Tale coerenza si applica al modo in cui i testi delle note e degli avvisi personalizzati vengono inseriti nei messaggi e inviati tra server.


> [!NOTE]
> Il filtro di protezione per messaggi istantanei comporta un aumento della quantità di risorse CPU necessarie per elaborare gli URL in un messaggio. La maggiore richiesta di risorse della CPU influisce anche sulle prestazioni di Lync Server.



Utilizzando la pagina **Filtro URL** nel gruppo **Messaggistica istantanea e presenza** del Pannello di controllo di Lync Server, è possibile bloccare alcuni o tutti i collegamenti ipertestuali oppure configurare un avviso. L'avviso viene inserito all'inizio di un messaggio istantaneo contenente un collegamento ipertestuale quando per **Prefisso di collegamento ipertestuale** si seleziona l'opzione **Invia messaggio di avviso**.

Quando un messaggio istantaneo passa da un server a un altro, si applicano le linee guida generali seguenti:

  - Se un server blocca un messaggio istantaneo (perché è stata selezionata la casella di controllo **Blocca URL con estensione di file** nella pagina **Filtro URL** o perché per **Prefisso di collegamento ipertestuale** è stata selezionata l'opzione **Blocca collegamenti ipertestuali**), al client viene restituito un messaggio di errore. I server successivi non ricevono il messaggio istantaneo.

  - Se un server (Server1) aggiunge un avviso a un messaggio istantaneo contenente un collegamento ipertestuale attivo, un server successivo (Server2) che riceve il messaggio istantaneo può comunque eseguire un'azione diversa in base a tale collegamento ipertestuale attivo presente nel messaggio istantaneo e bloccare il messaggio o aggiungere un avviso. Se Server2 è configurato solo per aggiungere un avviso per l'URL, il precedente avviso aggiunto da Server1 viene rimosso e quello configurato in Server2 viene aggiunto all'inizio del messaggio istantaneo.


> [!NOTE]
> Se si esegue Lync Server 2013 in un ambiente misto, Live Communications Server 2005 con SP1 è la versione minima richiesta per utilizzare l'applicazione del filtro di protezione per messaggi istantanei. Il filtro di protezione per messaggi istantanei non è supportato su Live Communications Server 2005 senza SP1.



## Filtro per gli URL

Gli URL vengono filtrati in base al relativo prefisso di collegamento ipertestuale. Gli esempi seguenti sono prefissi validi:

  - www\*.

  - ftp.

  - http:

Se non si configura il filtro per messaggi istantanei in modo da filtrare gli URL, tutti gli URL presenti nei messaggi istantanei verranno passati attraverso il server senza essere modificati. Se si configura il filtro per messaggi istantanei in modo da filtrare gli URL, gli URL presenti nei messaggi istantanei verranno filtrati in base alle opzioni selezionate nella finestra di dialogo **Modifica filtro URL** o **Crea nuovo filtro URL**.

  - **Abilita filtro URL**   Questa opzione consente di filtrare gli URL per l'intera distribuzione o solo per il sito selezionato.

  - **Blocca URL con estensione di file**   Il filtro per messaggi istantanei blocca qualsiasi URL Intranet o Internet attivo contenente un file con un'estensione elencata in **Estensioni di file da bloccare** nella finestra di dialogo **Modifica filtro file**. Quando un URL viene bloccato, al mittente viene visualizzato un messaggio di errore. Se viene selezionata, questa opzione ha la precedenza su tutte le altre opzioni di filtro per le estensioni di file definite in **Estensioni di file da bloccare**.
    
    > [!IMPORTANT]  
    > Il filtro delle estensioni di file è limitato ai nomi file standard. Il filtro potrebbe non funzionare con estensioni di file incorporate in altri nomi.

Per configurare la modalità con cui vengono gestiti i collegamenti ipertestuali nelle conversazioni istantanee, selezionare una delle opzioni seguenti in **Prefisso di collegamento ipertestuale**:

  - **Non filtrare**   Gli URL presenti nei messaggi vengono inviati attraverso il server. Quando si seleziona questa opzione, viene visualizzata la casella **Consenti messaggio**. In tale casella specificare la nota che si desidera inserire all'inizio di ogni messaggio istantaneo contenente collegamenti ipertestuali. Questa nota può essere costituita al massimo da 65535 caratteri.

  - **Blocca collegamenti ipertestuali**   Il recapito dei messaggi istantanei contenenti collegamenti ipertestuali attivi viene bloccato da Lync Server e al mittente viene visualizzato un messaggio di errore.

  - **Invia messaggio di avviso**   Lync Server consente i collegamenti ipertestuali attivi nei messaggi istantanei, ma include un avviso. Quando si seleziona questa opzione, viene visualizzata la casella **Messaggio di avviso**. In tale casella è necessario digitare l'avviso che si desidera inserire nei messaggi istantanei contenenti collegamenti ipertestuali validi. L'avviso ad esempio potrebbe segnalare i pericoli che si possono correre facendo clic su un collegamento sconosciuto o fare riferimento ai requisiti e ai criteri pertinenti dell'organizzazione. Questo avviso può essere costituito al massimo da 65535 caratteri.

Se si seleziona **Blocca collegamenti ipertestuali** o **Invia messaggio di avviso**, saranno disponibili le opzioni seguenti:

  - **Escludi collegamenti ipertestuali Intranet locali**   Il filtro per messaggi istantanei blocca solo gli URL Internet. Gli URL relativi ai percorsi all'interno della rete Intranet vengono passati attraverso il server senza essere modificati. Gli URL Intranet passati dai singoli server che eseguono Lync Server dipendono tuttavia dai tipi di siti Web locali considerati parte dell'area Intranet. Per verificare le impostazioni dell'area Intranet di un server, vedere la procedura per configurare le impostazioni Intranet in Internet Explorer in [Modificare il filtro URL predefinito](lync-server-2013-modify-the-default-url-filter.md).

  - **Filtra i seguenti prefissi di collegamento ipertestuale**   Per specificare i prefissi da bloccare, fare clic su **Seleziona** e quindi in **Seleziona prefisso di collegamento ipertestuale** aggiungere i prefissi all'elenco **Prefissi di collegamento ipertestuale**.
    
    Tutti i prefissi, ad eccezione di **href**, devono terminare con un punto o i due punti oppure con un asterisco seguito da un punto. I prefissi validi possono contenere qualsiasi carattere compreso nell'insieme di caratteri validi per gli URL ad eccezione dell'asterisco (\*). L'insieme di caratteri validi per gli URL è il seguente: \#\*+/0123456789=@ABCDEFGHIJKLMNOPQRSTUVWXYZ^\_\` abcdefghijklmnopqrstuvwxyz|~

## Filtro per il trasferimento di file

Il filtro per il trasferimento di file riguarda sia i messaggi istantanei che le conferenze. Per le conferenze, queste impostazioni influiscono sia sulla funzionalità relativa agli stampati del client Office Live Meeting 2007 che sulle funzionalità di riproduzione multimediale.


> [!NOTE]
> Anche Lync Server offre opzioni per l'impostazione del trasferimento di file. Tale opzione del lato server viene offerta in aggiunta ai controlli del lato client disponibili in Lync Server.



È possibile filtrare i trasferimenti di file durante le conversazioni istantanee, quando si utilizza la funzionalità relativa agli stampati del client Office Live Meeting 2007 e per le funzionalità di riproduzione multimediale per tutti i tipi di file. Per controllare i trasferimenti di file, è possibile impostare le opzioni seguenti:

  - **Abilita filtro file**   Questa opzione consente di filtrare i file per l'intera distribuzione o solo per il sito selezionato.
    
    Quando si abilita il filtro per i file, è possibile selezionare una delle opzioni seguenti in **Trasferimento file**:
    
      - **Blocca tipi di file specifici**   È possibile indicare quali richieste di trasferimento di file vengono filtrate dal server specificando un elenco delle estensioni di file da bloccare. Le voci nell'elenco possono contenere tutti i caratteri standard, ma non il carattere jolly (\*). Nel client Office Live Meeting 2007 la funzionalità relativa agli stampati sarà abilitata, ma i file con le estensioni specificate non potranno essere caricati o scaricati. Se si seleziona la casella di controllo **Blocca URL con estensione di file** nelle impostazioni di un filtro per gli URL nella scheda **Filtro URL**, tale filtro utilizzerà questo stesso elenco per bloccare i collegamenti ipertestuali attivi contenenti una qualsiasi di queste estensioni di file. Per specificare quali tipi di file bloccare, fare clic su **Seleziona** e quindi in **Seleziona estensioni di file** aggiungere le estensioni di file desiderate all'elenco **Estensioni di file selezionate**.
    
      - **Blocca tutto**   Il server rimuove tutti i messaggi istantanei contenenti richieste di trasferimento di file e restituisce un messaggio di errore al mittente della richiesta. La funzionalità relativa agli stampati del client Office Live Meeting 2007 sarà disabilitata.

> [!IMPORTANT]  
> Il filtro delle estensioni di file è limitato ai nomi file standard. Il filtro potrebbe non funzionare con estensioni di file incorporate in altri nomi.

## Contenuto della sezione

  - [Modificare il filtro trasferimento file predefinito](lync-server-2013-modify-the-default-file-transfer-filter.md)

  - [Creare un nuovo filtro trasferimento file per un sito specifico](lync-server-2013-create-a-new-file-transfer-filter-for-a-specific-site.md)

  - [Modificare il filtro URL predefinito](lync-server-2013-modify-the-default-url-filter.md)

  - [Creare un nuovo filtro URL per gestire i collegamenti ipertestuali nelle conversazioni istantanee](lync-server-2013-create-a-new-url-filter-to-handle-hyperlinks-in-im-conversations.md)

## Vedere anche

#### Ulteriori risorse

[Gestione delle impostazioni di messaggistica istantanea e presenza in Lync Server 2013](lync-server-2013-managing-im-and-presence-settings.md)

