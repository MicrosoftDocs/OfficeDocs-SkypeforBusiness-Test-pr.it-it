---
title: È stato superato il numero massimo di shell simultanee per questo utente
TOCTitle: È stato superato il numero massimo di shell simultanee per questo utente
ms:assetid: b309efe8-a214-41ea-a345-93e6a36e0cb1
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362837(v=OCS.15)
ms:contentKeyID: 56269971
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# È stato superato il numero massimo di shell simultanee per questo utente

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Ogni amministratore può eseguire fino a tre connessioni remote simultanee a Skype for Business online. Se sono attive tre connessioni remote a Windows PowerShell, qualsiasi tentativo di effettuare una quarta connessione simultanea non riuscirà, generando il messaggio di errore seguente:

    New-PSSession : [admin.vdomain.com] Connessione al server remoto admin.vdomain.com non riuscita con il seguente messaggio di errore: Servizio WS-Management: impossibile elaborare la richiesta. È stato superato il numero massimo di shell che è consentito aprire contemporaneamente per l'utente. Chiudere le shell esistenti oppure aumentare la quota per l'utente. Per ulteriori informazioni, vedere l'argomento della Guida about_Remote_Troubleshooting.

L'unico modo per risolvere il problema consiste nel chiudere almeno una delle connessioni precedenti. Dopo aver concluso una sessione di Skype for Business online, è consigliabile usare il cmdlet **Remove-PSSession** per terminare la sessione. Questa soluzione aiuta a prevenire il problema.

## Vedere anche

#### Concetti

[Diagnosi e risoluzione dei problemi di connessione di Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

