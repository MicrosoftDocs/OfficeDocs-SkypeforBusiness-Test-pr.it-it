---
title: Eliminare i file di log dell'aggiornamento dispositivi
TOCTitle: Eliminare i file di log dell'aggiornamento dispositivi
ms:assetid: 58d4097f-5bbf-4824-a04d-2a6555cd93c3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994039(v=OCS.15)
ms:contentKeyID: 52062163
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminare i file di log dell'aggiornamento dispositivi

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Il servizio Web di aggiornamento dispositivi crea e mantiene aggiornata un'ampia raccolta di file di log, che include sia log di controllo gestiti dal servizio stesso che file di log caricati dai dispositivi client. Per evitare che il server si riempia con i log del servizio Web di aggiornamento dispositivi, è probabile che sia necessario eliminare i file di log dopo un certo numero di giorni. È possibile impostare tale numero di giorni in base all'attività di aggiornamento e al numero di dispositivi client nell'organizzazione, utilizzando il Pannello di controllo di Lync Server o Lync Server Management Shell.

## Per cancellare il log di aggiornamento dei dispositivi tramite Pannello di controllo di Lync Server

1.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

2.  Sulla barra di spostamento sinistra fare clic su **Client** e quindi su **Configurazione log dispositivo**.

3.  Nella pagina **Configurazione log dispositivo** fare doppio clic sulla configurazione che si desidera modificare.

4.  Nella finestra di dialogo **Modifica impostazione log** specificare un numero di giorni in **Giorni per la conservazione dei file di log (1-365)**.

5.  Fare clic su **Commit**. Verranno eliminati tutti i file rimasti nel server per un numero di giorni maggiore di quello specificato. L'impostazione verrà applicata alla configurazione fino a quando non la si modifica.

## Cancellazione de log di aggiornamento dei dispositivi tramite i cmdlet di Windows PowerShell

È possibile cancellare i log di aggiornamento dei dispositivi tramite Windows PowerShell e il cmdlet **Clear-CsDeviceUpdateLog**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell.


> [!NOTE]
> Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=255876">http://go.microsoft.com/fwlink/p/?linkId=255876</A>.



## Per cancellare i log di aggiornamento dei dispositivi in un solo server

  - Il comando seguente consente di cancellare il log di aggiornamento dei dispositivi nel server Web atl-cs-001.litwareinc.com. Verranno rimosse dal log tutte le voci di log esistenti da più di 10 giorni, ovvero il valore specificato con il parametro DaysBack.
    
        Clear-CsDeviceUpdateLog -Identity "service:WebServer:atl-cs-001.litwareinc.com" -DaysBack 10

## Per cancellare tutti i log di aggiornamento dei dispositivi

  - Il comando seguente consente di rimuovere le voci obsolete (in questo esempio le voci esistenti da più di 10 giorni) da tutti i log di aggiornamento dei dispositivi attualmente in uso nell'organizzazione.
    
        Get-CsService -WebServer | Foreach-Object {Clear-CsDeviceUpdateLog -Identity $_.Identity -DaysBack 10}

Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet [Clear-CsDeviceUpdateLog](clear-csdeviceupdatelog.md).

