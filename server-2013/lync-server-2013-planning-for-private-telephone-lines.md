---
title: 'Lync Server 2013: Pianificazione per le linee telefoniche private'
TOCTitle: Pianificazione per le linee telefoniche private
ms:assetid: 9cc4f9e1-7b7a-4699-bd05-f16669ef2d21
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412728(v=OCS.15)
ms:contentKeyID: 49301479
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione per le linee telefoniche private con Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-11_

In Lync Server 2013 è stata introdotta la possibilità per gli utenti di utilizzare una seconda linea telefonica privata oltre alla linea telefonica principale. Le linee telefoniche private sono spesso assegnate ai dirigenti e ad altri utenti che desiderano disporre di un numero di telefono non in elenco a cui essere raggiunti direttamente.

Le linee telefoniche private possono essere configurate solo con Lync Server Management Shell. Non è possibile eseguire questa operazione tramite il Pannello di controllo di Lync Server. Le linee telefoniche private vanno configurate solo nelle distribuzioni di Lync Server e non nelle distribuzioni miste.

## Caratteristiche delle linee telefoniche private

Anche se il concetto di seconda linea telefonica privata è fondamentalmente semplice, è importante comprendere le caratteristiche delle linee private e le relative analogie e differenze rispetto alle linee telefoniche principali dell'utente.

## Caratteristiche generali delle linee telefoniche private

  - Un utente può disporre di un'unica linea telefonica privata.

  - Un utente con una linea telefonica privata dispone di una sola casella vocale e riceve le notifiche di chiamata senza risposta presso un unico indirizzo di posta elettronica.

  - Un utente con una linea telefonica privata non dispone di un secondo indirizzo SIP e una seconda linea telefonica privata non fornisce una seconda presenza in rete, ad esempio una seconda identità di messaggistica istantanea.

  - Le linee telefoniche private sono disponibili solo per le distribuzioni locali e non per le distribuzioni ospitate di Lync Server.

## Differenze tra linee telefoniche private e linee telefoniche principali

  - I numeri di telefono delle linee telefoniche private non vengono visualizzati negli elenchi telefonici o negli elenchi di contatti derivati da Servizi di dominio Active Directory.

  - Le funzionalità di inoltro di chiamata, intercettazione team, delega delle chiamate, inoltro chiamata al team, risposta alle chiamate di gruppo e l'applicazione Response Group non sono disponibili per una linea telefonica privata.

  - Le chiamate a una linea telefonica privata sono caratterizzate da uno squillo speciale e la notifica di sistema per la chiamata informa l'utente che la chiamata in arrivo è sulla linea privata.

  - Le chiamate alla linea telefonica privata suonano sempre e non seguono le regole "non disturbare".

  - Le linee telefoniche private sono solo in ingresso e non possono essere utilizzate per eseguire chiamate in uscita. Quando un utente che dispone di una linea telefonica privata esegue una chiamata, questa ha origine dalla linea telefonica principale dell'utente e non nasconde alla persona chiamata il nome, né il numero telefonico principale dell'utente.

## Analogie tra linee telefoniche private e linee telefoniche principali

  - Le chiamate senza risposta a una linea telefonica privata vengono inoltrate alla stessa casella di posta in arrivo per la segreteria telefonica della linea telefonica principale (se la segreteria telefonica è abilitata).

  - Il parcheggio di chiamata e l'accettazione della chiamata funzionano esattamente allo stesso modo che nella linea telefonica principale dell'utente.

  - Quando per la linea telefonica principale di un utente è abilitato lo squillo simultaneo, lo è anche per la linea telefonica privata.

  - Il numero di telefono di una linea telefonica privata viene registrato nel record dei dettagli chiamata allo stesso modo del numero telefonico della linea telefonica principale dell'utente, ma con l'indicazione che si tratta di un numero privato.

  - Quando un utente risponde a una chiamata su una linea telefonica privata, questa viene trattata allo stesso modo di una chiamata sulla linea telefonica principale. Se ad esempio un utente riceve una chiamata sulla linea telefonica privata e la inoltra, oppure invita altre persone a una conferenza telefonica, il suo nome viene visualizzato in Lync 2013 e nell'ID chiamante viene visualizzato il numero di telefono della sua linea telefonica principale.

  - Un utente può deviare una chiamata (reindirizzarla a un'altra destinazione, ad esempio un telefono cellulare o il telefono di casa, prima di rispondere) proveniente dalla linea telefonica privata con la stessa procedura utilizzata per una linea telefonica principale.
    

    > [!NOTE]
    > Quando una chiamata a una linea privata viene instradata a un numero di telefono alternativo, il numero di telefono della linea telefonica privata viene reso disponibile al numero di telefono alternativo e può essere visualizzato nei log per tale numero.

    

    > [!NOTE]
    > Le chiamate da una conferenza alla linea telefonica privata non presenteranno l'indicazione <EM>linea privata</EM> nella notifica di sistema in arrivo.



## Amministrazione delle linee telefoniche private

Oltre agli aspetti tecnici di creazione e gestione delle linee telefoniche private, sarà necessario stabilire procedure amministrative. Ciò include la determinazione di criteri per definire chi nell'organizzazione abbia diritto a una linea privata, la creazione e la gestione di elenchi degli utenti e delle relative linee telefoniche, l'eventuale creazione di un elenco telefonico privato per i dirigenti, l'organizzazione della formazione degli utenti e le attività correlate.


> [!NOTE]
> La linea telefonica privata è archiviate in Active Directory come attributo msRTCSIP-PrivateLine dell'oggetto utente. Per impostazione predefinita i membri del gruppo Authenticated Users dispongono di accesso in lettura e scrittura a tale attributo.



## Assegnazione di numeri di telefono

Gli account per i nuovi utenti che hanno bisogno di linee telefoniche private vengono creati allo stesso modo degli account senza linee telefoniche private, utilizzando Pannello di controllo di Lync Server o Lync Server Management Shell.

Utilizzare il cmdlet **Set-CsUser** in Lync Server Management Shell per assegnare un numero di telefono alla linea telefonica privata di un utente, ad esempio, **Set-CsUser -Identity "sip:joe@contoso.com" -PrivateLine "Tel:+14255551212"** .

I numeri di telefono delle linee telefoniche private possono avere una lunghezza compresa tra 3 e 15 cifre e devono essere preceduti dal prefisso "TEL:". Possono avere qualsiasi indicativo località e codice paese/area geografica, sempre che l'organizzazione disponga della funzionalità DID (Direct Inward Dialing) per tale indicativo località e codice paese.

Per informazioni dettagliate sui cmdlet e Lync Server Management Shell, vedere la documentazione di [Lync Server Management Shell](lync-server-2013-lync-server-management-shell.md).

## Linee telefoniche private in distribuzioni miste

Le linee telefoniche private andrebbero configurate solo per le distribuzioni di Lync Server. In una distribuzione in cui sono presenti server Lync Server e Office Communications Server 2007 o Office Communications Server 2007 R2, quando un utente che utilizza una versione precedente tenta di chiamare una linea telefonica privata il routing della chiamata non riesce. in quanto il server non è in grado di eseguire la ricerca inversa del numero in una linea telefonica privata.

