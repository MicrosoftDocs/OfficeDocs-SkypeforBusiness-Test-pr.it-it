---
title: Eliminare criteri per il PIN
TOCTitle: Eliminare criteri per il PIN
ms:assetid: 7c378927-2e41-418e-9721-327021bd2e45
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg521020(v=OCS.15)
ms:contentKeyID: 49301099
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminare criteri per il PIN

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Eseguire la procedura seguente per eliminare criteri PIN.


> [!NOTE]
> Non è possibile eliminare criteri PIN globali.



## Per eliminare criteri PIN in Pannello di controllo di Lync Server 2013

1.  Da un account utente membro del gruppo RTCUniversalServerAdmins (o con diritti utente equivalenti) oppure assegnato al ruolo CsServerAdministrator o CsAdministrator, accedere a un computer nella rete in cui è stato distribuito Lync Server 2013.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Sicurezza** e quindi su **Criteri PIN**.

4.  Nella pagina **Criteri PIN** e nel campo di ricerca digitare il nome, o parte di esso, dei criteri che si desidera eliminare.

5.  Nell'elenco di criteri fare clic sui criteri desiderati, fare clic su **Modifica** e quindi su **Elimina**.

6.  Fare clic su **OK**.

## Rimozione di criteri PIN attraverso Lync Server Management Shell e cmdlet

È possibile rimuovere criteri PIN utilizzando Windows PowerShell e il cmdlet Remove-CsPinPolicy. Questo cmdlet può essere eseguito da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Rimozione di un criterio PIN specifico

  - Questo comando rimuove il criterio PIN con identità (Identity) RedmondPinPolicy:
    
        Remove-CsPinPolicy -Identity "RedmondPinPolicy"

## Rimozione di tutti i criteri PIN applicati all'ambito sito

  - Questo comando rimuove tutti i criteri PIN configurati nell'ambito sito:
    
        Get-CsPinPolicy -Filter "site:*" | Remove-CsPinPolicy

## Rimozione di tutti i criteri PIN che consentono l'utilizzo di formati comuni

  - Questo comando rimuove tutti i criteri PIN che consentono l'utilizzo di formati comuni:G
    
        et-CsPinPolicy | Where-Object {$_.AllowCommonPatterns -eq $True} | Remove-CsPinPolicy

Per ulteriori informazioni, vedere l'argomento della Guida relativo al cmdlet [Remove-CsPinPolicy](https://docs.microsoft.com/en-us/powershell/module/skype/Remove-CsPinPolicy).

