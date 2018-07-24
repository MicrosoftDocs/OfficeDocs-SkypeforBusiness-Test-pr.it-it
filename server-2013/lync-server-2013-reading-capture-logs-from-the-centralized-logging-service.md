---
title: Lettura dei log di acquisizione dal servizio di registrazione centralizzato
TOCTitle: Lettura dei log di acquisizione dal servizio di registrazione centralizzato
ms:assetid: c86ccf61-d86f-4ebd-b8d1-984a1b73005d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ721879(v=OCS.15)
ms:contentKeyID: 49887750
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lettura dei log di acquisizione dal servizio di registrazione centralizzato

 

_**Ultima modifica dell'argomento:** 2013-02-22_

I vantaggi offerti dal servizio di registrazione centralizzato diventano evidenti quando si esegue una ricerca e si ottiene un file che può essere utilizzato per individuare un problema segnalato. È possibile procedere in diversi modi per leggere il file. Il file di output è in un formato di testo standard e può essere aperto con Notepad.exe o con qualsiasi altro programma abilitato per l'apertura e la lettura di file di testo. Per file di grandi dimensioni e problemi più complessi, è possibile utilizzare uno strumento come Snooper.exe, progettato per leggere e analizzare l'output di registrazione del servizio di registrazione centralizzato. Snooper è incluso in Lync Server 2013 Debugging Tools, disponibile come download separato. Non sono disponibili scelte rapida da tastiera o voci di menu per Lync Server 2013 Debugging Tools. Dopo aver installato Lync Server 2013 Debugging Tools, aprire Esplora risorse, una finestra della riga di comando oppure Lync Server Management Shell e passare alla directory (percorso predefinito) C:\\Programmi\\Microsoft Lync Server 2013\\Debugging Tools. Fare doppio clic su Snooper.exe oppure digitare Snooper.exe e quindi premere INVIO qualora si utilizzi la riga di comando o Lync Server Management Shell.

> [!important]  
> Lo scopo di questo argomento non è descrivere nei dettagli le tecniche di risoluzione dei problemi. La risoluzione dei problemi e i processi correlati sono un argomento complesso. Per informazioni dettagliate sulle nozioni fondamentali per la risoluzione dei problemi e sui carichi di lavoro specifici della risoluzione dei problemi, vedere la documentazione di riferimento tecnico del Resource Kit di Microsoft Lync Server 2010 all'indirizzo <a href="http://go.microsoft.com/fwlink/?linkid=211003%26clcid=0x410" class="uri">http://go.microsoft.com/fwlink/?linkid=211003&amp;clcid=0x410</a>. I processi e le procedure si applicano anche a Lync Server 2013.

In Lync Server 2013 è stata introdotta una versione aggiornata di Snooper che include alcune nuove funzionalità. Nella cattura di schermata seguente viene mostrata la versione di Snooper di Office Communications Server 2007.

![Versione di Snooper per Office Communications 2007.](images/JJ721879.129503a8-8edd-4bb0-a68f-c43f9a548b93(OCS.15).jpg "Versione di Snooper per Office Communications 2007.")

Nella cattura di schermata seguente viene mostrata la nuova versione di Snooper inclusa in Lync Server 2013 Debugging Tools.

![Versione di Snooper per Lync Server 2013.](images/JJ721879.131495dd-8220-4ae4-af37-0ac5c318fd45(OCS.15).jpg "Versione di Snooper per Lync Server 2013.")

Nella cattura di schermata seguente viene mostrata la barra degli strumenti con le funzioni utilizzate più frequentemente.

![Barra degli strumenti di Snooper 2013.](images/JJ721879.989249c5-a33e-4251-b8b4-411019cc12b2(OCS.15).jpg "Barra degli strumenti di Snooper 2013.")

La funzionalità più recente che rappresenta un valore aggiunto è costituita dalla visualizzazione diagramma Flow Chart (call flow). Selezionare un flusso di messaggi nella scheda **Message** e quindi fare clic sul pulsante **Call Flow**. Man mano che si scorrono i messaggi, il diagramma del flusso di chiamate viene aggiornato con nuovi dati.

![Diagramma del flusso di chiamate di Snooper 2013.](images/JJ721879.bb8be45d-a842-48fe-86f8-380207d70bab(OCS.15).jpg "Diagramma del flusso di chiamate di Snooper 2013.")

È possibile posizionare il puntatore sulla visualizzazione diagramma e ottenere dettagli sui messaggi e sul contenuto dei flussi e dei messaggi, nonché sugli elementi del server. Fare clic sulla freccia di un flusso di chiamate per passare al messaggio nella visualizzazione Messages.

![Dettagli del messaggio relativo al diagramma del flusso di chiamate.](images/JJ721879.1147d720-38a9-4bda-8361-78f27ecde3d1(OCS.15).jpg "Dettagli del messaggio relativo al diagramma del flusso di chiamate.")

## Per aprire un file di log in Snooper

1.  Per utilizzare Snooper per aprire file di log, è necessario disporre dell'accesso in lettura per i file di log. Per utilizzare Snooper per accedere ai file di log, è necessario essere membri del gruppo di sicurezza di controllo di accesso basato sui ruoli (RBAC) CsAdministrator o CsServerAdministrator oppure di un ruolo RBAC personalizzato contenente uno di questi due gruppi.

2.  Dopo l'installazione di Lync Server Debugging Tools (LyncDebugTools.msi), passare alla directory di Snooper.exe utilizzando Esplora risorse oppure la riga di comando. Per impostazione predefinita, gli strumenti di debug sono posizionati in C:\\Programmi\\Microsoft Lync Server 2013\\Debugging Tools. Fare doppio clic su Snooper.exe oppure eseguire il programma.

3.  Dopo aver aperto Snooper, fare clic con il pulsante destro del mouse su **File**, scegliere **OpenFile**, individuare i file di log, selezionarne uno nella finestra di dialogo **Open** e quindi fare clic su **Open**.

4.  I messaggi di traccia **Trace** del file di log sono visualizzati nella scheda **Trace**. Fare clic sulla scheda **Messages** per visualizzare il contenuto dei messaggi delle tracce raccolte.

## Per visualizzare un diagramma del flusso di chiamate

1.  Per utilizzare Snooper per aprire file di log, è necessario disporre dell'accesso in lettura per i file di log. Per utilizzare Snooper per accedere ai file di log, è necessario essere membri del gruppo di sicurezza di controllo di accesso basato sui ruoli (RBAC) CsAdministrator o CsServerAdministrator oppure di un ruolo RBAC personalizzato contenente uno di questi due gruppi.

2.  Aprire un file di log e fare clic sulla scheda **Messages**, selezionare una conversazione nella visualizzazione dei messaggi oppure selezionare un componente di traccia nella scheda **Trace**.

3.  Fare clic su **Call Flow**.
    

    > [!NOTE]
    > Se si fa clic su un messaggio o una traccia che non fa parte di un flusso di chiamate, il diagramma non sarà disponibile e nella parte inferiore di Snooper verrà visualizzato un messaggio di stato "This message is not eligible for callfow", in cui viene indicato che il messaggio non è idoneo per il flusso di chiamate. Scegliere un altro messaggio o un'altra traccia e il flusso di chiamate verrà visualizzato, purché il messaggio o la traccia faccia parte di un flusso di chiamate.



4.  Scorrere i messaggi o le righe relative alle tracce e osservare se il diagramma del flusso di chiamate si aggiorna o cambia in un nuovo diagramma.

5.  Posizionare il puntatore sugli elementi per ottenere informazioni sui messaggi, gli endpoint delle chiamate e altri componenti.

