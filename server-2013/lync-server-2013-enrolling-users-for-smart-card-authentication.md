---
title: Registrazione degli utenti per l'autenticazione con smart card
TOCTitle: Registrazione degli utenti per l'autenticazione con smart card
ms:assetid: a6445a83-a94b-423f-ba2a-12b5f84c5d75
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn308570(v=OCS.15)
ms:contentKeyID: 56269965
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Registrazione degli utenti per l'autenticazione con smart card

 

_**Ultima modifica dell'argomento:** 2013-07-03_

Esistono in genere due metodi per registrare gli utenti per l'autenticazione con smart card. Il metodo più semplice consiste nel chiedere agli utenti di registrarsi direttamente mediante Web, mentre il più complesso implica l'utilizzo di un agente di registrazione. In questo argomento viene illustrata l'autoregistrazione per i certificati smart card.

Per ulteriori informazioni sulla registrazione per conto di altri utenti come agente di registrazione, vedere Registrare certificati per conto di altri utenti [http://go.microsoft.com/fwlink/p/?LinkID=313367](http://go.microsoft.com/fwlink/p/?linkid=313367).

## Per registrare gli utenti per l'autenticazione con smart card

1.  Accedere alla workstation Windows 8 con le credenziali di un utente abilitato per Lync.

2.  Avviare Internet Explorer.

3.  Passare alla pagina **Registrazione Web Autorità di certificazione**, ad esempio https://MyCA.contoso.com/certsrv.
    

    > [!NOTE]
    > Se si utilizza Internet Explorer 10, potrebbe essere necessario visualizzare il sito Web in modalità di compatibilità.



4.  Nella pagina inizialeselezionare **Richiedi un certificato**.

5.  Quindi, selezionare **Richiesta avanzata di certificati**.

6.  Selezionare **Creare e inviare una richiesta a questa CA**.

7.  Selezionare **Utente con smart card** nella sezione **Modello di certificato** e completare la richiesta avanzata di certificati con i valori seguenti:
    
      - In **Opzioni chiave** confermare l'impostazione seguente:
        
          - Selezionare il pulsante di opzione **Crea nuovo set di chiavi**.
        
          - Per **CSP** selezionare **Microsoft Base Smart Card Crypto Provider**.
        
          - Per **Utilizzo chiave** selezionare **Scambio** (l'unica opzione disponibile).
        
          - Per **Dimensioni chiave** immettere **2048**.
        
          - Verificare che sia selezionata l'opzione **Nome del contenitore chiave automatico**.
        
          - Lasciare le altre caselle deselezionate.
    
      - In **Opzioni aggiuntive** confermare i valori seguenti:
        
          - Per **Formato richiesta** selezionare **CMC**.
        
          - Per **Algoritmo hash** selezionare **sha1**.
        
          - Per **Nome descrittivo** immettere **Certificato smart card**.

8.  Se si utilizza un lettore di smart card fisico, inserire la smart card nel dispositivo.

9.  Fare clic su **Invia** per inviare la richiesta di certificato.

10. Quando richiesto, immettere il PIN utilizzato per creare la smart card virtuale.
    

    > [!NOTE]
    > Il valore predefinito del PIN per la smart card virtuale è "12345678".



11. Dopo l'emissione del certificato, fare clic su **Installa questo certificato** per completare il processo di registrazione.
    

    > [!NOTE]
    > Se la richiesta di certificato non riesce e viene visualizzato il messaggio di errore "Il browser non supporta la generazione di richieste di certificati", esistono tre modi per risolvere il problema: 
    > <OL>
    > <LI>
    > <P>Abilitare Visualizzazione Compatibilità in Internet Explorer</P>
    > <LI>
    > <P>Abilitare l'opzione Attiva impostazioni Intranet in Internet Explorer</P>
    > <LI>
    > <P>Selezionare l'impostazione Ripristina livello predefinito per tutte le aree nella scheda Sicurezza del menu Opzioni Internet.</P></LI></OL>


