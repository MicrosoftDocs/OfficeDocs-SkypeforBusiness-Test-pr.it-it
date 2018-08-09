---
title: "#VALUE!"
TOCTitle: "#VALUE!"
ms:assetid: 23b192d2-93ec-42a8-b175-b6ed502a2c35
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ687993(v=OCS.15)
ms:contentKeyID: 49887478
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eseguire la migrazione delle impostazioni dell'applicazione Parcheggio di chiamata

 

_**Ultima modifica dell'argomento:** 2012-10-19_

La migrazione dell'applicazione Parcheggio chiamata da Lync Server 2010 a Lync Server 2013 include il provisioning del pool di Lync Server 2013 con eventuali file di musica di attesa personalizzati caricati in Lync Server 2010, il ripristino delle impostazioni di livello di servizio e il reindirizzamento di tutti i codici orbit di Parcheggio chiamata al pool di Lync Server 2013. Se i file di musica di attesa personalizzati sono stati configurati nel pool di Lync Server 2010, devono essere copiati nel nuovo pool di Lync Server 2013. È inoltre consigliabile eseguire il backup dei file di musica di attesa personalizzati di Parcheggio chiamata da Lync Server 2010 in un'altra destinazione per conservare una copia di backup separata di qualsiasi file di musica di attesa personalizzato caricato per Parcheggio chiamata. I file di musica di attesa personalizzati per l'applicazione Parcheggio chiamata sono archiviati nell'archivio file del pool. Per copiare i file audio da un archivio file del pool di Lync Server 2010 in un archivio file di Lync Server 2013, utilizzare il comando **Xcopy** con i parametri seguenti:

```
Xcopy <Source: Lync Server 2010 Pool CPS File Store Path> <Destination: Lync Server 2013 Pool CPS File Store Path>
```
```
Example usage:  Xcopy "<Lync Server 2010 File Store Path>\OcsFileStore\coX-ApplicationServer-X\AppServerFiles\CPS\"  "<Lync Server 2013 File Store Path>\OcsFileStore\coX-ApplicationServer-X\AppServerFiles\CPS\" 
```

Quando tutti i file audio personalizzati sono stati copiati nell'archivio file di Lync Server 2013, è necessario configurare le impostazioni dell'applicazione Parcheggio chiamata del pool di Lync Server 2013 e riassegnare al pool di Lync Server 2013 gli intervalli di codici orbit di Parcheggio chiamata associati al pool di Lync Server 2010.

Le impostazioni di Parcheggio chiamata includono la soglia di timeout di pick-up, l'abilitazione o la disabilitazione della musica di attesa, il numero massimo di tentativi di pick-up chiamata e la richiesta di timeout. È necessario gestire le impostazioni dell'applicazione Parcheggio chiamata utilizzando Lync Server Management Shell per eseguire il cmdlet **Set-CsCpsConfiguration**. Non è possibile gestire le impostazioni dell'applicazione Parcheggio chiamata tramite il Pannello di controllo di Lync Server.

**Riconfigurare le impostazioni del servizio Parcheggio chiamata**

1.  In Lync Server 2013 Front End Server aprire Lync Server Management Shell.

2.  Nella riga di comando digitare quanto segue:
    

    > [!NOTE]
    > Se le impostazioni dell'applicazione Parcheggio chiamata di Lync Server 2013 sono identiche alle impostazioni legacy di Lync Server 2010, è possibile saltare questo passaggio. Se tali impostazioni sono diverse per gli ambienti Lync Server 2013 e Lync Server 2010, utilizzare il cmdlet di seguito come modello per aggiornare le modifiche.

    
        Set-CsCpsConfiguration -Identity "<LS2013 Call Park Service ID>" -CallPickupTimeoutThreshold "<LS2010 CPS TimeSpan>" -EnableMusicOnHold "<LS2010 CPS value>" -MaxCallPickupAttempts "<LS2010 CPS pickup attempts>" -OnTimeoutURI "<LS2010 CPS timeout URI>"

Per riassegnare tutti gli intervalli di codici orbit di Parcheggio chiamata dal pool di Lync Server 2010 al pool di Lync Server 2013, è possibile usare il Pannello di controllo di Lync Server o Lync Server Management Shell.

**Riassegnare tutti gli intervalli di codici orbit di Parcheggio chiamata utilizzando il Pannello di controllo di Lync Server**

1.  Aprire il Pannello di controllo di Lync Server.

2.  Nel riquadro sinistro, selezionare **Funzionalità vocali**.

3.  Selezionare la scheda **Parcheggio chiamata**.

4.  Per ogni intervallo di codici orbit di Parcheggio chiamata assegnato a un pool di Lync Server 2010, modificare l'impostazione **FQDN del server di destinazione** e selezionare il pool di Lync Server 2013 che elaborerà le richieste di Parcheggio chiamata.

5.  Selezionare **Commit** per salvare le modifiche.

**Riassegnare tutti gli intervalli di codici orbit di Parcheggio chiamata utilizzando Lync Server Management Shell**

1.  Aprire il Lync Server Management Shell.

2.  Nella riga di comando digitare quanto segue:
    
        Get-CsCallParkOrbit
    
    Questo cmdlet elenca tutti gli intervalli di codici orbit di Parcheggio chiamata nella distribuzione. Tutti i codici orbit di Parcheggio chiamata con i parametri **CallParkServiceId** e **CallParkServerFqdn** impostati come il pool di Lync Server 2010 devono essere riassegnati.
    
    Per riassegnare gli intervalli di codici orbit di Parcheggio chiamata di Lync Server 2010 al pool di Lync Server 2013, digitare quanto segue nella riga di comando:
    
        Set-CsCallParkOrbit -Identity "<Call Park Orbit Identity>" -CallParkService "service:ApplicationServer:<Lync Server 2013 Pool FQDN>"

Dopo la riassegnazione di tutti gli intervalli di codici orbit di Parcheggio chiamata al pool di Lync Server 2013, il processo di migrazione per l'applicazione Parcheggio chiamata è completato e il pool di Lync Server 2013 gestirà tutte le richieste future di Parcheggio chiamata.

