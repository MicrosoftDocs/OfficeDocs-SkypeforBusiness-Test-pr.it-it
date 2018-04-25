---
title: È stato superato il numero massimo di shell simultanee per questo tenant
TOCTitle: È stato superato il numero massimo di shell simultanee per questo tenant
ms:assetid: a4c91ffa-fdcc-414c-b941-a0d36c906825
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362832(v=OCS.15)
ms:contentKeyID: 56269948
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# È stato superato il numero massimo di shell simultanee per questo tenant

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Sebbene ogni amministratore possa stabilire fino a tre connessioni simultanee a un tenant di Skype for Business online, un tenant non può avere più di nove connessioni simultanee. Supponiamo ad esempio che tre amministratori abbiano tre sessioni aperte ciascuno. Se un quarto amministratore cerca di stabilire una connessione, portando a 10 le connessioni simultanee, il tentativo non riuscirà e genererà il messaggio di errore seguente:

    New-PSSession : [admin.vdomain.com] Connessione al server remoto admin.vdomain.com non riuscita con il seguente messaggio di errore: Servizio WS-Management: impossibile elaborare la richiesta. È stato superato il numero massimo di shell simultanee per questo tenant. Chiudere le shell esistenti oppure aumentare la quota per il tenant. Per altre informazioni, vedere l'argomento della Guida about_Remote_Troubleshooting.

L'unico modo per risolvere il problema consiste nel chiudere almeno una delle connessioni precedenti. Dopo aver concluso una sessione di Skype for Business online, è consigliabile usare il cmdlet **Remove-PSSession** per terminare la sessione. Questa soluzione aiuta a prevenire il problema.

## Vedere anche

#### Concetti

[Guida di riferimento rapido: Uso di Windows PowerShell per eseguire attività comuni di gestione di Lync Online](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

