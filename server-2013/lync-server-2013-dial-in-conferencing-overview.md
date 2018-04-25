---
title: Panoramica delle conferenze telefoniche con accesso esterno
TOCTitle: Panoramica delle conferenze telefoniche con accesso esterno
ms:assetid: 6e581cef-960a-4730-8b22-91b2129d34e3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398524(v=OCS.15)
ms:contentKeyID: 49300918
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Panoramica delle conferenze telefoniche con accesso esterno

 

_**Ultima modifica dell'argomento:** 2012-09-30_

Se nell'organizzazione sono presenti utenti che devono partecipare a conferenze locali di Lync Server 2013 quando non sono in ufficio o non possono accedere a un computer, è possibile distribuire la funzionalità per conferenze telefoniche con accesso esterno in modo che tali utenti possano partecipare alla conferenza utilizzando un telefono PSTN (Public Switched Telephone Network).

Le conferenze telefoniche con accesso esterno sono una caratteristica facoltativa per la distribuzione di conferenze di Lync Server 2013. Benché le conferenze telefoniche con accesso esterno utilizzino alcuni degli stessi componenti di Lync Server 2013 utilizzati da VoIP aziendale , è possibile distribuire tali conferenze anche se non si distribuisce VoIP aziendale.


> [!NOTE]
> Se si distribuiscono le conferenze telefoniche con accesso esterno, è necessario distribuirle in ogni pool in cui si distribuiscono le conferenze di Lync Server 2013. . Non è necessario assegnare numeri di accesso in ogni pool, ma è necessario distribuire la caratteristica di accesso esterno in ogni pool. Questo requisito supporta la caratteristica di registrazione dei nomi quando un utente chiama un numero di accesso da un pool per partecipare a una conferenza di Lync Server 2013 in un pool diverso.



È necessario abilitare le conferenze per l'accesso esterno tramite criteri di riunione. Per impostazione predefinita, le conferenze abilitate per l'accesso esterno includono le informazioni seguenti nell'invito alla conferenza:

  - ID conferenza numerico che identifica la conferenza.

  - Uno o più numeri di accesso PSTN.

  - Collegamento a pagina Impostazioni conferenza telefonica con accesso esterno, che contiene un elenco completo di numeri di accesso con le rispettive lingue associate, un'area in cui creare, reimpostare o sbloccare numeri di identificazione personali (PIN) e altre informazioni, ad esempio i controlli DTMF (Dual-Tone Multi-Frequency).

Le conferenze telefoniche con accesso esterno supportano utenti sia aziendali sia anonimi. Gli utenti aziendali dispongono di credenziali Servizi di dominio Active Directory e account Lync Server 2013 all'interno dell'organizzazione. Gli utenti anonimi non dispongono di credenziali aziendali all'interno dell'organizzazione. Nel contesto delle conferenze telefoniche con accesso esterno un utente in un'organizzazione di un partner federato che utilizza la rete PSTN per connettersi a una conferenza viene considerato un utente anonimo. Per le conferenze telefoniche con accesso esterno, diversamente da altri contesti, gli utenti federati non vengono autenticati.

Gli utenti aziendali o i coordinatori delle conferenze che partecipano a una conferenza abilitata per l'accesso esterno compongono uno dei numeri di accesso alla conferenza e devono immettere l'ID conferenza. Se un coordinatore non ha ancora eseguito l'accesso alla riunione, gli utenti possono immettere il proprio interno (o il numero di telefono completo) per le comunicazioni unificate e il PIN o attendere di essere ammessi da un coordinatore. Gli organizzatori della riunione possono partecipare alla riunione come coordinatori semplicemente immettendo il proprio PIN. Il Front End Server utilizza la combinazione di numero di telefono completo o estensione e PIN per associare in modo univoco gli utenti aziendali alle rispettive credenziali Active Directory. Di conseguenza, gli utenti aziendali vengono autenticati e identificati in base al nome nella conferenza. Gli utenti aziendali possono anche assumere un ruolo della conferenza predefinito dall'organizzatore.


> [!NOTE]
> Gli utenti aziendali che eseguono l'accesso esterno da un telefono IP dell'ufficio o da Lync Server 2013 o Lync 2010 Attendant non devono immettere il proprio numero di telefono, perché sono già autenticati.



Gli utenti anonimi che desiderano partecipare a una conferenza telefonica con accesso esterno compongono uno dei numeri di accesso alla conferenza e devono quindi immettere il proprio ID conferenza. Gli utenti anonimi non autenticati devono inoltre registrare il proprio nome. Il nome registrato identifica gli utenti non autenticati nella conferenza. Gli utenti anonimi non vengono ammessi alla conferenza fino a quando un responsabile o un utente autenticato non accede, e non possono ricevere un ruolo predefinito.


> [!NOTE]
> Gli utenti aziendali che scelgono di non immettere il proprio numero di telefono e il PIN non vengono autenticati e pertanto devono registrare il proprio nome e vengono considerati utenti anonimi nella conferenza.



In fase di pianificazione, l'organizzatore della riunione può scegliere di limitare l'accesso alla riunione chiudendola o bloccandola. In questo caso, agli utenti connessi tramite chiamata in ingresso viene richiesto di eseguire l'autenticazione. Se gli utenti riescono ad autenticarsi o scelgono di non farlo, vengono trasferiti alla pagina di benvenuto, in cui attendono fino a quando un responsabile non li accetta o rifiuta o, in caso di timeout, non vengono disconnessi. Gli utenti connessi tramite chiamata in ingresso ascoltano un brano musicale se devono attendere di essere ammessi alla conferenza. Una volta ammessi alla conferenza, tali utenti possono partecipare alla parte audio della conferenza e utilizzare i comandi DTMF dal tastierino del telefono. I responsabili connessi tramite chiamata in ingresso possono utilizzare i comandi DTMF per consentire o meno ai partecipanti di disattivare il proprio audio, bloccare o sbloccare la conferenza, ammettere altre persone dalla pagina di benvenuto e attivare o disattivare gli annunci di entrata o uscita. I responsabili possono inoltre utilizzare un comando DTMF per ammettere chiunque dalla pagina di benvenuto, scelta che comporta la modifica delle autorizzazioni della riunione in modo da ammettere chiunque acceda successivamente. Tutti i partecipanti connessi tramite chiamata in ingresso possono utilizzare i comandi DTMF per ascoltare la Guida e l'elenco dei partecipanti e disattivare il proprio audio.

I partecipanti connessi tramite chiamata in ingresso, che chiamino o meno dalla rete PSTN, possono ascoltare annunci personali durante la conferenza, ad esempio relativi alla disattivazione o meno del proprio audio, alla registrazione o meno della riunione o all'eventuale presenze di altri utenti nella pagina di benvenuto.


> [!NOTE]
> I partecipanti che accedono alla conferenza facendo clic su un collegamento invece di comporre un numero non possono ascoltare gli annunci personali.


