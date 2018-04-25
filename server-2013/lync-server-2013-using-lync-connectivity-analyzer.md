---
title: Utilizzo dell'analizzatore connettività Lync
TOCTitle: Utilizzo dell'analizzatore connettività Lync
ms:assetid: 954953fb-0c7a-4fd5-8acd-68ecb59b20af
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ907302(v=OCS.15)
ms:contentKeyID: 52062232
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Utilizzo dell'analizzatore connettività Lync

 

_**Ultima modifica dell'argomento:** 2014-02-11_

Microsoft Lync Connectivity Analyzer consente agli amministratori di Lync di determinare se la distribuzione e la configurazione di Office 365 o dell'ambiente Lync Server locale soddisfano i requisiti per il supporto delle connessioni dalle app app Windows Store Lync e Lync nei dispositivi mobili.

Lync Connectivity Analyzer tenta la connessione a Lync Server in locale o a Skype for Business online usando gli stessi servizi e protocolli usati da app Windows Store Lync e le app Lync mobili. È possibile eseguire i test di connessione sulla rete interna o su una rete esterna connessa a Lync Server o a Skype for Business online. Lync Connectivity Analyzer offre un rapporto con informazioni dettagliate su ogni passaggio di connessione per facilitare la convalida della configurazione e la risoluzione dei problemi di connessione.

Lync Connectivity Analyzer verifica i componenti seguenti di Lync Server:

  - Servizio di individuazione automatica

  - Servizio broker autenticazione (Reach)

  - Servizio Mobility (MCX)

  - Servizio Mobility (UCWA)

  - Servizio WebTicket

Lync Connectivity Analyzer verifica la configurazione degli altri componenti seguenti:

  - Pubblicazione dei record DNS per gli URL di individuazione automatica

  - Certificati

  - Server proxy

È possibile scaricare Lync Connectivity Analyzer dall'Area download Microsoft all'indirizzo <http://go.microsoft.com/fwlink/?linkid=277056>.

## Per analizzare la connettività

1.  Immettere le credenziali per un account valido di Lync (un account Lync locale o un account Office 365Lync) che verrà usato dallo strumento per testare la connessione:
    
      - In **Lync Account Type** selezionare **Office 365** oppure **On-Premises**.
    
      - In **SIP URI** immettere l'indirizzo di accesso SIP per la connessione di Lync nel formato **utente@dominio.com**.
    
      - In **Password** immettere la password associata all'account.
    
      - In **User name (optional)** immettere un nome utente, se pertinente. Il nome utente è noto anche come nome dell'entità utente (UPN). Se il nome utente e l'URI SIP sono uguali non è necessario immettere un nome utente. Se sono diversi, immettere il nome utente nel formato **utente@dominio.com** o **dominio\\utente**, come appropriato.
    
      - In **Network access** scegliere **From inside my organization** se si esegue Lync Connectivity Analyzer da un computer connesso alla rete interna. In caso contrario, scegliere **External (Internet)**. Lync Connectivity Analyzer esegue sempre sia test interni che esterni, ma specificando se ci si trova all'interno o all'esterno della rete, lo strumento potrà stabilire meglio se determinati errori sono previsti.
    
      - In **Client** specificare se eseguire i test di connettività per **Lync Windows Store App**, **Lync Mobile 2010 App** o **Lync Mobile 2013 App**.
    
      - In **Server Discovery** selezionare il tipo di test da eseguire:
        
          - Se si desidera che lo strumento individui il server Lync automaticamente, selezionare **Automatic**.
        
          - Se si preferisce non eseguire il test di individuazione automatica oppure se si conosce il nome del server a cui si desidera connettersi, selezionare **Manual using address:** e specificare il nome di dominio completo (FQDN) del server Lync, ad esempio **lync.azienda.com**.

2.  (Facoltativo) In **Log File**, selezionare la casella di controllo se si desidera creare un file di log in un percorso specifico. Se la registrazione è abilitata, fare clic su **Clear** per cancellare il file di log, fare clic su **Open** per aprire e visualizzare il file e fare clic su **Email** per aprire un messaggio di posta elettronica e inviare i risultati al supporto tecnico (è necessario allegare manualmente il file di log dal percorso specificato).

3.  Fare clic su **Start**.

Nella figura seguente sono illustrati risultati di esempio di Lync Connectivity Analyzer.

**Lync Connectivity Analyzer**

![Cattura di schermata di Lync Connectivity Analyzer](images/JJ907302.a7cc0abe-fac2-4691-a7d8-9ffef59cdee5(OCS.15).png "Cattura di schermata di Lync Connectivity Analyzer")

## Componenti testati da Lync Connectivity Analyzer

Lync Connectivity Analyzer tenta di individuare il server Lync e di stabilire una connessione utilizzando gli stessi passaggi utilizzati da app Windows Store Lync e dalle app mobili Lync. I test vengono eseguiti come descritto in questa sezione.

Se si seleziona **Automatic discovery**, Lync Connectivity Analyzer esegue le operazioni seguenti:

  - Recupera gli URL di individuazione automatica da DNS (Domain Name System).

  - Tenta l'individuazione utilizzando il canale interno protetto, ad esempio, **HTTPS://lyncdiscoverinternal.azienda.com/**.

  - Tenta l'individuazione utilizzando il canale interno non protetto, ad esempio, **HTTP://lyncdiscoverinternal.azienda.com/**.

  - Tenta l'individuazione utilizzando il canale esterno protetto, ad esempio, **HTTPS://lyncdiscover.azienda.com/**.

  - Tenta l'individuazione utilizzando il canale esterno non protetto, ad esempio, **HTTP://lyncdiscover.azienda.com/**.

Se si seleziona **Use the following server discovery address**, Lync Connectivity Analyzer esegue le operazioni seguenti:

  - Recupera il nome di dominio completo (FQDN) del server da DNS.

  - Tenta l'individuazione utilizzando il canale protetto, ad esempio, **HTTPS://serverFQDN/**.

  - Tenta l'individuazione utilizzando il canale non protetto, ad esempio, **HTTP://serverFQDN/**.

Se si seleziona **Lync Windows Store app** in **Test the requirements for**, Lync Connectivity Analyzer esegue le operazioni seguenti:

  - Controlla che il servizio WebTicket sia disponibile e verifica l'autenticazione delle credenziali dell'account Lync.

  - Controlla che il servizio broker autenticazione (Reach) sia disponibile.

Se si seleziona **Lync Mobile 2010 App** in **Client**, Lync Connectivity Analyzer esegue le operazioni seguenti:

  - Controlla che il servizio WebTicket sia disponibile e verifica l'autenticazione delle credenziali dell'account Lync.

  - Controlla che il servizio Mobility (MCX) sia disponibile.

Se si seleziona **Lync Mobile 2013 App** in **Client**, Lync Connectivity Analyzer esegue le operazioni seguenti:

  - Controlla che il servizio WebTicket sia disponibile e verifica l'autenticazione delle credenziali dell'account Lync.

  - Controlla che il servizio Mobility (UCWA) sia disponibile.

Durante l'esecuzione di questi test Lync Connectivity Analyzer convalida i certificati installati in Lync Server, i servizi di bilanciamento del carico hardware, i server proxy e il computer in cui si eseguono i test.

## Altre risorse

Microsoft offre inoltre Microsoft Remote Connectivity Analyzer, uno strumento di test della connettività basato su Web, disponibile all'indirizzo <https://testconnectivity.microsoft.com/>. Esistono le differenze seguenti tra Lync Connectivity Analyzer e Remote Connectivity Analyzer:

  - Remote Connectivity Analyzer consente di testare la connettività per Microsoft Exchange e Outlook, oltre che per Microsoft Lync.

  - Remote Connectivity Analyzer completa l'accesso SIP, mentre Lync Connectivity Analyzer esegue solo la convalida delle credenziali dell'account senza eseguire l'accesso.

  - Remote Connectivity Analyzer verifica le connessioni solo dall'esterno della rete dell'organizzazione perché viene eseguito da un server Web pubblico.

  - Remote Connectivity Analyzer non controlla la disponibilità dei servizi broker autenticazione (Reach), Mobility (MCX) e WebTicket.

  - Lync Connectivity Analyzer controlla il servizio di individuazione automatica.

  - Remote Connectivity Analyzer consente la connessione a qualsiasi versione di Lync Server, mentre Lync Connectivity Analyzer può connettersi in modo corretto solo a Lync Server 2010 con gli aggiornamenti cumulativi per Lync Server 2010 di febbraio 2012 (come minimo) o all'ultima versione di Lync Server.

Nella documentazione seguente vengono descritti i requisiti e le procedure per la distribuzione e la configurazione di Lync Server per il supporto di app Windows Store Lync e dei client mobili di Lync:

  - [Distribuzione di client e dispositivi in Lync Server 2013](lync-server-2013-deploying-clients-and-devices.md)

  - [Pianificazione della versione per dispositivi mobili in Lync Server 2013](lync-server-2013-planning-for-mobility.md)

  - [Distribuzione delle funzionalità per dispositivi mobili in Lync Server 2013](lync-server-2013-deploying-mobility.md)

