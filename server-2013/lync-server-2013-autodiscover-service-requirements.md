---
title: 'Lync Server 2013: Requisiti del servizio di individuazione automatica'
TOCTitle: Requisiti del servizio di individuazione automatica
ms:assetid: 0ac5dbf7-9acd-4d25-b21a-932022b8b983
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690012(v=OCS.15)
ms:contentKeyID: 49299633
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti del servizio di individuazione automatica per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-25_

Il servizio di individuazione automatica di Microsoft Lync Server 2013 viene eseguito nei server dei pool di server Director e Front End e, se pubblicato in DNS, può essere utilizzato dai dispositivi mobili con Lync Mobile per individuare i servizi per dispositivi mobili. Prima che i dispositivi mobili che eseguono Lync Mobile possano avvalersi dell'individuazione automatica, è necessario modificare gli elenchi dei nomi alternativi del soggetto dei certificati in qualsiasi Server Director e Front End Server che esegua tale servizio. Potrebbe inoltre essere necessario modificare gli elenchi dei nomi alternativi del soggetto nei certificati utilizzati per le regole di pubblicazione dei servizi Web esterni nei proxy inversi.

Per informazioni dettagliate sulle voci dei nomi alternativi del soggetto necessarie per i Director, i Front End Server e i proxy inversi, vedere [Requisiti tecnici per i dispositivi mobili in Lync Server 2013](lync-server-2013-technical-requirements-for-mobility.md) nella documentazione relativa alla pianificazione dei servizi per dispositivi mobili.

La decisione relativa agli elenchi dei nomi alternativi del soggetto nei proxy inversi dipende dal fatto che il servizio di individuazione automatica venga pubblicato sulla porta 80 o sulla porta 443:

  - **Pubblicato sulla porta 80**   Non sono necessarie modifiche relative ai certificati se la query iniziale inviata al servizio di individuazione automatica avviene sulla porta 80. Questo è dovuto al fatto che i dispositivi mobili che eseguono Lync accederanno al proxy inverso sulla porta 80 esternamente e quindi verranno reindirizzati a un Server Director o a un Front End Server sulla porta 8080 internamente. Per informazioni dettagliate, vedere la sezione "Processo di individuazione automatica iniziale tramite la porta 80" più avanti in questo argomento.

  - **Pubblicato sulla porta 443**   L'elenco dei nomi alternativi del soggetto nei certificati utilizzati dalla regola di pubblicazione dei servizi Web esterni deve contenere una voce *lyncdiscover.\<dominiosip\>* per ogni dominio SIP all'interno dell'organizzazione.

La riemissione dei certificati tramite un'autorità di certificazione interna in genere è un processo semplice, ma per i certificati pubblici utilizzati nella regola di pubblicazione dei servizi Web l'aggiunta di più voci dei nomi alternativi del soggetto può diventare un'attività dispendiosa. Per ovviare al problema, viene fornito il supporto per la connessione di individuazione automatica iniziale sulla porta 80, con conseguente reindirizzamento alla porta 8080 del pool di server Server Director o Front End Server.

Si supponga ad esempio che un client mobile che esegue Lync Mobile sia configurato per eseguire l'accesso a Lync Server 2013 mediante la funzionalità di individuazione automatica con HTTP per la richiesta iniziale.

## Processo di individuazione automatica iniziale per i dispositivi mobili che utilizzano la porta 80

1.  Il dispositivo mobile che esegue Lync Mobile cerca lyncdiscover.contoso.com con DNS, dove è presente un record A.

2.  Il sistema DNS esterno restituisce al client l'indirizzo IP dei servizi Web esterni.

3.  Il dispositivo mobile che esegue Lync Mobile invia la richiesta http://lyncdiscover.contoso.com?sipuri=lyncUser1@contoso.com al proxy inverso.

4.  La regola di pubblicazione Web inoltrerà la richiesta dalla porta 80 esternamente alla porta 8080 internamente che quindi la instraderà a un Server Director oppure a Front End Server.
    
    Poiché si tratta di una richiesta HTTP e non HTTPS, per supportare il servizio di individuazione automatica non sono necessarie modifiche per il certificato nella regola di pubblicazione dei servizi Web esterni.

5.  Il servizio di individuazione automatica restituisce gli URL dei servizi Web esterni nel formato HTTPS.

6.  Il dispositivo mobile che esegue Lync Mobile può quindi riconnettersi al proxy inverso sulla porta 443 e viene reinstradato tramite la porta 4443 al servizio per dispositivi mobili in esecuzione nel pool principale dell'utente.
    
    Poiché la query HTTPS riguarda l'URL dei servizi Web esterni e non l'URL del servizio di individuazione automatica, ha esito positivo perché il certificato conterrà già le voci dei nomi alternativi del soggetto per i nomi di dominio completi (FQDN) dei servizi Web esterni.
    
    In questo scenario non è necessario apportare modifiche ai certificati per supportare i servizi per dispositivi mobili.
    

    > [!NOTE]
    > Se nel server Web di destinazione è presente un certificato che include lyncdiscover.contoso.com come valore dell'elenco dei nomi alternativi del soggetto:<BR>a.&nbsp;&nbsp;&nbsp;Il server Web risponde con "Server Hello" e nessun certificato.<BR>b.&nbsp;&nbsp;&nbsp;Il dispositivo mobile che esegue Lync Mobile termina immediatamente la sessione.<BR>Se nel server Web di destinazione è presente un certificato che include lyncdiscover.contoso.com come valore dell'elenco dei nomi alternativi del soggetto:<BR>a.&nbsp;&nbsp;&nbsp;Il server Web risponde con "Server hello" e un certificato.<BR>b.&nbsp;&nbsp;&nbsp;Il dispositivo mobile che esegue Lync Mobile convalida il certificato e completa l'handshake.



Per supportare una connessione iniziale al servizio di individuazione automatica utilizzando la porta 80 nel server proxy inverso, è possibile creare una regola di pubblicazione http simile a questo esempio per una regola di pubblicazione Web di proxy inverso di Forefront Threat Management Gateway 2010:

1.  Creare una nuova regola di pubblicazione Web, ad esempio **Individuazione automatica Lync Server (HTTP)** .

2.  In **Nome pubblico** immettere lyncdiscover.contoso.com.

3.  Nella scheda **Bridging** selezionare solo l'opzione per inoltrare le richieste dalla porta 80 alla porta 8080.

4.  Nella scheda **Autenticazione** selezionare **Nessuna delega.** **Il client non può eseguire l'autenticazione direttamente** .

5.  Eseguire il commit delle modifiche e spostare la regola all'inizio dell'elenco delle regole di Lync (ordine di elaborazione First In).

## Mobilità per la distribuzione del dominio diviso

Uno spazio indirizzo SIP condiviso, noto anche come *dominio diviso* o *distribuzione ibrida* , è una configurazione in cui gli utenti sono distribuiti in una distribuzione locale e un ambiente online. Il risultato desiderato è che gli utenti, indipendentemente dalla posizione in cui si trova il server principale (in locale oppure online), accedano alla distribuzione e vengano reindirizzati alla posizione del server principale. A questo scopo, la funzionalità di individuazione automatica di Microsoft Lync Server 2013 viene utilizzata per reindirizzare gli utenti online alla topologia online. Questo risultato si ottiene configurando l'URL del servizio di individuazione automatica mediante Lync Server Management Shell e i cmdlet **Get-CsHostingProvider** e **Set-CsHostingProvider** .

Sarà necessario raccogliere e prendere nota degli attributi distribuiti seguenti:

  - In Lync Server Management Shell digitare
    
        Get-CsHostingProvider

  - Nei risultati, individuare il provider online con l'attributo **ProxyFQDN** . Ad esempio, sipfed.online.lync.com

  - Prendere nota del valore di ProxyFQDN

  - Abilitare la federazione nel Pannello di controllo di Lync Server locale, consentendo la federazione con il provider online

  - Abilitare la federazione per il provider online. Per impostazione predefinita, tutti gli utenti online sono abilitati per la federazione dei domini e possono comunicare con tutti i domini

  - Se si prevede di definire domini bloccati e consentiti, determinare i domini che verranno esplicitamente consentiti o bloccati

  - Per la federazione online è necessario pianificare le eccezioni del firewall, i certificati e i record dell'host DNS (A oppure AAAA se si utilizza IPv6). È inoltre necessario configurare i criteri di federazione. Per informazioni dettagliate, vedere [Pianificazione della federazione di Lync Server e Office Communications Server](lync-server-2013-planning-for-lync-server-and-office-communications-server-federation.md)

