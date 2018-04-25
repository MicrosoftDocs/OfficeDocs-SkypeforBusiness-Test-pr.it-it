---
title: Errore di Import-Module causato dal criterio di esecuzione di Windows PowerShell
TOCTitle: Errore di Import-Module causato dal criterio di esecuzione di Windows PowerShell
ms:assetid: 4bc093ca-fd30-44c9-a0a3-16f78698df2b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362786(v=OCS.15)
ms:contentKeyID: 56269903
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Errore di Import-Module causato dal criterio di esecuzione di Windows PowerShell

 

_**Ultima modifica dell'argomento:** 2015-06-22_

Il criterio di esecuzione di Windows PowerShell consente di determinare quali file di configurazione possono essere caricati nella console di Windows PowerShell e quali script possono essere eseguiti da un'utente da tale console. Come minimo, il modulo connettore per Skype for Business online non può essere importato a meno che il criterio di esecuzione non sia stato impostato su RemoteSigned. In caso contrario, verrà visualizzato il seguente messaggio di errore quando si tenta di importare il modulo:

    Import-Module: Impossibile caricare il file C:\Programmi\Common Files\Microsoft Lync Server 2013\Modules\LyncOnlineConnector\LyncOnlineConnectorStartup.psm1. L'esecuzione di script è disattivata nel sistema in uso. Per ulteriori informazioni, vedere about_Execution_Policies  all'indirizzo http://go.microsoft.com/fwlink/?LinkID=135170.

Per risolvere il problema, avviare Windows PowerShell come amministratore ed eseguire il comando seguente:

    Set-ExecutionPolicy RemoteSigned

Per informazioni dettagliate sul criterio di esecuzione, vedere l'argomento all'indirizzo [http://go.microsoft.com/fwlink/?LinkID=135170](http://go.microsoft.com/fwlink/?linkid=135170).

## Vedere anche

#### Concetti

[Diagnosi e risoluzione dei problemi di connessione di Lync Online](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

