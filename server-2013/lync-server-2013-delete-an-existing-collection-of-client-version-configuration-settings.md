---
title: Eliminare una raccolta esistente di impostazioni di configurazione delle versioni client
TOCTitle: Eliminare una raccolta esistente di impostazioni di configurazione delle versioni client
ms:assetid: 70bf1216-d0d2-45ce-881f-b8edadf3cec7
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ898480(v=OCS.15)
ms:contentKeyID: 52062182
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eliminare una raccolta esistente di impostazioni di configurazione delle versioni client

 

_**Ultima modifica dell'argomento:** 2013-02-23_

Se si desidera rimuovere le impostazioni di configurazione client precedentemente configurate per un sito, è possibile utilizzare il Pannello di controllo di Lync Server 2013 o Lync Server 2013 Management Shell.

## Per rimuovere le impostazioni di configurazione client tramite il Pannello di controllo di Lync Server

1.  Da un account utente assegnato al ruolo CsUserAdministrator o CsAdministrator, accedere a qualsiasi computer nella distribuzione interna.

2.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

3.  Sulla barra di spostamento sinistra fare clic su **Client** e quindi sul pulsante di spostamento **Configurazione versione client**.

4.  Selezionare il sito, fare clic su **Modifica** e su **Elimina**, quindi fare clic su **OK**.

## Rimozione delle impostazioni di configurazione delle versioni client tramite i cmdlet di Windows PowerShell

Per eliminare le impostazioni di configurazione delle versioni client, è possibile utilizzare il cmdlet **Remove-CsClientVersionConfiguration**. È possibile eseguire questo cmdlet da Lync Server 2013 Management Shell o da una sessione remota di Windows PowerShell. Per informazioni dettagliate sull'utilizzo di Windows PowerShell remoto per la connessione a Lync Server, vedere l'articolo "Avvio rapido: gestione di Microsoft Lync Server 2010 con PowerShell remoto" nel blog su Windows PowerShell per Lync Server all'indirizzo [http://go.microsoft.com/fwlink/p/?linkId=255876](http://go.microsoft.com/fwlink/p/?linkid=255876).

## Per rimuovere una raccolta specificata di impostazioni di configurazione delle versioni client

  - Il comando seguente rimuove le impostazioni di configurazione delle versioni client applicate al sito Redmond:
    
        Remove-CsClientVersionConfiguration -Identity "site:Redmond"

## Per rimuovere tutte le impostazioni di configurazione delle versioni client applicate all'ambito del sito

  - Questo comando rimuove tutte le impostazioni di configurazione delle versioni client configurate nell'ambito del sito:
    
        Get-CsClientVersionConfiguration -Filter site:* | Remove-CsClientVersionConfiguration

## Per rimuovere tutte le impostazioni di configurazione delle versioni client basate sul valore della proprietà DefaultAction

  - Questo comando rimuove tutte le impostazioni di configurazione delle versioni client per le quali l'azione predefinita è impostata su "Block":
    
        Get-CsClientVersionConfiguration | Where-Object {$_.DefaultAction -eq "Block" | Remove-CsClientVersionConfiguration

Per informazioni dettagliate, vedere l'argomento della Guida relativo al cmdlet [Remove-CsClientVersionConfiguration](remove-csclientversionconfiguration.md).

