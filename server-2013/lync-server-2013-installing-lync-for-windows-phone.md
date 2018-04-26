---
title: Installazione di Lync per Windows Phone
TOCTitle: Installazione di Lync per Windows Phone
ms:assetid: bf502546-ff69-489f-a92e-a78b58803d53
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh690996(v=OCS.15)
ms:contentKeyID: 52062258
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Installazione di Lync per Windows Phone

 

_**Ultima modifica dell'argomento:** 2014-02-03_

Lync 2013 per Windows Phone è un'applicazione installabile dagli utenti, disponibile nel sito Marketplace di Windows Phone.

## Installazione di Lync per Windows Mobile

È possibile dare istruzioni agli utenti di installare Lync 2013 per Windows Phone nei dispositivi indirizzandoli al sito Marketplace di Windows Phone all'indirizzo <http://go.microsoft.com/fwlink/?linkid=231901>.

## Se si usa un record SRV DNS per pubblicare Servizi Web Exchange

Per consentire l'integrazione di Exchange per i client Lync, alcune organizzazioni pubblicano l'URL dei Servizi Web Exchange mediante un record SRV DNS. Nel documento "Informazioni e risoluzione dei problemi relativi all'integrazione di Exchange", disponibile nell'Area download Microsoft all'indirizzo [http://go.microsoft.com/fwlink/?LinkID=391095](http://go.microsoft.com/fwlink/?linkid=391095), vengono descritti gli scenari in cui tale operazione potrebbe essere necessaria. In questo scenario, tuttavia, l'integrazione di Exchange per utenti di Windows Phone non funzionerà perché la piattaforma Windows Phone non supporta le ricerche SRV. Sarà necessario comunicare agli utenti di Windows Phone di specificare l'URL di Servizi Web Exchange anziché consentire al telefono di rilevare automaticamente il server.

Comunicare agli utenti di configurare le impostazioni di Lync nei propri Windows Phone nel modo seguente:

1.  In Windows Phone selezionare la schermata **Exchange** nelle impostazioni di Lync.

2.  Impostare **Rilevamento autom.** su **No**.

3.  Toccare il campo vuoto e immettere il nome di dominio completo (FQDN) o l'URL di Servizi Web Exchange.
    

    > [!NOTE]
    > È possibile specificare il nome di dominio completo (FQDN) o l'URL completo del server di Servizi Web Exchange. Se si specifica il nome di dominio completo, il protocollo (https://) e il percorso di Servizi Web Exchange (/ews/exchange.asmx) verranno aggiunti automaticamente. Se si usa un percorso diverso per Servizi Web, è possibile specificare l'URL completo.



4.  Chiudere la schermata.

## Verifica dell'installazione del client mobile

Dopo avere configurato il client e avere eseguito l'accesso, utilizzare i test seguenti per verificare il corretto funzionamento dell'installazione di Lync 2013 nel dispositivo mobile.

**Cercare un contatto nella directory aziendale**

1.  Nell'elenco Contatti toccare **Cerca** in basso.

2.  Cercare un contatto presente solo nell'elenco indirizzi globale.

3.  Verificare che il nome del contatto sia incluso nei risultati della ricerca.

**Eseguire il test delle funzionalità di messaggistica istantanea e presenza**

1.  Toccare un contatto nell'elenco Contatti.

2.  Nella scheda del contatto toccare l'icona **Messaggistica istantanea**.

3.  Verificare che venga visualizzata una finestra di messaggistica istantanea e che sia possibile digitare e inviare un messaggio istantaneo.

**Verificare le funzionalità di conferenza telefonica con accesso esterno**

1.  In Outlook, pianificare una riunione di Lync.

2.  Aprire l'invito alla riunione nel dispositivo mobile.

3.  Fare clic sul collegamento nell'invito per partecipare alla riunione.

4.  Rispondere alla chiamata dal servizio di conferenza e verificare di essere connessi all'audio della riunione.

**Verificare le notifiche push**

1.  Nel dispositivo mobile dell'utente A accedere a Lync con l'account dell'utente A.

2.  Aprire un'altra applicazione nel dispositivo mobile.

3.  In un altro client, accedere a Lync con l'account dell'utente B.

4.  Inviare un messaggio istantaneo dall'utente B all'utente A.

5.  Verificare che la notifica di messaggio istantaneo venga visualizzata nel dispositivo mobile dell'utente A.

