---
title: Ripristino dei dati di monitoraggio o archiviazione
TOCTitle: Ripristino dei dati di monitoraggio o archiviazione
ms:assetid: 60118526-13bb-4b03-803e-6ffae219d436
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Hh202175(v=OCS.15)
ms:contentKeyID: 52062168
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ripristino dei dati di monitoraggio o archiviazione

 

_**Ultima modifica dell'argomento:** 2013-02-18_

Il ripristino dei dati di monitoraggio e archiviazione non è necessario per rimettere in funzione Lync Server dopo un errore. Se tali dati sono cruciali per l'organizzazione, tuttavia, è possibile ripristinarli dopo aver ricreato il database.

La procedura seguente descrive come utilizzare SQL Server Management Studio per ripristinare i dati di archiviazione o monitoraggio.

## Per ripristinare i dati di monitoraggio o archiviazione da un file di backup

1.  Accedere al server da ripristinare come membro del gruppo Administrators nel computer locale o di un gruppo con diritti utente equivalenti.

2.  Aprire SQL Server Management Studio: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft SQL Server 2012** o **Microsoft SQL Server 2008 R2** e quindi fare clic su **SQL Server Management Studio**.

3.  In **Connetti al server** connettersi all'istanza di SQL Server specificando almeno il nome del server e le informazioni di autenticazione.

4.  In **Esplora oggetti** fare clic con il pulsante destro del mouse su **Database** e quindi scegliere **Ripristina database**.

5.  In **Selezione pagina** fare clic su **Generale** e quindi in **Database di destinazione** selezionare il nome del database come indicato di seguito:
    
      - Per un database di archiviazione selezionare **LcsLog**.
    
      - Per un database di registrazione dettagli chiamata selezionare **LcsCDR**.
    
      - Per un database QoE (Quality of Experience) selezionare **QoEMetrics**.

6.  Fare clic su **Periferica di origine**.

7.  In **Selezionare i set di backup da ripristinare** fare clic sul file di backup e quindi fare clic su **Ripristina**.

8.  In **Selezione pagina** fare clic su **Opzioni** verificare che il percorso del file di dati e il percorso del log si trovino nella cartella corretta e quindi fare clic su **OK**.

## Per assicurarsi che gli elenchi di controllo di accesso (ACL) siano corretti

1.  Espandere **Database**, espandere il database di archiviazione o di monitoraggio, espandere **Sicurezza** e quindi espandere **Utenti**.

2.  Verificare che il gruppo di dominio RTCComponentUniversalServices esista come utente.

3.  Se RTCComponentUniversalServices non esiste in **Utenti**, eseguire le operazioni seguenti:
    
    1.  Fare clic con il pulsante destro del mouse su **Utenti** e quindi scegliere **Nuovo utente**.
    
    2.  In **Nome account di accesso** digitare il nome del gruppo mancante, ovvero RTCComponentUniversalServices.
    
    3.  In **Appartenenza a ruoli del database** selezionare l'autorizzazione **ServerRole** e quindi fare clic su **OK**.
    

    > [!NOTE]
    > Non è necessario riavviare il servizio di archiviazione o di monitoraggio.


