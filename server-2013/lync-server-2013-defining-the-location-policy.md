---
title: 'Lync Server 2013: Definizione di criteri percorso'
TOCTitle: Definizione di criteri percorso
ms:assetid: da3cca7f-f6e5-4b6f-90a1-2008e3dd1ebd
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398962(v=OCS.15)
ms:contentKeyID: 49302167
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Definizione di criteri percorso per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-29_

In ogni criterio percorso sono contenute le informazioni seguenti:

  - **Servizi di emergenza abilitati**  
    Se si imposta **Sì**, il client è abilitato per il servizio E9-1-1. Quando esegue la registrazione, un client tenta di acquisire una posizione dal servizio Informazioni percorso e include le informazioni sulla posizione come parte di una chiamata di emergenza.

<!-- end list -->

  - **Posizione obbligatoria**  
    Questa opzione viene utilizzata solo quando l'opzione **Servizi di emergenza abilitati** è impostata su **Sì**.
    
    È possibile configurare l'impostazione **Posizione obbligatoria** per definire il comportamento del client. Se si imposta il valore su **No**, all'utente non verrà richiesta una posizione. Se invece si imposta il valore su **Sì**, all'utente verrà richiesto di specificare una posizione, ma potrà ignorare la richiesta. Se si imposta il valore su **Dichiarazione di non responsabilità**, all'utente verrà richiesta una posizione e verrà visualizzata anche una dichiarazione di non responsabilità se tenta di ignorare la richiesta. In tutti i casi, l'utente potrà continuare a utilizzare il client.
    

    > [!NOTE]
    > Il testo della dichiarazione di non responsabilità non verrà visualizzato se l'utente immette manualmente una posizione prima di essere abilitato per il servizio E9-1-1. Gli aggiornamenti della dichiarazione di non responsabilità non verranno mostrati agli utenti che hanno già visualizzato la dichiarazione.



<!-- end list -->

  - **Dichiarazione di non responsabilità avanzata per i servizi di emergenza**  
    È possibile specificare quale dichiarazione di non responsabilità visualizzare se gli utenti ignorano la richiesta di una posizione. In Lync Server 2013 è possibile utilizzare criteri percorso per impostare dichiarazioni di non responsabilità diverse per impostazioni locali diverse o insiemi di utenti diversi.
    

    > [!NOTE]
    > Questa impostazione di criteri percorso si differenzia da Lync Server 2010, dove viene utilizzato il cmdlet <STRONG>Set-CsEnhancedEmergencyServiceDisclaimer</STRONG> per impostare una dichiarazione di non responsabilità globale per l'intera organizzazione. Se esiste già una dichiarazione di non responsabilità globale, specificarla nel criterio percorso. Lync Server 2013 infatti utilizza solo le dichiarazioni di non responsabilità specificate nei criteri percorso.



<!-- end list -->

  - **Stringa di composizione di emergenza**  
    Questa stringa di composizione (meno il segno "+" iniziale, ma con l'eventuale normalizzazione effettuata dal dial plan dell'utente di Lync) indica che una chiamata è di emergenza. Impostando **Stringa di composizione di emergenza**, il client include nella chiamata informazioni su posizione e richiamata.
    

    > [!NOTE]
    > Se nell'organizzazione non viene utilizzato un prefisso di accesso alla linea esterna, non è necessario creare una corrispondente regola di normalizzazione del dial plan per l'aggiunta di un segno "+" alla stringa del numero di emergenza prima dell'invio della chiamata al routing in uscita in un server del pool Lync. Il segno "+" iniziale verrà aggiunto automaticamente dal client Lync in base ai criteri percorso. Se tuttavia nel sito viene utilizzato un prefisso di accesso alla linea esterna, sarà necessario aggiungere una regola di normalizzazione ai criteri applicabili del dial plan per eliminare tale prefisso e aggiungere il segno "+". Se ad esempio per la posizione viene utilizzato il prefisso di accesso 9 e l'utente antepone questo prefisso al numero della chiamata di emergenza, il client utilizzerà i criteri del dial plan per normalizzare questa stringa aggiungendo il segno "+" al numero prima che il numero composto venga valutato dalle route nel profilo località del chiamante.



<!-- end list -->

  - **Maschere della stringa di composizione di emergenza**  
    Elenco di stringhe di composizione delimitate da punti e virgola convertito nella **Stringa di composizione di emergenza** specificata. È ad esempio possibile scegliere di aggiungere 112, che corrisponde al numero del servizio di emergenza per la maggior parte dei paesi europei. Un utente di Lync proveniente dall'Europa potrebbe non sapere che il numero di emergenza negli Stati Uniti è 911, ma potrà comporre 112 e ottenere lo stesso risultato. Come per la stringa di composizione di emergenza, non includere un segno "+" prima di ogni numero e se si utilizzano codici di accesso alla linea esterna, verificare che i criteri del dial plan dell'utente includano regole di normalizzazione per eliminare la cifra del codice di accesso.

<!-- end list -->

  - **Utilizzo PSTN**  
    Nome dell'utilizzo PSTN contenente i percorsi di routing che determinano il trunk SIP, il gateway PSTN o il gateway ELIN a cui verranno indirizzate le chiamate di emergenza.
    

    > [!NOTE]
    > È possibile assegnare un solo utilizzo a un criterio percorso. Questo utilizzo PSTN sovrascrive gli utilizzi PSTN assegnati ai criteri vocali dell'utente, ma si applica solo alle chiamate effettuate con la stringa di composizione di emergenza o con una delle relative maschere.



<!-- end list -->

  - **URI notifica**  
    È possibile specificare uno o più URI SIP del personale di sicurezza che riceverà una notifica tramite messaggistica istantanea quando viene effettuata una chiamata di emergenza. Sono supportati i gruppi di distribuzione.

<!-- end list -->

  - **URI conferenza**  
    È possibile specificare un numero DID (Direct Inward Dialing), in genere un numero del desk di sicurezza, da utilizzare per le conferenze quando viene effettuata una chiamata di emergenza.

<!-- end list -->

  - **Modalità conferenza**  
    È possibile specificare se l'URI conferenza verrà utilizzato per le conferenze in una chiamata di emergenza utilizzando una comunicazione unidirezionale o bidirezionale.

<!-- end list -->

  - **Intervallo di aggiornamento della posizione**  
    È possibile specificare l'intervallo di tempo (in ore) che deve intercorrere tra le richieste client di aggiornamento della posizione dal servizio Informazioni percorso. È possibile specificare un valore compreso tra 1 e 12. Il valore predefinito è 4.

