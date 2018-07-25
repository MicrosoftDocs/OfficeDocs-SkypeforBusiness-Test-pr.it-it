---
title: 'Lync Server 2013: Installazione dello strumento di pianificazione'
TOCTitle: Installazione dello strumento di pianificazione
ms:assetid: ebdc9e26-4b22-4b02-85b9-7462bcfe7c93
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg615046(v=OCS.15)
ms:contentKeyID: 52062467
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Installazione dello strumento di pianificazione in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-11-07_

Prima di iniziare la progettazione e la pianificazione dell'infrastruttura di Lync Server 2013 con Microsoft Lync Server 2013, Strumento di pianificazione, è necessario installare lo Strumento di pianificazione. Non è necessario distribuire lo Strumento di pianificazione in una workstation o in un server che fa parte del dominio o dell'infrastruttura in cui si prevede di installare Lync Server 2013. Nel file Leggimi fornito con Strumento di pianificazione vengono fornite informazioni importanti sull'installazione e l'utilizzo dello strumento. Alcune delle informazioni contenute nel file Leggimi vengono riportate in questo argomento per maggiore chiarezza.

> [!important]  
> L'installazione di Strumento di pianificazione in un computer deve essere eseguita da un utente che dispone di diritti e autorizzazioni di amministratore in tale computer.

I sistemi operativi supportati per l'installazione e il funzionamento dello Strumento di pianificazione sono i seguenti:

  - Windows 8

  - Windows 8,1

  - Windows Server 2012

  - Windows Server 2012 R2

  - Windows 7, edizione a 32 bit

  - Windows 7, edizione a 64 bit con Windows on Win32 (WOW)

  - Windows Server 2008 R2, con WOW

Inoltre, per lo Strumento di pianificazione è necessario Microsoft .NET Framework 4.5.

Quando i requisiti di pre-installazione sono soddisfatti, è possibile installare Strumento di pianificazione.

## Per installare lo strumento di pianificazione

1.  Accedere al computer locale come membro del gruppo Administrators.

2.  Utilizzando Esplora risorse o una finestra di comando, individuare la directory in cui sono stati scaricati i file di installazione dello Strumento di pianificazione .

3.  Individuare il file LyncPlanningTool.msi e fare doppio clic su di esso in Esplora risorse. Nella finestra di comando digitare il nome del file e quindi premere **INVIO** per eseguirlo.

4.  Nella pagina iniziale dell'installazione guidata dello strumento di pianificazione di Microsoft Lync Server 2013 fare clic su **Avanti** .

5.  Leggere il **Contratto di Licenza con l'utente finale** , selezionare **Accetto i termini del Contratto di Licenza** se si sceglie di accettare le condizioni per l'utilizzo riportate nel contratto e quindi fare clic su **Avanti** .

6.  Scegliere dove installare i file dello strumento di pianificazione. Il percorso predefinito è C:\\Program Files (x86)\\Microsoft Lync Server 2013\\Planning Tool. Se si desidera cambiarlo, fare clic su **Cambia** . In **Modifica cartella di destinazione** , individuare o digitare il percorso in cui installare i file, fare clic su **OK** e quindi su **Avanti** .

7.  A questo punto è possibile installare lo Strumento di pianificazione. Fare clic su **Installa** per avviare il processo di installazione.

8.  L'installazione verrà avviata e verrà visualizzato il relativo stato. Al termine dell'installazione, fare clic su **Fine** .

9.  È ora possibile utilizzare lo Strumento di pianificazione.

## Vedere anche

#### Concetti

[Installazione di software facoltativo in Lync Server 2013](lync-server-2013-installing-optional-software.md)

