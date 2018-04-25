---
title: 'Lync Server 2013: Prerequisiti del plug-in VDI di Lync'
TOCTitle: Prerequisiti del plug-in VDI di Lync
ms:assetid: da25a976-7624-4dfc-b332-9c4db4ee78da
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205304(v=OCS.15)
ms:contentKeyID: 49302151
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Prerequisiti del plug-in VDI di Lync in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2015-07-20_

In un ambiente VDI (Virtual Desktop Infrastructure) le macchine virtuali e il computer locale dell'utente devono soddisfare i requisiti illustrati in questa sezione.


> [!NOTE]
> Per informazioni su come installare e distribuire un ambiente virtualizzato, contattare il provider della soluzione di virtualizzazione di cui si dispone. Per informazioni su come distribuire un ambiente virtualizzato basato su Hyper-V e Servizi Desktop remoto, vedere gli articoli seguenti nella libreria Microsoft TechNet: 
> <UL>
> <LI>
> <P>Hyper-V all'indirizzo <A class=uri href="http://go.microsoft.com/fwlink/p/?linkid=247514">http://go.microsoft.com/fwlink/p/?linkid=247514</A></P>
> <LI>
> <P>Servizi Desktop remoto in Windows Server&nbsp;2008&nbsp;R2 all'indirizzo <A class=uri href="http://go.microsoft.com/fwlink/p/?linkid=247513">http://go.microsoft.com/fwlink/p/?linkid=247513</A></P></LI></UL>



I requisiti per le macchine virtuali in esecuzione nel computer del data center sono i seguenti:

  - Le macchine virtuali devono essere configurate con Windows 8, Windows 7 o Windows Server 2008 R2 con i Service Pack più recenti.

I requisiti per l'utente e per il computer locale dell'utente sono i seguenti:

  - L'utente deve trovarsi in Lync Server 2013.

  - Nel computer locale deve essere in esecuzione Windows Embedded Standard 7 con SP1, Windows 7 con SP1 o Windows 8.

  - Se si utilizza Servizi Desktop remoto, il numero di bit del plug-in di Lync VDI (ovvero se l'applicazione è a 32 bit o a 64 bit) deve corrispondere al numero di bit del sistema operativo del computer locale. Il numero di bit del sistema operativo nel computer locale e del sistema operativo nella macchina virtuale non devono necessariamente corrispondere. Se si utilizza un'altra soluzione o piattaforma di virtualizzazione, fare riferimento alle indicazioni del provider della soluzione di virtualizzazione in uso per i requisiti del numero di bit.

  - Nel computer locale deve essere in esecuzione l'ultima versione del client Desktop remoto. Installare gli ultimi aggiornamenti del client Servizi Desktop remoto dal sito Microsoft oppure l'ultimo software del client desktop remoto fornito dal provider della soluzione di virtualizzazione di cui si dispone. Per gli ultimi aggiornamenti di Servizi Desktop remoto, vedere [http://go.microsoft.com/fwlink/p/?LinkId=268032](http://go.microsoft.com/fwlink/p/?linkid=268032).

  - Nel computer locale le impostazioni del client Desktop remoto devono essere configurate in modo che l'audio venga riprodotto nel computer locale e la registrazione remota sia disabilitata. Per configurare queste impostazioni per Connessione Desktop remoto in Windows, vedere la sezione successiva "Per configurare le impostazioni di Connessione Desktop remoto".

## Per configurare le impostazioni di Connessione Desktop remoto

Per preparare Connessione Desktop remoto in Windows per il plug-in di Lync VDI, eseguire le operazioni seguenti.

1.  Se nel computer locale è in esecuzione Windows 8, ignorare questo passaggio. Se invece nel computer locale è in esecuzione Windows 7 con SP1, installare l'ultima versione del client Servizi Desktop remoto per Windows 8 disponibile all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=268032](http://go.microsoft.com/fwlink/p/?linkid=268032).

2.  Avviare il client Servizi Desktop remoto facendo clic sul pulsante **Start** e quindi scegliendo **Connessione Desktop remoto** .

3.  Fare clic su **Opzioni** .

4.  Fare clic sulla scheda **Risorse locali** . In **Audio remoto** fare clic su **Impostazioni** e quindi eseguire le operazioni seguenti:
    
      - In **Riproduzione audio remoto** selezionare **Riproduci nel computer locale** .
    
      - In **Registrazione audio remoto** selezionare **Non registrare** .
    
      - Fare clic su **OK** .

5.  Fare clic sulla scheda **Esperienza** . In **Prestazioni** deselezionare la casella di controllo **Cache bitmap persistente** .

6.  Fare clic sulla scheda **Generale** . In **Computer** digitare il nome della macchina virtuale e quindi fare clic su **Connetti** .

