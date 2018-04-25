---
title: Rimuovere file di aggiornamento dispositivi non associati a un dispositivo
TOCTitle: Rimuovere file di aggiornamento dispositivi non associati a un dispositivo
ms:assetid: ecebbf73-b456-4990-a91d-308b84d39404
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ994084(v=OCS.15)
ms:contentKeyID: 52062468
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Rimuovere file di aggiornamento dispositivi non associati a un dispositivo

 

_**Ultima modifica dell'argomento:** 2013-02-20_

Ogni volta che sul sistema vengono caricati degli aggiornamenti dei dispositivi, viene creata una corrispondente regola di aggiornamento dei dispositivi. Per impostazione predefinita, questa nuova regola di aggiornamento dei dispositivi viene assegnata allo stato Pending; ciò significa che la regola può essere scaricata e installata su dispositivi di prova ma non su dispositivi in produzione. In questo modo, è possibile provare gli aggiornamenti prima di renderli disponibili agli utenti. In base ai risultati dei test, si accetta e distribuisce l'aggiornamento o lo si rifiuta ed elimina. Quando si rifiuta un aggiornamento, viene annullata l'associazione tra l'aggiornamento e la corrispondente regola.


I file di aggiornamento dei dispositivi che non sono più associati a un dispositivo possono essere rimossi tramite Windows PowerShell e il cmdlet **Clear-CsDeviceUpdateFile**. Questo cmdlet può essere eseguito in Lync Server 2013 Management Shell o in una sessione remota di Windows PowerShell.


> [!NOTE]
> Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=255876">http://go.microsoft.com/fwlink/p/?linkId=255876</A>.




  - Ad esempio, il comando seguente rimuove dal server Web atl-cs-001.litwareinc.com qualsiasi regola di aggiornamento dei dispositivi non più associata a un dispositivo:
    
        Clear-CsDeviceUpdateFile -Identity "service:WebServer:atl-cs-001.litwareinc.com"

Per informazioni dettagliate, vedere l'argomento della guida relativo al cmdlet [Clear-CsDeviceUpdateFile](clear-csdeviceupdatefile.md).

