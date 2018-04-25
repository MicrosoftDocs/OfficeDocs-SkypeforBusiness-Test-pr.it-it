---
title: Configurazione della CA globale (enterprise) per l'autenticazione con smart card
TOCTitle: Configurazione della CA globale (enterprise) per l'autenticazione con smart card
ms:assetid: c24e0891-e108-4cb6-9902-c6a4c8e68455
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn308571(v=OCS.15)
ms:contentKeyID: 56269976
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione della CA globale (enterprise) per l'autenticazione con smart card

 

_**Ultima modifica dell'argomento:** 2013-07-03_

La sezione seguente illustra come configurare una CA globale (enterprise) radice per il supporto dell'autenticazione con smart card. Per informazioni su come installare un'autorità di certificazione globale (enterprise) radice, vedere l'argomento corrispondente all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkID=313364](http://go.microsoft.com/fwlink/p/?linkid=313364).

## Configurazione di un'autorità di certificazione globale (enterprise) radice per il supporto dell'autenticazione con smart card

I passaggi seguenti illustrano come configurare una CA radice dell'organizzazione per il supporto dell'autenticazione con smart card:

1.  Accedere al computer della CA globale (enterprise) utilizzando un account di amministratore del dominio.

2.  Avviare il gestore di sistema e verificare che il ruolo di Registrazione Web Autorità di certificazione sia installato.

3.  Dal menu **Strumenti di amministrazione** aprire la console di gestione **Autorità di certificazione**.

4.  Nel riquadro di spostamento espandere **Autorità di certificazione**.

5.  Fare clic con il pulsante destro del mouse su **Modelli di certificato**, scegliere **Nuovo** e quindi selezionare **Modello di certificato da rilasciare**.

6.  Selezionare **Enrollment Agent**, **Utente con smart card** e **Accesso con smart card**.

7.  Fare clic su **OK**.

8.  Fare clic con il pulsante destro del mouse su **Modelli di certificato**.

9.  Selezionare **Gestisci**.

10. Aprire le proprietà del modello Utente con smart card.

11. Fare clic sulla scheda **Sicurezza**.

12. Modificare le autorizzazioni come segue:
    
      - Aggiungere singoli account utente Active Directory con autorizzazioni Lettura/Registrazione (Consenti), oppure
    
      - Aggiungere un gruppo di sicurezza contenente utenti smart card con autorizzazioni Lettura/Registrazione (Consenti), oppure
    
      - Aggiungere il gruppo Domain Users con autorizzazioni Lettura/Registrazione (Consenti)

