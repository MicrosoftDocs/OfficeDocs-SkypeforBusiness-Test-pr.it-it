---
title: Aggiornamento dalla versione di valutazione di Lync Server 2013
TOCTitle: Aggiornamento dalla versione di valutazione di Lync Server 2013
ms:assetid: 62a88180-4289-4a2a-9cb9-1b9899344a63
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg521005(v=OCS.15)
ms:contentKeyID: 49300772
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Aggiornamento dalla versione di valutazione di Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-06-20_

Se è stata installata la versione di valutazione di Microsoft Lync Server 2013, sarà successivamente necessario aggiornare tale installazione mediante una copia con licenza del software, in quanto la versione di valutazione scade 180 giorni dopo l'installazione. Non sarà tuttavia necessario disinstallare completamente la versione di valutazione e quindi installare la versione con licenza. Dopo aver ottenuto un codice di licenza valido, è infatti possibile aggiornare la versione di valutazione di Lync Server 2013 eseguendo la procedura descritta di seguito in ogni computer che opera come Front End Server, Director o server perimetrale di Lync Server. Si noti che non è necessario aggiornare i computer che svolgono altri ruoli del server, ad esempio Monitoring Server o server di archiviazione.

## Aggiornamento dalla versione di valutazione di Microsoft Lync Server 2013

Per aggiornare un computer dalla versione di valutazione di Lync Server 2013 alla versione con licenza del software:

**Aggiornamento dalla versione di valutazione di Microsoft Lync Server 2013**

1.  Accedere al computer come amministratore locale.

2.  Fare clic sul pulsante **Start** , scegliere **Tutti i programmi** , **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  In Lync Server Management Shell digitare il comando seguente e quindi premere INVIO:
    
        msiexec.exe /fvomus server.msi EVALTOFULL=1 /qb
    
    Si noti che potrebbe essere necessario specificare il percorso completo del file server.msi. Questo file è disponibile nella cartella Setup dei file di installazione nei supporti per i contratti multilicenza di Lync Server.

4.  Al termine dell'esecuzione del programma di installazione, digitare il comando seguente al prompt dei comandi e quindi premere INVIO:
    
        Enable-CsComputer

5.  Ripetere la procedura in qualsiasi altro Front End Server, Director o server perimetrale che esegue una copia di valutazione di Lync Server. È consigliabile eseguire questa procedura anche in qualsiasi server di succursale distribuito tramite i file di installazione nei supporti di Lync Server.

Se non si è certi che la versione di Lync Server in esecuzione in un determinato computer sia la versione di valutazione, è possibile verificarlo eseguendo il comando seguente da Lync Server Management Shell:

    Get-CsServerVersion

Il cmdlet [Get-CsServerVersion](get-csserverversion.md) analizzerà il computer locale e fornirà una delle indicazioni seguenti:

  - Il codice del contratto multilicenza di Lync Server è installato nel computer e ciò indica che non è necessario l'aggiornamento.

  - Nel computer è installato il codice della licenza di valutazione di Lync Server e ciò indica che il computer deve essere installato.

  - Non è necessario alcun codice di contratto multilicenza nel computer. L'aggiornamento dalla versione di valutazione a quella con licenza è necessaria solo nei Front End Server, nei server Director e nei server perimetrali.

