---
title: Creazione o modifica di criteri percorso
TOCTitle: Creazione o modifica di criteri percorso
ms:assetid: 10338418-4da4-42df-b231-f52098c08dae
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ687971(v=OCS.15)
ms:contentKeyID: 49887446
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Creazione o modifica di criteri percorso

 

_**Ultima modifica dell'argomento:** 2012-11-01_

In Lync Server 2013 è possibile utilizzare il criterio percorso per applicare impostazioni relative alla funzionalità per chiamate di emergenza Enhanced 9-1-1 (E9-1-1) e impostazioni relative alla posizione per utenti o contatti. Determina infatti se un utente è abilitato per i servizi di emergenza avanzati e, in caso affermativo, qual è il comportamento di una chiamata di emergenza. Ad esempio, è possibile utilizzare il criterio percorso per definire i numeri che rappresentano una chiamata di emergenza, per specificare se inviare o meno una notifica all'ufficio di sicurezza aziendale e per impostare la modalità di instradamento della chiamata.

I criteri percorso possono essere configurati nel gruppo **Configurazione di rete** del Pannello di controllo di Lync Server 2013. Dal Pannello di controllo di Lync Server è possibile visualizzare, creare, modificare o eliminare criteri percorso. Utilizzare le procedure descritte in questa sezione per creare o modificare un criterio percorso. Per informazioni dettagliate sull'eliminazione di criteri percorso, vedere [Eliminazione di criteri percorso](lync-server-2013-deleting-a-location-policy.md).

In Lync Server 2013 è possibile eseguire l'override della quantità di tempo predefinita tra le richieste client di aggiornamento di un percorso dal servizio Informazioni percorso. Il valore predefinito è 4 ore. Per ignorare il valore predefinito, utilizzare il cmdlet **Set-CsLocationPolicy** con il parametro LocationRefreshInterval.

## Per creare un nuovo criterio percorso in Pannello di controllo di Lync Server

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Nella barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Criteri percorso**.

4.  Nella pagina **Criteri percorso** fare clic su **Nuovo** e quindi selezionare il tipo di criterio che si desidera creare:
    
      - Per creare un criterio sito, fare clic su **Criteri sito**. In **Seleziona un sito** selezionare il sito a cui si desidera applicare il criterio e fare clic su **OK**. Nella pagina **Crea nuovi criteri percorso** il campo **Ambito** conterrà il valore **Sito**, mentre il campo **Nome** conterrà il nome del sito selezionato. Tali campi non possono essere modificati. Un criterio sito viene infatti applicato automaticamente a tutti gli utenti del sito specificato e ha la priorità sul criterio globale valido per tali utenti.
    
      - Per creare un criterio utente, fare clic su **Criteri utente**. Nella pagina **Crea nuovi criteri percorso** il campo **Ambito** conterrà il valore **Utente**. Tale valore non può essere modificato. Nel campo **Nome** digitare il nome che si desidera assegnare al criterio. Un criterio utente non viene applicato automaticamente a qualsiasi utente. Dopo avere creato tale criterio, è necessario assegnarlo manualmente agli utenti o ai siti di rete a cui si desidera applicarlo.

5.  Completare i campi restanti come indicato di seguito:
    
      - **Abilita servizi di emergenza avanzati**   Selezionare questa casella di controllo per abilitare gli utenti associati a questo criterio per il servizio E9-1-1. Quando i servizi per le chiamate di emergenza sono abilitati, i client Lync Server recuperano le informazioni relative alla posizione al momento della registrazione e includono tali informazioni quando viene effettuata una chiamata di emergenza.
    
      - **Percorso**   Specificare uno dei valori seguenti:
        
          - **Richiesto**   All'utente verrà richiesta l'immissione delle informazioni sulla posizione quando il client si registra in una nuova posizione. L'utente può ignorare la richiesta e non immettere alcuna informazione. Se le informazioni vengono immesse, alla chiamata di emergenza effettuata risponderà innanzitutto il provider dei servizi di emergenza per verificare la posizione prima dell'instradamento al centro di raccolta delle chiamate di emergenza (PSAP, Public Safety Answering Point).
        
          - **Non richiesto**   All'utente non verrà richiesto di immettere la posizione. Quando viene effettuata una chiamata senza informazioni sulla posizione, il provider dei servizi di emergenza risponderà alla chiamata e richiederà la posizione.
        
          - **Dichiarazione di non responsabilità**   Questa opzione è analoga all'opzione **Richiesto**, con la differenza che l'utente non può ignorare la richiesta senza immettere le informazioni relative alla posizione. L'utente può comunque effettuare una chiamata di emergenza, ma non è possibile effettuare altre chiamate senza immettere le informazioni. Viene inoltre visualizzato il testo della dichiarazione di non responsabilità per comunicare all'utente le conseguenze derivanti dal rifiuto di immettere le informazioni sulla posizione. Per impostare il testo della dichiarazione di non responsabilità, è necessario utilizzare Lync Server Management Shell per eseguire il cmdlet **Set-CsLocationPolicy** o il cmdlet **New-CsLocationPolicy** con il parametro EnhancedEmergencyServiceDisclaimer. Per informazioni dettagliate, vedere [Set-CsLocationPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Set-CsLocationPolicy) o [New-CsLocationPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/New-CsLocationPolicy) nella documentazione di Lync Server Management Shell.
            

            > [!NOTE]
            > In Lync Server 2013 è possibile utilizzare i criteri percorso per impostare diverse dichiarazioni di non responsabilità per impostazioni locali o set di utenti diversi, mentre in Lync Server 2010 è possibile solo specificare una dichiarazione di non responsabilità globale per l'intera organizzazione.

    
      - **Utilizza percorso solo per i servizi di emergenza**   Le informazioni relative alla posizione possono essere utilizzate dal client Lync per diversi motivi, ad esempio per segnalare agli altri membri del team la posizione corrente dell'utente. Selezionare questa casella di controllo per assicurarsi che le informazioni sulla posizione siano disponibili esclusivamente per l'utilizzo con una chiamata di emergenza.
    
      - **Utilizzo PSTN**   L'utilizzo PSTN (Public Switched Telephone Network) che verrà impiegato per determinare la route vocale utilizzata per instradare le chiamate di emergenza dai client che utilizzano questo profilo. La route associata a tale utilizzo deve puntare a un trunk SIP dedicato alle chiamate di emergenza o a un gateway ELIN (Emergency Location Identification Number) che instrada le chiamate di emergenza al punto di raccolta PSAP più vicino.
    
      - **Numero di composizione di emergenza**   Il numero che viene composto per chiamare i servizi di emergenza. Negli Stati Uniti il numero è 911. La stringa deve essere costituita da cifre comprese tra 0 e 9 e avere una lunghezza massima di 10 cifre.
    
      - **Maschera di composizione di emergenza**   Un numero che si desidera venga convertito nel valore del numero di composizione di emergenza quando viene composto. Ad esempio, se si immette 212 in questo campo mentre nel campo del numero di composizione di emergenza il valore è 911, quando un utente compone 212, la chiamata viene comunque effettuata al 911. In questo modo viene consentita la composizione di numeri di emergenza alternativi per raggiungere comunque i servizi di emergenza (ad esempio, se una persona proveniente da un altro paese con un diverso numero di emergenza tenta di comporre il numero di quel paese anziché il numero del paese in cui si trova attualmente). È possibile definire più maschere di composizione del numero di emergenza separando i valori con un punto e virgola, ad esempio 212;414. La lunghezza massima della stringa è 100 caratteri. Ogni carattere deve essere una cifra compresa tra 0 e 9.
        
        > [!important]  
        > Accertarsi che il valore specificato come maschera di composizione non corrisponda a un numero dell'intervallo di codici orbit del parcheggio di chiamata. L'instradamento del parcheggio di chiamata avrà infatti la precedenza sulla conversione delle stringhe di composizione per le chiamate di emergenza. Per visualizzare gli intervalli di codici orbit del parcheggio di chiamata esistenti, fare clic su <strong>Funzionalità vocali</strong> nella barra di spostamento sinistra e quindi fare clic su <strong>Parcheggio di chiamata</strong>. Per informazioni dettagliate, vedere <a href="lync-server-2013-configure-phone-number-extensions-for-parking-calls.md">Configurare le estensioni del numeri di telefono per il parcheggio chiamata</a>.    
      - **URI notifica**   Uno o più URI (Uniform Resource Identifier) SIP a cui inviare una notifica quando viene effettuata una chiamata di emergenza. Ad esempio, l'ufficio che si occupa della sicurezza aziendale potrebbe ricevere una notifica tramite messaggio istantaneo ogni volta che viene effettuata una chiamata di emergenza. Se la posizione del chiamante è disponibile, verrà inclusa nella notifica. Per includere più URI SIP, utilizzare un elenco separato da virgole, ad esempio "sip:security@litwareinc.com","sip:kmyer@litwareinc.com". Le liste di distribuzione non sono supportate. La stringa deve avere una lunghezza compresa tra 1 e 256 caratteri e deve iniziare con il prefisso "sip:". Prima di fare clic nel campo URI notifica, viene visualizzato un esempio.
    
      - **URI conferenza**   L'URI SIP, in questo caso il numero di telefono, di terze persone che parteciperanno alle chiamate di emergenza effettuate. Ad esempio, l'ufficio che si occupa della sicurezza aziendale potrebbe ricevere una chiamata quando viene effettuata una chiamata di emergenza e ascoltare o partecipare alla chiamata (in base al valore specificato nel campo **Modalità conferenza**). La stringa deve avere una lunghezza compresa tra 1 e 256 caratteri e deve iniziare con il prefisso sip:. Finché non si fa clic in questo campo, viene visualizzato un esempio.
    
      - **Modalità conferenza**   Se si specifica un valore nel campo **URI conferenza**, l'impostazione del campo **Modalità conferenza** determinerà se terze persone possono partecipare alla chiamata o solo ascoltare. Selezionare una delle opzioni seguenti:
        
          - **Unidirezionale**   Terze persone possono solo ascoltare la conversazione tra il chiamante e l'operatore del centro PSAP.
        
          - **Bidirezionale**   Terze persone possono ascoltare e partecipare alla chiamata tra il chiamante e l'operatore del centro PSAP.

6.  Fare clic su **Commit**.
    
    > [!important]  
    > Quando si crea un criterio utente, inizialmente tale criterio non viene applicato ad alcun utente o sito di rete. Per applicare il criterio a un utente, fare clic su <strong>Utenti</strong> sulla barra di spostamento sinistra, individuare l'utente a cui applicare il criterio, scegliere <strong>Mostra dettagli</strong> dal menu <strong>Modifica</strong> e nella pagina <strong>Modifica utente di Lync Server</strong> selezionare il nuovo criterio percorso nell'elenco a discesa <strong>Criteri percorso</strong>, quindi fare clic su <strong>Commit</strong>.<br />    Per applicare il criterio a un sito di rete, fare clic su <strong>Configurazione di rete</strong> sulla barra di spostamento sinistra, fare clic su <strong>Sito</strong>, individuare il sito di rete a cui applicare il criterio, scegliere <strong>Mostra dettagli</strong> dal menu <strong>Modifica</strong> e in <strong>Modifica sito</strong> selezionare il nuovo criterio percorso nell'elenco a discesa <strong>Criteri percorso</strong>, quindi fare clic su <strong>Commit</strong>.

## Per modificare un criterio percorso in Pannello di controllo di Lync Server

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Configurazione di rete** e quindi su **Criteri percorso**.

4.  Nella pagina **Criteri percorso** selezionare il criterio percorso da modificare.

5.  Scegliere **Mostra dettagli** dal menu **Modifica**.

6.  Nella pagina **Modifica criteri percorso** modificare i campi in base alle proprie esigenze. Per informazioni dettagliate, vedere il passaggio 5 nelle procedure "Per creare un nuovo criterio percorso" più indietro in questo argomento.

7.  Fare clic su **Commit**.

## Vedere anche

#### Attività

[Eliminazione di criteri percorso](lync-server-2013-deleting-a-location-policy.md)  

#### Concetti

[Definizione di criteri percorso per Lync Server 2013](lync-server-2013-defining-the-location-policy.md)  

#### Ulteriori risorse

[Configurare le estensioni del numeri di telefono per il parcheggio chiamata](lync-server-2013-configure-phone-number-extensions-for-parking-calls.md)

