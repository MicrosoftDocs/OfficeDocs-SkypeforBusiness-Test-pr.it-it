---
title: Eliminare un criterio delle versioni client esistente
TOCTitle: Eliminare un criterio delle versioni client esistente
ms:assetid: b88aaa25-97ff-4eb6-bd34-b97332cd6890
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ923064(v=OCS.15)
ms:contentKeyID: 52062251
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminare un criterio delle versioni client esistente

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Se si desidera eliminare criteri delle versioni client configurati in precedenza, è possibile eliminarli dal Pannello di controllo di Lync Server 2013 o da Lync Server 2013 Management Shell.

## Per eliminare criteri delle versioni client utilizzando il Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Client** e quindi sul pulsante di spostamento **Criteri versione client**.

4.  Nella pagina **Criteri versione client** selezionare uno o più criteri delle versioni client da eliminare, fare clic su **Modifica** e quindi su **Elimina**.

## Eliminazione di criteri delle versioni client utilizzando i cmdlet di Windows PowerShell

È possibile eliminare criteri delle versioni client utilizzando il cmdlet **Remove-CsClientVersionPolicy**. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per rimuovere criteri delle versioni client specifici

  - Questo comando elimina i criteri delle versioni client applicati al sito Redmond:
    
        Remove-CsClientVersionPolicy -Identity site:Redmond

## Per rimuovere tutti i criteri delle versioni client applicati all'ambito del sito

  - Questo comando rimuove tutti i criteri delle versioni client configurati nell'ambito sito:
    
        Get-CsClientVersionPolicy -Fiter "site:*" | Remove-CsClientVersionPolicy

## Per rimuovere i criteri delle versioni client che non includono un agente utente specifico

  - Questo comando rimuove qualsiasi criterio delle versioni client che non includa una regola per l'agente utente Windows Phone Lync (WPLync):
    
        Get-CsClientVersionPolicy | Where-Object {$_.Rules -notmatch "UserAgent=WPLync" | Remove-CsClientVersionPolicy

Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet [Remove-CsClientVersionPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsClientVersionPolicy).

