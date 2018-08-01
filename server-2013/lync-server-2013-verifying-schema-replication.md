---
title: 'Lync Server 2013: Verifica della replica dello schema'
TOCTitle: Verifica della replica dello schema
ms:assetid: ad01a7cf-aa79-4648-ba5a-a7a09172db36
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412822(v=OCS.15)
ms:contentKeyID: 49301642
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verifica della replica dello schema in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-29_

Prima di eseguire la preparazione della foresta, verificare manualmente che la partizione dello schema sia stata replicata.

## Per verificare manualmente la replica dello schema

1.  Accedere a un controller di dominio come membro del gruppo Enterprise Admins.

2.  Aprire ADSI Edit. A tale scopo, fare clic sul pulsante **Start** , scegliere **Strumenti di amministrazione** , quindi **ADSI Edit** .
    
    > [!TIP]  
    > In alternativa, è possibile eseguire <strong>adsiedit.msc</strong> dalla riga di comando.

3.  Nell'albero di Microsoft Management Console (MMC) fare clic su **ADSI Edit** se la voce non è già selezionata.

4.  Scegliere **Connetti a** dal menu **Azioni** .

5.  Nella finestra di dialogo **Impostazioni connessione** selezionare **Schema** in **Selezionare un contesto dei nomi noto** e quindi fare clic su **OK** .

6.  Nel contenitore Schema individuare la voce CN=ms-RTC-SIP-SchemaVersion. Se questo oggetto è presente e il valore dell'attributo **rangeUpper** è 1150 e il valore dell'attributo **rangeLower** è 3, lo schema è stato aggiornato e replicato correttamente. Se l'oggetto non è presente o i valori degli attributi **rangeUpper** e **rangeLower** sono diversi da quelli specificati, lo schema non è stato modificato o replicato.

## Vedere anche

#### Attività

[Esecuzione della preparazione dello schema in Lync Server 2013](lync-server-2013-running-schema-preparation.md)  

#### Concetti

[Preparazione dello schema di Active Directory in Lync Server 2013](lync-server-2013-preparing-the-active-directory-schema.md)

