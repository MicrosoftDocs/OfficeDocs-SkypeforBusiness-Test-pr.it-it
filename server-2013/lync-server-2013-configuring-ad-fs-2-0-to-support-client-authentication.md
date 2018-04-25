---
title: Configurazione di ADFS 2.0 per il supporto dell'autenticazione client
TOCTitle: Configurazione di ADFS 2.0 per il supporto dell'autenticazione client
ms:assetid: 4d93d400-ccaa-4da8-a71b-d05d7ba79d93
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn308565(v=OCS.15)
ms:contentKeyID: 56269904
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione di ADFS 2.0 per il supporto dell'autenticazione client

 

_**Ultima modifica dell'argomento:** 2013-07-03_

Per garantire il supporto dell'autenticazione tramite smart card in ADFS 2.0, è possibile configurare due tipi di autenticazione:

  - Autenticazione basata su moduli

  - Autenticazione client TLS (Transport Layer Security)

Tramite l'autenticazione basata su moduli è possibile sviluppare una pagina Web che consenta agli utenti di effettuare l'autenticazione tramite il proprio nome utente e la propria password oppure mediante una smart card con relativo PIN. In questo argomento viene descritto come implementare l'autenticazione client TLS con ADFS 2.0. Per ulteriori informazioni sui tipi di autenticazione di ADFS 2, vedere l'articolo sulla modifica del tipo di autenticazione locale in ADFS 2.0 disponibile all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=313384](http://go.microsoft.com/fwlink/p/?linkid=313384).


**Per configurare ADFS 2.0 per il supporto dell'autenticazione client**

1.  Accedere al computer ADFS 2.0 utilizzando un account di amministratore del dominio.

2.  Avviare Esplora risorse.

3.  Passare a C:\\inetpub\\adfs\\ls

4.  Eseguire una copia di backup del file web.config esistente.

5.  Aprire il file web.config esistente nel Blocco note.

6.  Nella barra dei menu selezionare **Modifica** e quindi **Trova**.

7.  Cercare **\<localAuthenticationTypes\>**.
    
    Si noti che vengono elencati quattro tipi di autenticazione, uno per riga.

8.  Spostare la riga contenente il tipo di autenticazione TLSClient in cima all'elenco nella sezione corrente.

9.  Salvare e chiudere il file web.config.

10. Avviare un prompt dei comandi con privilegi elevati.

11. Riavviare IIS eseguendo il comando seguente:
    
        IISReset /Restart /NoForce

